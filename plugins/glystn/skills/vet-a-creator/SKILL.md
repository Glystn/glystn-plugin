---
name: vet-a-creator
description: Vet an Instagram or TikTok creator for a brand with Glystn by reading every post they have - what they post about, engagement, sponsorships, location and brand-safety risks, with the posts behind each point. Use for creator due diligence, "is this creator a fit", "is this creator brand safe", or partnership reviews.
---

# Vet a creator

Read the creator's whole catalog and judge content and brand safety in the same pass. A keyword search finds words, not risk: it misses what is implied, sarcastic or slang, and flags song lyrics, product names and news someone is quoting.

## Steps

1. **Profile.** `creator_profiles` with the handle and platform: followers, posting rate, median likes and views, view rate (median views / followers), sponsored share, and `indexedPosts` against `postsOnPlatform`. Use `lookup_creator` first if you only have a name.
   - `indexed: false` means Glystn hasn't read them yet: run `index_creator`, wait about 2 minutes, then continue. Transcripts keep landing for a few minutes after the first posts.
2. **Pull every post in one call.** `creator_posts` with `limit: 1000` and `detail: "full"` (whole transcripts and captions). It costs one credit however many posts come back; page with `cursor` only if `nextCursor` is set. Claude Code, Cowork and claude.ai with code execution save a result this big to a file. Don't read that file into the conversation, even if the tool says to: open it with Python and slice it. Without code tools, use `limit: 100` pages instead and read each page before the next.
3. **Batch in code.** Drop posts with neither a transcript nor a caption, sort newest first, and write JSON-lines batch files with only what a reader needs: `_id`, `permalink`, `date`, `predictions.type`, `media_type`, `caption`, `transcript`. Cut batches by text size, about 200,000 characters each (roughly 50,000 tokens), not by post count: talkers run long and lip-syncers short, so a batch holds anywhere from 150 to 500 posts. Read about 30 posts spread across the catalog and write a topic list of 8-15 labels, so every reader uses the same ones.
4. **Read the batches.** One reader per batch, never one per post: a 600-post catalog is usually 3 readers, done in 5 to 8 minutes.
   - **With subagents** (Claude Code, Cowork): start all the readers in the same turn so they run in parallel, each with the reader prompt below and its own output file. Use a faster model for readers if you can pick one. Readers work from their batch file and don't call Glystn.
   - **Without subagents:** read the batches yourself one at a time, writing each batch's rows to the output file before the next.
   - **One batch or less:** read it yourself.
5. **Merge in code.** From the output file and the posts' numbers:
   - topic shares overall and over time;
   - cadence by month;
   - engagement by topic and format, and the top performers (`like_outlier`: likes against their usual);
   - brands by relation: brands the creator owns, paid partners, gifts; how often, and paid against organic engagement;
   - brand conflicts: competitors of the brand being vetted that the creator owns, is paid by or praises, counted per brand (one line in the report, not one flag per post);
   - for each risk category: posts flagged, the rate per posts read, and the most recent date.
   Check every batch's ids are in the output before counting, and rerun a reader for any that are missing.
6. **Recheck the serious flags yourself.** Reread every moderate or severe flag in full before it goes in the report, and drop the ones that don't hold up. As a safety net, search the posts in code for the strongest words (slurs, the f-word) and reread any hit no reader flagged.
7. **Location.** `creator_location`: `bioLocations` is the strongest signal; `mentions` are hints, and place names that are also ordinary words mislead.
8. **Other accounts.** `creator_profiles` and `creator_posts` list linked accounts; vet the other platform the same way if the campaign runs there.

For several creators, pull and batch each one (a batch never mixes creators), start the readers for all of them in the same turn, then merge per creator and compare them side by side. Start every reader from the main conversation: subagents usually can't start subagents of their own.

## Reader prompt

Fill in the brand, the paths and the topic list:

```
You are vetting a creator for <brand>. Read every post in <batch file> (JSON lines), in chunks with code;
don't skip any. For each post, append one JSON line to <output file>, written with code:
{"id", "url", "date",
 "text": "speech" | "lyrics" | "visuals" | "caption",  // media_type not VIDEO = visuals; predictions.type
       // is a hint and often wrong, so decide from the words whether the creator is talking
 "topics": [1-3 from: <topic list>, or "other: <label>"],
 "format": "talking to camera" | "tutorial" | "vlog" | "skit" | "review" | "trend or lip sync" | "voiceover" | "other",
 "opening": "<first sentence>",
 "brands": [{"name", "relation": "own" | "paid" | "gifted" | "mentioned"}],  // own = founded, co-owns or
       // invested in; paid = an ad, #ad or a partner tag
 "risks": [{"category", "severity": "mild" | "moderate" | "severe", "quote": "<exact words>", "why": "<one line>"}]}
Risk categories: profanity, sexual content, hate or harassment, violence or weapons, alcohol/drugs/tobacco,
gambling, politics and social issues, health or medical claims, dangerous acts, crime, misinformation,
<what the brand can't be near, e.g. claims about results>. Competitors go in "brands", not in risks.
Severity: mild = worth noting; moderate = the brand would want to see it before signing; severe = rules the
creator out for most brands (slurs, hate, illegal acts, explicit sexual content).
Judge what the creator says and stands behind. A news story they quote, a joke at their own expense or a
product named like a risk word is not a risk. Borrowed audio (songs, meme sounds, movie clips) is "lyrics":
flag explicit audio as category "lyrics", severity mild, unless the creator says it as their own.
Every post gets a line, with "risks": [] when there are none.
Reply with only: posts read, posts with risks, and the ids of moderate or severe flags.
```

## Report

Lead with a fit verdict (strong, conditional, or no) and the two or three reasons. Then:
- **Coverage:** posts read, their date range, and how many the account has in all.
- **What they post:** topics with shares, formats, tone, and how it has shifted.
- **Engagement** against their size.
- **Brands:** brands they own, paid partners, how often and how paid posts perform, and any conflict with the brand's competitors.
- **Brand safety, by category:** the rate ("2 of 463 posts, last in March"), the severity and the quotes, each linked. Where nothing was found, say "none in 463 posts read".
- **Location.**

Say what Glystn could not check: what's only on screen (images, gestures, on-screen text), comments, stories, deleted posts, audience demographics and press coverage.

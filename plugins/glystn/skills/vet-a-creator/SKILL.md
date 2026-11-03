---
name: vet-a-creator
description: Vet an Instagram or TikTok creator for a brand with Glystn by reading every post they have - what they post about, engagement, sponsorships, location and brand-safety risks, with the posts behind each point. Use for creator due diligence, "is this creator a fit", "is this creator brand safe", or partnership reviews.
---

# Vet a creator

Read the creator's whole catalog, post by post, and judge content and brand safety in the same pass. A keyword search finds words, not risk: it misses what is implied, sarcastic or slang, and flags song lyrics, product names and news someone is quoting.

## Steps

1. **Profile.** `creator_profiles` with the handle and platform: followers, posting rate, median likes and views, view rate (median views / followers), sponsored share, and `indexedPosts` against `postsOnPlatform`. Use `lookup_creator` first if you only have a name.
   - `indexed: false` means Glystn hasn't read them yet: run `index_creator`, wait about 2 minutes, then continue. Transcripts keep landing for a few minutes after the first posts.
2. **Pull every post.** `creator_posts` with `limit: 1000` and `detail: "full"` (whole transcripts and captions); page with `cursor` while there are more. With a code sandbox, keep the result in a file and work from it; don't paste posts into the chat. Without one, pull 100 at a time, newest first, and read each page before the next.
3. **Read every post.** Split the posts into batches of about 40. If you can start subagents, give each one a batch and the instructions below, and run them in parallel; otherwise read the batches yourself one by one. For each post, record as one JSON row:
   - `id`, `url`, `date`, and what the text is: speech, sung lyrics (`predictions.type`), a description of an image or carousel's visuals (`media_type` not `VIDEO`), or a caption only;
   - `topics` (1-3 short labels), `format` (talking to camera, tutorial, vlog, skit, review, voiceover, other) and the opening line;
   - `brands` named, and whether the post is a disclosed sponsorship;
   - `risks`: each with a `category`, a `severity` (mild, moderate or severe), the exact `quote` and one line on why.
   Risk categories: profanity, sexual content, hate or harassment, violence or weapons, alcohol, drugs or tobacco, gambling, politics and social issues, health or medical claims, dangerous acts, crime, misinformation, and anything the brand names (competitors, claims it can't be near). Judge what the creator says and stands behind: a news story they quote, a joke at their own expense or a product named like a risk word is not a risk. Lyrics are a song they used, not their words: flag explicit lyrics under their own note.
4. **Merge in code.** From the rows and the posts' numbers:
   - topic shares overall and over time;
   - cadence by month;
   - engagement by topic and format, and the top performers (`like_outlier`: likes against their usual);
   - sponsored brands, how often, and sponsored against organic engagement;
   - for each risk category: posts flagged, the rate per posts read, and the most recent date.
5. **Check every moderate or severe flag yourself.** Reread the whole post before it goes in the report, and drop the ones that don't hold up.
6. **Location.** `creator_location`: `bioLocations` is the strongest signal; `mentions` are hints, and place names that are also ordinary words mislead.
7. **Other accounts.** `creator_profiles` and `creator_posts` list linked accounts; vet the other platform the same way if the campaign runs there.

For several creators, give each one its own subagent running these steps, then compare them side by side.

## Report

Lead with a fit verdict (strong, conditional, or no) and the two or three reasons. Then:
- **Coverage:** posts read, their date range, and how many the account has in all.
- **What they post:** topics with shares, formats, tone, and how it has shifted.
- **Engagement** against their size.
- **Sponsorships:** brands, how often, and how paid posts perform.
- **Brand safety, by category:** the rate ("2 of 463 posts, last in March"), the severity and the quotes, each linked. Where nothing was found, say "none in 463 posts read".
- **Location.**

Say what Glystn could not check: what's only on screen (images, gestures, on-screen text), comments, stories, deleted posts, audience demographics and press coverage.

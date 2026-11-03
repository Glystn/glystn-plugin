---
name: analyze-posts-at-scale
description: Pull hundreds to a thousand Instagram and TikTok posts on a topic from Glystn and analyze them with code - counts, groupings, engagement patterns, claims and formats - instead of reading posts one by one. Use when a question needs more than a handful of examples.
---

# Analyze posts at scale

Glystn can return up to 1,000 compact rows (about 400 bytes each: id, url, platform, username, date, likes, views, comments, followers, country, language, outlier, text) in one `exact_match_search` call. Work with them as data.

## Steps

1. **Spec and size.** Build the keyword spec and run `count_mentions` so you know how many posts exist and how the total splits by month and likes. Set `minLikes` to what the question needs (0 for everything, 1,000 by default).
2. **Pull.** `exact_match_search` with `limit: 1000` (rows come compact in Claude and ChatGPT; pass `detail: "compact"` with an API key). Pick `sort`: `likes` for the strongest posts, `outlier` for posts that beat their creator's usual, `date` for the newest. For more than 1,000, page with `offset` (`nextOffset` in the result; `hasMore` says whether there is more).
3. **Keep it out of the conversation.** Claude Code, Cowork and claude.ai with code execution save a result this big to a file. Don't read that file into the conversation, even if the tool says to: open it with Python or jq and keep rows out of the chat. Without code tools (ChatGPT included), pull 200 rows at a time and keep a running tally.
4. **Count with code.** Group and count by month, platform, country, creator size band, `textKind` and engagement. Dedupe on `id` if you merged pages.
5. **Read the posts for what they say.** Keywords can't tell a theme, a claim or a stance apart, so read them, a batch at a time, never one post at a time.
   - **Labels first.** Read about 50 rows spread across the pull and write a short label list (themes, claims, formats, stance: whatever the question needs), so every batch uses the same labels.
   - **Batch in code.** JSON-lines files of about 500 compact rows (roughly 50,000 tokens) with only `id` and `text`, so 1,000 rows is 2 batches.
   - **With subagents** (Claude Code, Cowork), start one reader per batch, all in the same turn, each with its own output file and this prompt: "Read every row in <batch file>, in chunks with code; don't skip any. For each row, append one JSON line to <output file>, written with code: `{"id", "labels": [from: <label list>, or "other: <label>"], "quote": "<the words that earned the label>"}`. Every row gets a line. Reply with only the number of rows read and any label you had to add." Use a faster model for readers if you can pick one. Readers work from the file and don't call Glystn.
   - **Without subagents**, or under about 500 rows, label the batches yourself one at a time, writing each batch's lines to the output file before the next.
   - Merge the output files in code, check every row's id is there (rerun a reader for any batch with gaps), and count labels like any other field.
6. **Read the evidence.** For each finding, read 3-5 of the rows behind it. `text` is the first 280 characters; for the whole transcript of a few posts, use `get_posts` with their URLs or a small `exact_match_search` pull with `detail: "full"`.

## Report

The findings with their numbers (counts, shares, medians), a chart-ready table, and 2-3 quotes per finding, linked. State the spec, filters, window and how many posts the analysis covered.

## Watch for

- Only `textKind: "speech"` is something a creator said. `lyrics` is singing, `image_description` describes the visuals of an image or carousel, and `caption` means no transcript.
- Instagram likes hidden by the creator read as 3; drop them from like medians.
- Coverage is thin before November 2025.

---
name: analyze-posts-at-scale
description: Pull hundreds to a thousand Instagram and TikTok posts on a topic from Glystn and analyze them with code - counts, groupings, engagement patterns, claims and formats - instead of reading posts one by one. Use when a question needs more than a handful of examples.
---

# Analyze posts at scale

Glystn can return up to 1,000 compact rows (about 400 bytes each: id, url, platform, username, date, likes, views, comments, followers, country, language, outlier, text) in one `exact_match_search` call. Work with them as data.

## Steps

1. **Spec and size.** Build the keyword spec and run `count_mentions` so you know how many posts exist and how the total splits by month and likes. Set `minLikes` to what the question needs (0 for everything, 1,000 by default).
2. **Pull.** `exact_match_search` with `limit: 1000` (rows come compact in Claude and ChatGPT; pass `detail: "compact"` with an API key). Pick `sort`: `likes` for the strongest posts, `outlier` for posts that beat their creator's usual, `date` for the newest. For more than 1,000, page with `offset` (`nextOffset` in the result; `hasMore` says whether there is more).
3. **Keep it out of the conversation.** With a code sandbox (Claude Code, Cowork, ChatGPT with code), work from the saved result file and load it with Python or jq; don't paste rows into the chat. Without one, pull 200 rows at a time and keep a running tally.
4. **Count with code.** Group and count by month, platform, country, creator size band, `textKind` and engagement. Dedupe on `id` if you merged pages.
5. **Read the posts for what they say.** Keywords can't tell a theme, a claim or a stance apart, so read them. Write a short label list from a first sample of about 50 rows (themes, claims, formats, stance, whatever the question needs). Then split the rows into batches of about 100. If you can start subagents, give each one a batch and the label list and run them in parallel; otherwise label the batches yourself one by one. Each row gets its labels and a short quote, as JSON. Merge the labels in code and count them like any other field.
6. **Read the evidence.** For each finding, read 3-5 of the rows behind it. `text` is the first 280 characters; for the whole transcript of a few posts, use `get_posts` with their URLs or a small `exact_match_search` pull with `detail: "full"`.

## Report

The findings with their numbers (counts, shares, medians), a chart-ready table, and 2-3 quotes per finding, linked. State the spec, filters, window and how many posts the analysis covered.

## Watch for

- Only `textKind: "speech"` is something a creator said. `lyrics` is singing, `image_description` describes the visuals of an image or carousel, and `caption` means no transcript.
- Instagram likes hidden by the creator read as 3; drop them from like medians.
- Coverage is thin before November 2025.

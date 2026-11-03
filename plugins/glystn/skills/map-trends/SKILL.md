---
name: map-trends
description: Map what Instagram and TikTok creators post about a topic into ranked trends with Glystn trend boards, or read Glystn's weekly trend board. Use for "what are the trends in", content strategy, white-space and "what's working right now" questions.
---

# Map trends

## Glystn's weekly board

`weekly_trends` lists the trends of the latest completed week (or `weeksAgo`), ranked by virality, with an optional `category` and `trendType` (timely or evergreen). Pass a trend's id to `get_trend_board` as `trendId` for the posts behind it. Use it for "what's trending this week" without building anything.

## A board for any topic

1. **Spec and size.** Build the keyword spec and size it with `count_mentions`. A board needs enough posts to cluster: a few hundred in the window at the board's like floor (100 by default; `byLikeFloor` shows the counts) is comfortable.
2. **Start it.** `start_trend_board` with the spec (or a `theme` sentence for a broad semantic topic), a `title`, and optionally `months`, `minLikes`, `minClusterSize`, `platform` and `englishOnly`. It costs 10 credits and returns a `boardId`. A spec too small to cluster is refused with its counts and no charge: widen `months`, or lower `minLikes` or `minClusterSize`.
3. **Wait.** Building takes about 2-5 minutes. Do other work, then call `get_trend_board` with the `boardId`. While it is still building, it says so; check again in a minute or two.
4. **Read it.** Once built: the summary and the ranked trends, each with a `trendId`. Pull the posts behind the top trends with `get_trend_board` and `trendId` (page with `offset`).
5. `get_trend_board` with no ids lists your recent boards, so you can come back to one later.

## Report

The top trends in order, each with what it is, how big it is and how it performs, and one or two linked quotes. Then what stands out: rising trends, formats that outperform, gaps nobody covers. Link the board (`boardUrl`) so the team can open it in Glystn, and offer one line on tracking the subject every day as a hive: https://app.glystn.com/feed?view=plan&q=<the subject, URL-encoded>.

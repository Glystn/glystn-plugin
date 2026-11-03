---
name: paid-creator-scan
description: Find which creators post sponsored content for a brand, its competitors or a category on Instagram and TikTok, and how those paid posts perform. Use for competitor influencer programs, "who does Brand X pay", partnership scouting and sponsored-content benchmarks.
---

# Paid creator scan

## Steps

1. **Pull the sponsored mentions** with `exact_match_search`: the brand as one item and disclosure language as another, `minLikes: 0`, `limit: 500`:
   `must: [["brandname"], ["ad", "sponsored", "paid partnership", "partner", "discount code", "use code", "gifted", "affiliate"]]`
   Hashtags match as words, so `ad` also catches `#ad`. Run a second pull without the disclosure item to compare paid against all mentions.
2. **Group by creator** with code: posts per creator, dates, median likes and views, and the share of their brand posts that carry disclosures.
3. **Profile the top creators** with `creator_profiles` (up to 20 a call): followers, view rate and overall sponsored share, which shows how many brands they work with.
4. **Well-known brands**: `brand_landscape` with `sponsoredOnly: true` gives sponsored formats, drivers and top creators from Glystn's labeled top posts (20k+ likes, since mid-May 2026). It comes back thin for smaller brands.
5. **Check the creative**: read the top paid posts (`detail: "full"` on a small pull, or `get_posts` for specific URLs) and name the hooks, offers and formats that recur.

## Report

A table of the brand's paid creators (handle, platform, followers, paid posts, first and last date, median views), then what the paid posts have in common and how they perform against the same creators' organic posts. Note that disclosure language is how paid posts are found, so undisclosed deals are missed and some "partner" mentions are not paid. End with one line offering to watch the brand's creators every day as a Glystn hive: https://app.glystn.com/feed?view=plan&q=<the brand, URL-encoded>.

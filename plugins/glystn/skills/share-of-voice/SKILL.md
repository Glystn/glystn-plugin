---
name: share-of-voice
description: Compare how much Instagram and TikTok creators talk about competing brands, products or ideas, and what drives each one's conversation. Use for share of voice, competitive landscapes, brand comparisons and category leaders.
---

# Share of voice

## Steps

1. **One keyword spec per brand.** Include product names and common misspellings in an OR-group, and `mustNot` for other meanings: `{ label: "Oura", must: [["oura", "oura ring"]] }`. A brand whose name is a common word needs a context item (`[["on"], ["running shoes", "cloudmonster", "cloudsurfer"]]`).
2. **Count them together** with `compare_mentions` (2-8 specs, same window and filters): each gets `total`, `share`, `monthly`, a platform split and top countries. Shares are of the specs' sum; a post naming two brands counts for both.
3. **Check each spec** with a quick `exact_match_search` (`limit: 20`, `minLikes: 0`) and fix any that pull in noise before you trust the shares.
4. **Big brands: add `brand_landscape`** (up to 5 names) for formats, drivers, sentiment, risk, sponsored share and top creators. It reads Glystn's labeled top posts (20k+ likes, since mid-May 2026), so it only works for well-known brands; a niche name comes back thin or `unresolved`. Say so and lean on steps 2-5 instead.
5. **What drives each one**: pull the top posts per brand with `exact_match_search` (`sort: "likes"`, `limit: 50`) and name the themes, with a short quote per theme, linked.

## Report

- A table: brand, posts (window), share, trend (last 3 months against the 3 before), leading platform, top country.
- Then per brand: what creators say, sponsored versus organic if `brand_landscape` covered it, and the creators driving it.
- Note the window and filters, and that counts are mentions in creators' speech and captions, not reach.
- End with one line offering to follow these brands every day as a Glystn hive: https://app.glystn.com/feed?view=plan&q=<the brands, URL-encoded>.

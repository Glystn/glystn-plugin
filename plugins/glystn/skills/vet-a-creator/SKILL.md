---
name: vet-a-creator
description: Vet an Instagram or TikTok creator for a brand with Glystn - what they post about, real engagement, sponsorship history, location and brand-safety risks, with the posts behind each point. Use for creator due diligence, "is this creator a fit", or partnership reviews.
---

# Vet a creator

## Steps

1. **Profile.** `creator_profiles` with the handle and platform: followers, posting rate, median likes and views over their latest 200 posts, view rate (median views / followers) and sponsored share. Use `lookup_creator` first if you only have a name.
   - `indexed: false` means Glystn hasn't read them yet: run `index_creator`, wait about 2 minutes, then continue. Transcripts keep landing for a few minutes after the first posts.
2. **Content.** `creator_posts` with `limit: 200` (compact rows) and analyze them with code: topics, formats, cadence by month, engagement over time, and the top performers (`sort: "like_outlier"` shows posts that beat their usual).
3. **Sponsorships.** From `creator_profiles` (sponsored share and markers) and the posts: which brands they have worked with, how often, and whether sponsored posts perform below their organic ones.
4. **Brand safety.** Search their transcripts for risk terms with `exact_match_search` and `usernames: ["handle"]`, `minLikes: 0`: one OR-group per risk (profanity, alcohol and drugs, gambling, politics, health claims, competitors). For a single word you can also use `creator_posts` with `query`. Read every hit in context before calling it a risk; quote it and link it.
5. **Location.** `creator_location`: `bioLocations` is the strongest signal; `mentions` are hints, and place names that are also ordinary words mislead.
6. **Other accounts.** `creator_profiles` and `creator_posts` list linked accounts; vet the other platform too if the campaign runs there.

## Report

Lead with a fit verdict (strong, conditional, or no) and the two or three reasons. Then: audience size and engagement against similar creators, what they talk about, sponsorship history, each brand-safety finding with its quote and link (or "none found" and what you searched for), and location. Say what Glystn could not check: audience demographics, private stories, deleted posts.

---
name: size-a-trend
description: Size a topic, product, phrase or behavior in what Instagram and TikTok creators say, and tell whether it is growing. Use for "how big is", "is X trending", "how many creators talk about", or before any deeper Glystn research.
---

# Size a trend

Answer "how big is this conversation, and where is it going" with numbers from Glystn's transcript index.

## Steps

1. **Write the keyword spec.** `must` items are all required; an item that is a list is an OR-group of up to 8 spellings, plurals and aliases of one idea. Matching is on whole words with no stemming, so list the forms people actually say: `[["matcha latte", "matcha lattes", "iced matcha"]]`.
   - Names that are also everyday words (Dove, Apple, Glow) collide. Add a context item (`[["dove"], ["soap", "body wash", "deodorant"]]`) or `mustNot` terms.
   - Leave `match` at `phrase`; use `all_words` only for loose descriptions, never for names or sayings.
2. **Size it** with `count_mentions`. Read `last12Months`, `monthly`, the per-platform split, `byCountry` and `byLikeFloor` (how much of it reaches 1,000+ likes).
3. **Check the matches are real.** Pull 20-30 posts with `exact_match_search` (`minLikes: 0`, `sort: "likes"`) and skim them. If many are off-topic, tighten the spec and size it again. Say which spec you settled on.
4. **Compare variants when the name is unsettled.** Use `compare_mentions` for 2-8 phrasings or competing terms in one call.
5. **Report**: monthly volume and the direction (compare the last 3 months with the 3 before), which platform leads, top creator countries, and 2-3 quotes from high-engagement posts, each linked.

## Reading the numbers

- Coverage is thin before November 2025: treat all-time totals as about the last year, and don't read growth into the earliest months.
- The current month is partial. Compare whole months, or scale the partial month by days elapsed and say so.
- Countries are the creator's country, not the audience's.
- `exact_match_search` returns only posts with 1,000+ likes unless you pass `minLikes`; its `totalMatches` still counts every post.
- Image and carousel posts carry a description of the visuals instead of speech, and some videos are sung lyrics. Quote only `textKind: "speech"` as something a creator said.

## Going further

- To see what the conversation is made of, run the `map-trends` skill on the same spec.
- To find who drives it, run `find_creators` with the topic.

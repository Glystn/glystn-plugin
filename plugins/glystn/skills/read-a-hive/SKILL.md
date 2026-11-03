---
name: read-a-hive
description: Answer questions about the user's Glystn hives (a brand, title or topic Glystn follows on Instagram and TikTok) - its numbers over any days or weeks, topics, how people feel and why, any slice of its labels and the posts behind it, ideas for what to dig into, and weekly reports. Use whenever the user names one of their hives or asks what's new in a hive.
---

# Read a hive

A hive is a subject Glystn follows for the user: every post about it is filed by topic and read for what it says, how the creator feels and why. Its numbers come from the hive tools, not from searching: a search sees a sample, the hive holds every post it filed. The hive tools are free.

## Steps

1. **Name the hive.** Call `list_hives` when the user hasn't named one or has several: it gives each hive's topics, start day, link and whether its dashboard is open to them. No hive tools, or an empty list, means this account has no hives: say so and stop.
2. **Numbers: `hive_dashboard`.** Any days (`from`, `to`, UTC), by day or by week. `posts.aboutIt` is the hive's volume; every count is of those posts.
   - **Say which period, every time.** "The past 7 days" means the last 7 days through today unless the user asks for calendar weeks: "the last 7 days (Oct 10-16, today so far)". A weekly report uses `by: "week"` over whole Monday-to-Sunday weeks: "the week of Oct 6-12". Compare equal spans cut the same way, and name both.
   - **The newest days are still filling in.** Today and yesterday undercount, and `posts.read` trailing `posts.inHive` means posts are still being read. Views keep growing after a post lands, so the newest posts' views run low. Say so, or end the comparison at yesterday and lean on post counts and shares.
3. **Any slice: `where`.** `hive_dashboard` and `hive_posts` take the same `where`: any combination of the labels the dashboard returns (topics, feeling, likedFor and dislikedFor, intent, kind for format, driver, who, paid, risk, `answers` to the hive's questions, mentions), plus creators, apps, minViews, and `not` to leave some out. One label's values are any of; labels together are all of. With topics, feeling and reasons are about those topics. `hive_dashboard` with a `where` gives that slice its own numbers; count with it, never by paging posts.
4. **The posts behind a number: `hive_posts`.** Same days and `where`; its `total` matches the dashboard. Up to 25 a page, most viewed or newest first, with `said`, feeling, reasons, transcript excerpts and top comments. Quote `said` or the transcript and link the post.
5. **Ideas, when the user opens broad.** Read the dashboard, then offer 3-5 combinations worth pulling, one line each with its count from a `where` call: a topic's dislike reason among people who tried it, ads against organic posts on one topic, one of the hive's questions crossed with feeling, breakouts (`minViews`) by format, posts that name a competitor. Lead with the ones whose shares break most from the hive as a whole and say why each matters; pull the posts for the one they pick.

## Weekly report

`hive_dashboard` by week over the last five full weeks, leaving out the week in progress. A table of each week's posts, views, creators and feeling, and each topic's posts by week, ready to chart (with a code sandbox, write it to a CSV too). Then what changed in the latest week against the four before, with the posts behind the biggest changes, quoted and linked.

## Report

Lead with the number and its window ("1,240 posts about it the week of Oct 6, up 18% on the week before"), then the evidence. A hive the user can't see, or a dashboard that isn't open to them, comes back as a refusal: relay it in plain words. End with the hive's link from `list_hives`, so the user can open its dashboard in Glystn.

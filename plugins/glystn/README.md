# Social Search by Glystn

Search what people actually say in TikTok and Instagram videos: the spoken words and captions, not just hashtags. Find content ideas from what is breaking out, check whether a trend is growing, pull real quotes, compare brands and find creators, for any topic. It also reads YouTube videos by link. Built for creators, founders and product teams, marketers and agencies, e-commerce sellers, analysts and journalists.

The plugin connects Claude to Glystn's MCP server (`https://app.glystn.com/api/mcp`, sign in with a Glystn account) and adds these skills:

| Skill | For | Say this |
|-------|-----|----------|
| `get-started` | Checks the connection, credits and hives, and points to the right skill | "What can Glystn do for me?" |
| `size-a-trend` | How big a topic is, whether it's Rising, Steady, Fading or a one-off spike, and whether an idea will land | "Is protein coffee growing on TikTok?" |
| `share-of-voice` | Competing brands side by side | "Compare share of voice for the top three running-shoe brands this year" |
| `explain-a-spike` | Why talk about a subject jumped: when, who set it off, what changed | "Why did mentions of our brand jump last week?" |
| `map-trends` | Trend boards and the weekly trend board | "What are the trends in at-home skincare right now?" |
| `break-down-a-post` | Why one video blew up against the creator's usual numbers, and what to reuse | "Why did this Reel blow up? <link>" |
| `consumer-verbatims` | What people say about a product or category, by theme, with exact linked quotes | "What do people say about our new sparkling water, in their own words?" |
| `find-creators` | A creator shortlist from a brief | "Find 30 US creators who talk about budget travel with kids" |
| `vet-a-list` | A list of creators scored against a brief, with the quote behind each score, kept in Glystn | "Score these 20 creators for a UK protein brand launch" |
| `vet-a-creator` | Due diligence and brand safety on one creator | "Is @handle brand safe for a family snack brand?" |
| `paid-creator-scan` | Who posts sponsored content for a brand or category | "Which creators does Acme pay, and how do those posts do?" |
| `campaign-recap` | Whether a campaign's creators said the key messages and disclosed it, with quotes | "Recap our October campaign: did the creators say our three key messages and disclose?" |
| `creator-content-strategy` | A content playbook from a niche's outliers, by account size | "What's working for fitness accounts under 10k followers?" |
| `write-content-scripts` | Ready-to-shoot scripts, hooks and captions modeled on a niche's outliers, in the account's voice | "Write five scripts I can film this week for my home-cooking account" |
| `analyze-youtube-videos` | YouTube videos by link: transcripts, views, top comments and paid placements, compared | "Compare these five YouTube reviews of robot vacuums: <links>" |
| `read-a-hive` | A hive (a standing watchlist Glystn keeps reading for a subject): its numbers, slices, posts and weekly report | "What changed in my hive this week?" |

The skills name tools by their MCP names (`count_mentions`, `find_creators_by_content`, ...), so they work whichever way the server is connected. Each call costs 1 Glystn credit (refunded if it fails), a trend board 10 and vetting 1 per creator; `get_credit_balance`, saving and reading lists, listing and reading trend boards (`get_trend_board` without a `trendId`) and the hive tools are free, and the longer skills estimate their cost and ask before a big run. In Claude's apps, results also draw as cards (posts with covers, mention charts, creator cards, vetting progress, credits); Claude Code shows text.

Install in Claude Code with `/plugin install glystn --marketplace Glystn/glystn-plugin` (on older versions, `/plugin marketplace add Glystn/glystn-plugin`, then `/plugin install glystn@glystn`). To try a local copy: `claude --plugin-dir <path to this folder>`.

## What it runs and sends

The plugin runs no code of its own. Its only connection is the Glystn MCP server above: the searches Claude makes go to Glystn, and Glystn returns posts, creators, counts and trends. Calls use the credits of the Glystn account you sign in with. See Glystn's [privacy policy](https://glystn.com/privacy-policy) and [terms](https://glystn.com/terms-of-service).

## License

The plugin's files are MIT licensed (`LICENSE`). Use of the Glystn service is covered by Glystn's terms.

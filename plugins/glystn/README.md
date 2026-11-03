# Glystn plugin

Connects Claude to Glystn's MCP server (`https://app.glystn.com/api/mcp`, sign in with a Glystn account) and adds skills for the research Glystn customers do most. Glystn searches what creators say in Instagram and TikTok videos, and reads YouTube videos by link:

| Skill | For |
|-------|-----|
| `size-a-trend` | How big a topic is and whether it is growing |
| `share-of-voice` | Competing brands side by side |
| `find-creators` | A creator shortlist from a brief |
| `vet-a-creator` | Due diligence on one creator |
| `paid-creator-scan` | Who posts sponsored content for a brand or category |
| `analyze-posts-at-scale` | Pulling ~1,000 posts and analyzing them with code |
| `map-trends` | Trend boards and the weekly trend board |
| `read-a-hive` | A hive's numbers, slices, posts and weekly report |
| `creator-content-strategy` | A content playbook from a niche's outliers, by account size |
| `write-content-scripts` | Ready-to-shoot scripts, hooks and captions modeled on a niche's outliers, in the account's voice |
| `consumer-verbatims` | What people say about a product or category, by theme, with exact linked quotes |
| `campaign-recap` | Whether a campaign's creators said the key messages and disclosed it, with quotes |
| `explain-a-spike` | Why talk about a subject jumped: when, who set it off, what changed |
| `analyze-youtube-videos` | YouTube videos by link: transcripts, views, top comments and paid placements, compared |

The skills name tools by their MCP names (`count_mentions`, `find_creators`, ...), so they work whichever way the server is connected.

Install in Claude Code with `/plugin install glystn --marketplace Glystn/glystn-plugin` (on older versions, `/plugin marketplace add Glystn/glystn-plugin`, then `/plugin install glystn@glystn`). To try a local copy: `claude --plugin-dir <path to this folder>`.

## What it runs and sends

The plugin runs no code of its own. Its only connection is the Glystn MCP server above: the searches Claude makes go to Glystn, and Glystn returns posts, creators, counts and trends. Calls use the credits of the Glystn account you sign in with. See Glystn's [privacy policy](https://glystn.com/privacy-policy) and [terms](https://glystn.com/terms-of-service).

## License

The plugin's files are MIT licensed (`LICENSE`). Use of the Glystn service is covered by Glystn's terms.

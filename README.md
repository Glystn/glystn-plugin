# Glystn for Claude

The Glystn plugin connects Claude to [Glystn](https://glystn.com), which searches what people actually say in Instagram and TikTok videos. It's for anyone who can use social data: founders and product teams, brands and agencies, creators, retailers, investors, journalists and researchers. It adds skills for the research they do most, starting with a get-started skill that checks your credits and points you to the right one: sizing trends and testing ideas, share of voice, breaking down why a post blew up, finding and vetting creators, paid creator scans, trend maps, hives, creator content strategy, content scripts, consumer verbatims, campaign recaps, spike explainers and YouTube video research.

The plugin is in [`plugins/glystn`](plugins/glystn); its [README](plugins/glystn/README.md) lists the skills and what the plugin connects to. You need a Glystn account to sign in.

## Install

In Claude Code:

```
/plugin marketplace add Glystn/glystn-plugin
/plugin install glystn@glystn
```

## ChatGPT and Codex

The same folder is also the ChatGPT plugin. Its listing (name, subtitle, description, category, starter prompts, review cases) is in [`plugins/glystn/.codex-plugin/plugin.json`](plugins/glystn/.codex-plugin/plugin.json). To submit or update it, zip the contents of `plugins/glystn` and upload the ZIP at [platform.openai.com/plugins](https://platform.openai.com/plugins). Listing text or skill changes need a new ZIP; changes to the Glystn server's tools are picked up on their own.

## License

MIT. See [LICENSE](LICENSE). Use of the Glystn service is covered by Glystn's [terms](https://glystn.com/terms-of-service).

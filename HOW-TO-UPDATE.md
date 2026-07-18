# How to update the dashboard (moved)

As of 2026-07-17 the dashboard lives at https://obsidianjuggernaut.github.io/ and updates itself through the webpage:

1. Open the site, tap "Post a new month".
2. Upload the month's Excel spreadsheet.
3. Enter the ministry code and tap "Post the list & get the link".

Any deacon with the code can do this. No JSON, no git, no terminal.

## Backup path (Worker down or no ministry code handy)

On Sedric's Mac, the `update-communion` skill (`~/.claude/skills/update-communion/`) publishes a month JSON directly to the `Obsidianjuggernaut/Obsidianjuggernaut.github.io` repo. Ask Claude: "update the communion dashboard with <file>".

The manual v1 steps this file used to describe (copy JSON into `lists/`, git add/commit/push) still work against the new repo — same `lists/` layout — but also update `lists/manifest.json` to include the new month id, or the newest-list fallback won't know about it.

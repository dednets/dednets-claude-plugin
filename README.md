# DedNets plugins for Claude Code

A Claude Code marketplace with one plugin, `dednets`: it brings the DedNets MCP
server and a skill, so Claude Code can enroll hosts, publish services at public
URLs and set up watchdogs against your DedNets Console.

```sh
# 1. tell Claude Code where your Console is and how to authenticate
export DEDNETS_CONSOLE=https://console.dednets.com   # omit if you use the hosted Console
export DEDNETS_TOKEN=...                             # Console > Settings > API tokens

# 2. install the plugin
claude plugin marketplace add dednets/dednets-claude-plugin
claude plugin install dednets@dednets
```

Restart Claude Code after changing either variable: plugin MCP servers start
once, at session start. `/mcp` then lists **dednets**.

Docs: <https://docs.dednets.com/automation/ai-agent/>

**Generated mirror, do not send pull requests here.** The source of truth is
`apps/claude-plugin/` in the DedNets monorepo; this repository is regenerated
by `scripts/sync-claude-plugin.sh` and hand edits are overwritten on the next
sync.

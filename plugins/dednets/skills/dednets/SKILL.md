---
name: dednets
description: Set up, repair and safely drive the DedNets MCP connection from Claude Code. TRIGGER when the user asks to enroll or add a DedNets host or machine, publish a service at a public URL, mint or scope a DedNets API token, point Claude at a self-hosted Console, or when the dednets MCP tools are missing, unauthorized, or failing to connect. Also trigger when a DedNets install or enroll command has to run on a machine other than this one. Do NOT trigger for unrelated networking, Docker, VPN or tunnel questions, and do not use it to explain what a host, app or watchdog is, because the MCP server already teaches that.
---

# Driving DedNets from Claude Code

The `dednets` MCP tools do the Console side, and the server itself teaches you
the object model (its initialize primer) and the order of operations (its
prompts). This file covers only what neither can reach from inside the Console:
the local binary, the environment that starts it, the token, and the machine at
the other end.

## The binary the server runs

This plugin starts the server through `bin/dednets-mcp`, which takes the first
hit of:

1. `$DEDNETSCTL`
2. `~/Applications/Haunted.app/Contents/MacOS/dednetsctl`
3. `/Applications/Haunted.app/Contents/MacOS/dednetsctl`
4. `dednetsctl` on `PATH`

If none exists the server exits with `cli_not_found`. The fix is to install the
CLI (<https://docs.dednets.com/automation/ai-agent/>) or the Haunted Terminal,
which bundles it, and then **restart Claude Code**: plugin MCP servers are
started once at session start, so nothing you change in the environment reaches
a running server.

## Which Console

Unset means the hosted `https://console.dednets.com`. A self-hosted Console
needs `DEDNETS_CONSOLE` exported in the shell that starts Claude Code, before it
starts. Changing it mid-session does nothing until a restart.

## Tokens

Ask the user for the least the task needs, and have them export `DEDNETS_TOKEN`
in the shell that starts Claude Code, before it starts.

| The user asked to | Scopes to tick |
| --- | --- |
| Look at hosts, apps or watchdogs | read |
| Add or remove a host | read, hosts:manage |
| Publish or unpublish a service or port | read, services:manage |
| Create, pause or fix a watchdog | read, watchdogs:manage |

The secret is shown exactly once. Never write it into a file in a repository,
never echo it back in a reply, and never put it into an MCP config you create.

## The machine at the other end

Before enrolling, settle how you will reach the machine being enrolled: an ssh
session you already have, a terminal the user drives, or this machine if that is
what the user meant. Say plainly which one you are using. The install command
carries a join token, so treat it as a credential: do not paste it into a file
or a commit, and if it leaks, enroll again for a fresh one rather than reusing
it.

## Canned workflows

The server publishes prompts for the common workflows. Prefer one of those over
inventing your own sequence.

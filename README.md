# builderOS

A protocol for coordinating human and AI work at company scale.

builderOS uses a structured local directory as the single source of truth for your projects, priorities, career, and tools. An AI agent operates within that directory, managing context, enforcing prioritization, syncing work to the cloud, and surfacing what matters.

## What it does

- **Protects deep work.** One session, one focus. The agent manages your queue and pushes back when you drift.
- **Eliminates meta-work.** Progress, meeting notes, and career evidence are captured as a byproduct of doing the work.
- **Breaks down silos.** Machine-readable project context makes visibility automatic, not performative.
- **Scales coordination.** At team and company scale, shared directories surface overlaps, dependencies, and institutional knowledge.

## Directory structure

```
<your-ldap>-os/
  context.md              # Seed: identity, scope, relationships, value function
  queue.md                # Scored and prioritized task list
  projects/
    <project-name>/
      project.md          # Purpose, links, decisions, status
      alignment/          # Meeting notes for this project
      ...                 # All artifacts: queries, docs, dashboards, designs
  career/
    progress/             # Weekly files tracking what you shipped
    feedback/             # Received feedback and performance reviews
    contributions.md      # Non-project evidence (mentorship, culture, etc.)
    alignment/            # Notes with manager and skip-level
  tools/
    mcps/                 # MCP server configs and integrations
```

## What's in this repo

- **`whitepaper.html`** - Full whitepaper describing the protocol, how it works, and what it enables.
- **`sample-os/`** - A complete sample directory showing what a builderOS workspace looks like in practice.

## How it works

1. Initialize your directory with a **context seed**: who you are, what you own, who you work with, what you're optimizing for.
2. Organize work into **project folders**. Every artifact (queries, docs, dashboards, designs, meeting notes) lives with its project.
3. Maintain a **queue** scored by urgency, importance, difficulty, and delegability. The agent manages it dynamically.
4. The agent runs a **heartbeat** on Slack and email, triaging inbound signals and protecting your focus.
5. Meetings are **ingested automatically** via transcription summaries, filed to the right project or career alignment folder.
6. At end of day, the agent compiles **progress** into weekly files. At end of week, your entire contribution record is current.
7. Your **career folder** builds your promotion case in real time: progress, feedback, contributions, manager alignment.

## Built with

- [Claude Code](https://docs.anthropic.com/en/docs/claude-code) as the TUI and agent runtime
- [Model Context Protocol (MCP)](https://modelcontextprotocol.io/) for tool integrations (Snowflake, Slack, Gmail, Google Calendar, Google Drive, Mode, Figma, and more)

## Status

This is a working implementation, not a concept. The protocol is running on a real job today.

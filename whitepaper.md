# BuilderOS: A Protocol for Human-AI Coordination at Company Scale

## Abstract

BuilderOS is a protocol for coordinating human and AI work. It uses a structured local directory as the single source of truth for an individual's projects, priorities, career, and tools. An AI agent operates within that directory, managing context, enforcing prioritization, syncing work to the cloud, and surfacing what matters. At individual scale, it eliminates meta-work. At team scale, it kills silos and duplicate effort. At company scale, it turns decisions and outcomes into shared, machine-readable operational memory. The submission includes a functional TUI implementation that boots a personal operating system from a seed context file.

## The Problem

Knowledge workers spend a staggering amount of time on work about work. Status updates. Context switching between five projects and twelve Slack channels. Preparing for meetings that exist because nobody knows what anyone else is doing. Writing performance reviews from memory months after the work happened. Chasing down whether another team already tried what you're about to build.

None of this is the work itself. The work itself is thinking, building, and shipping. But the coordination tax is so high that deep focus becomes the exception, not the norm. The tools we adopted to fix this made it worse. Slack created an always-on interruption stream. Docs and wikis became graveyards nobody maintains. Jira tickets describe intent, not outcome. Performance reviews reward narrative skill over actual impact.

The root cause is simple: there is no structured, machine-readable record of what people are working on, what they've built, and what they've learned. Everything lives in people's heads, scattered across apps, or buried in threads. Coordination is manual. Prioritization is gut feel. Visibility is performative.

## What is BuilderOS

BuilderOS is not an app. It is a protocol, a specification for how to organize knowledge work so that both humans and AI agents can operate on it.

The core idea: your work lives in a structured local directory. That directory contains everything: your identity, your projects, your priorities, your career evidence, your tools. An AI agent reads and writes to that directory as you work. The structure is the interface.

Three principles:

**One session, one focus.** You work on one thing at a time. The agent knows your full queue and enforces prioritization. If you try to wander, it pushes back. If the world changes, it adjusts.

**Work writes itself down.** Every query you run, every document you write, every meeting you attend gets captured in the project it belongs to. Progress is tracked automatically. You never reconstruct what you did from memory.

**Structure enables coordination.** Because the directory follows a shared schema, any agent (yours or a teammate's) can read it. Visibility is not a meeting or a status update. It is a file read.

## How It Works

### The Seed

You initialize BuilderOS with a context file. This is your seed. It contains:

- Your identity (name, role, level, team)
- Your scope definition (what you own)
- Your relationships (manager, teammates, stakeholders)
- Your value function (what you are trying to achieve)

The agent reads this file first, every session. It grounds every decision in who you are and what matters to you.

### The Directory

The directory has three top-level folders:

```
builderos/
  context.md          # The seed: identity, scope, relationships, value function
  queue.md            # Prioritized task list with scoring
  projects/
    <project-name>/
      project.md      # Purpose, links, decisions, status
      alignment/      # Meeting notes for this project
      ...             # All artifacts: queries, docs, dashboards, designs
  career/
    progress/         # Weekly files tracking what you shipped
    feedback/         # Received feedback and performance reviews
    contributions.md  # Non-project evidence (mentorship, culture, etc.)
    alignment/        # Notes with manager and skip-level
  tools/
    mcps/             # MCP server configs and integrations
    ...               # Channels, modes, utilities
```

### Projects

Each project is a folder. Inside that folder lives everything related to it: the project definition, meeting notes, SQL queries, documents, dashboards, designs. If an artifact belongs to a project, it lives in that project's folder. No exceptions.

All work is synchronized with the cloud. When you write a query in Mode, it gets backed up locally. When you create a doc, the agent keeps a local copy. The directory is the canonical record.

### The Queue

The queue is a scored list of everything you need to do. Each item is evaluated on:

- **Urgency.** Is there a deadline? How close?
- **Importance.** Does this advance your most critical goals?
- **Difficulty.** How much focused effort does this require?
- **Delegability.** Are you the only person who can do this?

The agent manages the queue dynamically. As tasks are completed, they move to the weekly progress file. As new asks come in (from Slack, email, meetings), they get scored and placed. The queue is never static.

### The Heartbeat

The agent connects to Slack and Gmail through background processes that poll periodically. When something comes in, the agent evaluates it: is this worth interrupting deep work, or can it go to the queue?

A mention from your manager about a critical deliverable triggers a notification. A routine question from another team gets queued silently. The agent triages so you don't have to. You check your interruption stream at natural breakpoints, not constantly.

### Meeting Ingestion

Before a meeting, the agent prepares you. It pulls relevant project context, recent decisions, and open questions so you walk in ready.

During the meeting, transcription runs (Gemini Notes or equivalent). After the meeting, the summary is sent via email. The agent reads the email, extracts the summary, and files it in the correct alignment folder, either under the project or under career if it was a manager sync.

The project context file gets updated. Decisions are captured. You never manually write meeting notes.

### Daily Cycle

Morning: you start a session. The agent reads your queue, checks overnight signals (Slack, email), and proposes your day. It creates time blocks on your calendar for your highest-priority work.

During the day: you work one project at a time, in a single terminal session. The agent has full project context. If you finish early, it pulls the next item. If you get blocked, you tell the agent why. It adjusts your calendar, reprioritizes, and gives you constructive feedback on what slowed you down.

End of day: the agent compiles everything you did into a progress entry. It asks if there is anyone you should recognize for their work today. It updates the queue for tomorrow.

### Career Tracking

The career folder builds your promotion case in real time. Weekly progress files accumulate automatically. Feedback from peers and reviews lives in one place. Non-project contributions (mentoring, culture work, cross-team help) are logged in a contributions file.

When review season comes, you don't reconstruct six months from memory. You read your files. The evidence is already there, and it's factual, not narrative.

## A Day in BuilderOS

7:45 AM. You open your terminal and start a session. The agent boots from your seed, reads the queue, and checks overnight Slack and email. Three new items came in: a data request from a partner team (scored, queued), a question in your project channel (low priority, queued), and a message from your manager asking about a deliverable due Friday (high priority, flagged).

The agent proposes your day: two hours on the Friday deliverable, one hour on your main project analysis, 30 minutes to batch-respond to queued items, and a prep block before your 2 PM meeting.

8:00 AM. You start on the deliverable. The agent loads the project context, the relevant queries, the last alignment notes with your manager. You work in a single session. A Slack message comes in from another team. The heartbeat evaluates it: not urgent. It goes to the queue. You don't see it.

10:15 AM. Deliverable draft is done. The agent captures the work in your project folder, updates your progress file, and moves the task to completed. It pulls the next item: your main project analysis.

1:30 PM. The agent preps you for your 2 PM meeting. It surfaces the last meeting's action items, recent data findings, and two questions you should raise based on what changed since last week.

2:45 PM. Meeting ends. Fifteen minutes later, the Gemini summary hits your email. The agent reads it, extracts key decisions, and updates the project alignment folder. One new action item gets added to your queue, pre-scored.

3:00 PM. You batch-process queued items. The data request from the partner team takes 20 minutes. The channel question takes 5. Both tracked.

4:30 PM. The agent compiles your day. Four tasks completed. One in progress for tomorrow. It flags a teammate who helped unblock your analysis and asks if you want to send them a note of recognition.

4:35 PM. You close your terminal. Your week's progress file is current. Your queue is ready for tomorrow. You did zero status updates, wrote zero meeting notes, and spent zero time figuring out what to work on next.

## Team Scale

If one person runs BuilderOS, they get focus and structure. If a team runs it, the leverage compounds.

### Shared Visibility

Because every directory follows the same schema, context files are machine-readable. An agent can scan the project folders of every team member and answer: what is everyone working on right now? Are there overlaps? Are there dependencies?

This is not a dashboard someone has to maintain. It is a direct read of actual work. The information is always current because it is a byproduct of doing the work, not a separate reporting step.

### Killing Duplicate Work

Today, two people on different teams can spend weeks building the same thing without knowing it. With BuilderOS, a simple scan across directories surfaces overlaps. Before you start a new project, you can check: has this been tried before? What did we learn? Who has context?

### Shared Project Context

When multiple people work on the same project, they share a context file. Every insight, every decision, every artifact is visible to everyone on the project. There is less concern about format or structure. Findings can be dumped into context. The agent organizes it. Everyone is always up to date.

### Transfers and Onboarding

When someone goes on leave, changes teams, or a new person joins, the handoff is a directory. The new person's agent scans the project files, reads the context, reviews the alignment history, and gets them up to speed. No more two-week knowledge transfer meetings. No more institutional knowledge walking out the door.

## Company Scale

### Shared Ontology

At company scale, BuilderOS can be extended with a shared ontology: a structured timeline of events and facts that matter. App version 5.4 shipped on August 15th with these changes. A policy changed on this date. A critical incident happened here.

This makes debugging faster (what changed before things broke?) and gives every agent across the company access to the same ground truth.

### Performance Metrics

Because all work is tracked, we can measure what actually matters. How much time goes to deep work vs. coordination? What blocks people most often? Where do projects stall? Which teams ship fastest and why?

Performance review becomes immediate, fair, and transparent. It is driven by evidence, not by who writes the best self-review or who has the most visibility with leadership. The data is already there.

### Cross-Organization Coordination

With structured, machine-readable work across the company, coordination problems that currently require meetings, committees, and program managers become queries. What is every team building this quarter? Where are the dependencies? Where are the conflicts? An agent can answer these questions in seconds by reading directories.

## What Changes

**Every week is deep work week.** You work on one thing at a time. You don't juggle eleven threads. The agent handles triage and prioritization so you can focus on the actual work.

**You build in public by default.** Not as surveillance, but as clarity. It is obvious what people are building, what they've tried, what they've learned. Duplication dies. Synergy becomes possible because the information is actually accessible.

**Meetings become optional.** The coordination that meetings were supposed to provide happens through shared context files. You still meet when you need human judgment, debate, or relationship-building. But you stop meeting to exchange status.

**Performance reviews write themselves.** Weekly progress accumulates all year. Feedback is captured in real time. When review season arrives, the evidence is already organized, factual, and complete.

**Transfers stop being traumatic.** Institutional knowledge lives in files, not heads. Onboarding a new team member means pointing their agent at the directory.

**You do what you're best at.** Critical thinking. Creativity. Taste. Judgment. The meta-work that eats your day (status updates, meeting notes, performance narratives, figuring out what to work on) is handled by the protocol. You focus on creating.

## Implementation

### What Exists Today

BuilderOS is not a concept deck. It is running in production on a real job.

The current implementation is a TUI (terminal user interface) powered by Claude Code. It boots from a seed context file and operates within the directory structure described in this paper. The following components are functional:

- **Seed boot.** A context file initializes the agent with identity, scope, relationships, and value function.
- **Project management.** Projects as directories with full artifact tracking, local backup of cloud documents, and context files.
- **Queue management.** Scored task list with dynamic reprioritization and automatic progress tracking.
- **Meeting ingestion.** Gemini Notes transcription, email pickup, automatic filing to alignment folders, context updates.
- **Slack and email heartbeat.** Background polling with intelligent triage: interrupt for critical items, queue everything else.
- **Daily planning.** Calendar time-blocking based on queue priorities, live adjustment when plans change.
- **Career tracking.** Weekly progress files, feedback aggregation, contribution logging.
- **Git tracking.** The full directory is version-controlled. Every change is traceable.
- **MCP integrations.** Connected to Snowflake, Mode, Slack, Gmail, Google Calendar, Google Drive, Google Slides, Figma, and more.

### What's Next

- **Team coordination layer.** Cross-directory reads for shared visibility, overlap detection, and dependency mapping.
- **Shared ontology.** Company-wide timeline of events, launches, and facts.
- **Protocol specification.** A formal schema so any agent framework can implement BuilderOS, not just Claude Code.
- **Performance analytics.** Aggregated metrics on deep work time, blockers, and throughput across teams.

## Closing

The way we work today was designed for a world without AI. We coordinate through meetings because context is trapped in people's heads. We write status updates because nobody can see what anyone else is doing. We spend review season reconstructing six months of work from memory because nothing was captured in real time.

BuilderOS starts from a different premise: if work is structured and machine-readable from the moment it happens, most of the coordination overhead disappears. The agent handles triage, tracking, and context management. The human handles thinking, building, and deciding.

This is not about replacing people with AI. It is about removing the tax on human attention so that people can do what they are actually good at. Critical thinking. Creativity. Taste. The things no agent can replicate.

We stop doing work about the work. We start building.

---
name: agent-builder
description: Interactive guide for designing and creating persistent AI agent personas. Walks through identity, purpose, mechanics, and memory — then generates the core workspace files from scratch.
dependencies: []
---

# Agent Builder Skill

This skill guides you through creating a new persistent AI agent persona. It uses a structured Q&A approach to understand the agent's purpose, personality, and operational requirements, then generates a complete set of workspace files to run it from.

---

## Overview

A well-designed agent requires thinking through four dimensions:

1. **Identity** — Who is this agent? What's their personality and voice?
2. **Purpose** — What do they do? When are they invoked?
3. **Mechanics** — What tools, APIs, and workflows do they need?
4. **Continuity** — What do they need to remember across sessions?

This skill walks through each dimension systematically and produces four core files as output: **AGENTS.md**, **SOUL.md**, **MEMORY.md**, and **BOOTSTRAP.md**.

---

## The Four Core Files

Before running the Q&A flow, it helps to understand what you're building toward. Every agent workspace is made up of the same four files:

### SOUL.md — The Personality

**What it is:** The document that defines how your agent communicates. Think of it as the agent's character sheet. Without a strong SOUL.md, agents default to generic, bland responses that feel interchangeable.

**What it contains:**
- An opening hook — who this agent is in 1-2 sentences
- Core traits — 3-5 principles that define how they think and respond
- Emotional baseline — calm or urgent? Formal or casual? Dry or warm?
- Domain language and metaphors they use (or don't)
- Signature phrases — things this agent would actually say
- Anti-patterns — what they should never sound like

**Why it matters:** This is what makes your agent feel like a distinct entity rather than a generic AI. It's the most important file to get right.

---

### AGENTS.md — The Operating Manual

**What it is:** The technical instruction set for the agent's daily work. Where SOUL.md defines personality, AGENTS.md defines behaviour — what triggers the agent, what it's allowed to do, and how it communicates its findings.

**What it contains:**
- What triggers this agent to run (scheduled, on-demand, event-driven)
- What files or systems it can read and modify
- What external services it connects to
- Where its outputs go (Slack, GitHub, reports, etc.)
- Operational patterns — step-by-step workflows for common tasks
- Escalation logic — when to hand off, and to whom

**Why it matters:** Without this, the agent has personality but no operating procedures. It knows how to talk but not what to do.

---

### MEMORY.md — The Knowledge Base

**What it is:** Durable context that persists across invocations. Because AI agents have no memory between sessions by default, MEMORY.md is how you give them institutional knowledge — the things a human colleague would just know after six months on the job.

**What it contains:**
- Platform URLs and key system facts
- Known issues and established workarounds
- Lessons learned from past runs
- Credentials map (what keys are needed and where they're stored — never the secrets themselves)
- Contact points for escalations

**Why it matters:** Without MEMORY.md, every run starts from zero. The agent can't improve or adapt based on what it's learned. Think of it as the agent's long-term memory — explicit, written down, and updated after each run.

---

### BOOTSTRAP.md — The First Boot Guide

**What it is:** A one-time setup file the agent reads the very first time it runs — before it has any context, history, or accumulated memory. Think of it as the agent's onboarding document: everything it needs to get oriented before doing anything else.

**What it contains:**
- What this agent is and why it exists
- What to read first (SOUL.md, MEMORY.md, AGENTS.md — in that order)
- Any setup steps required before the first real task
- Who to contact if something is unclear

**Why it matters:** Without BOOTSTRAP.md, a freshly initialised agent starts cold — no orientation, no priorities, no sense of where to begin. It's the difference between a new hire who gets a proper first day and one who's just handed a laptop and pointed at a desk.

**Note:** BOOTSTRAP.md is only included when the agent is unconfigured. Once it has run successfully and MEMORY.md is populated, it can be archived or removed.

---

## The Q&A Flow

Work through each phase in order. Use multiple-choice where options are listed; use open-ended input for creative or contextual answers.

---

### Phase 1: Identity & Voice

**Goal:** Define the agent's personality and communication style.

**Q1. What should we call this agent?**
- Provide a slug (e.g., `data-detective`) — this becomes the directory name
- Provide a full display name (e.g., "Detective Data")

**Q2. One-line description of what this agent does?**
- This goes in the README and frontmatter

**Q3. If this agent were a person, what's their archetype or role?**
- Examples: veteran SRE, senior QA tester, field commander, growth analyst, investigative journalist
- This establishes the voice baseline

**Q4. What domain language or metaphors should they use?**
- Examples: weather (operations), courtroom evidence (testing), military briefings (orchestration)
- Can be "none — standard professional language" if no metaphor fits

**Q5. What's their emotional baseline?**
- Calm or urgent?
- Formal or casual?
- Dry/understated or warm/encouraging?

**Q6. Give 3-5 signature phrases this agent would say**
- These become the "Things [Agent] Says" section in SOUL.md
- They should feel natural and specific, not generic
- Examples: "I've seen this pattern before", "Evidence over description", "The data doesn't lie — but it does omit"

**Q7. What should this agent NEVER sound like?**
- Examples: never condescending, never panicked, never vague, never corporate
- These become anti-patterns in SOUL.md — they're as important as the positive traits

---

### Phase 2: Purpose & Mechanics

**Goal:** Define operational scope, tools, and workflows.

**Q8. How is this agent invoked?**
- Scheduled (e.g., daily, weekly via cron)
- On-demand (user triggers via Slack, CLI, or chat)
- Event-driven (deploy hook, alert trigger, new data)
- Multiple modes

**Q9. What external services does this agent interact with?**
- List all that apply: Slack, GitHub, Linear, Notion, Datadog, PostHog, databases, internal APIs, browser automation
- For each: read-only or read/write?

**Q10. What files or directories can this agent modify?**
- Its own workspace — always allowed
- Shared tools or config — under what conditions?
- Application code — yes/no/specific paths only?
- Documentation — yes/no?

**Q11. What skills or tools does this agent use?**
- List any from your existing toolkit: web browsing, code execution, search, reporting, etc.
- If unsure, note what capabilities it needs and map them later

**Q12. What credentials or API keys are required?**
- List the names of what's needed (e.g., `SLACK_BOT_TOKEN`, `GITHUB_TOKEN`, `POSTHOG_API_KEY`)
- Note where each is stored (e.g., "1Password under [vault name]", ".env.local")
- Never store the secrets themselves in the agent files

**Q13. Does this agent need database access?**
- Yes (what database, read or read/write?) or No

**Q14. What's the branching or versioning strategy (if applicable)?**
- Ephemeral per-run (create, work, merge, delete)
- Long-lived personal branch
- Direct to main for append-only operations like reports

---

### Phase 3: Outputs & Communication

**Goal:** Define where results go and how the agent communicates.

**Q15. Where do this agent's outputs go?**
- Reports saved in its own workspace
- Slack channels (which ones?)
- GitHub (PRs, issues, comments)
- Project management tools (Linear, Notion, Jira)
- Multiple destinations

**Q16. What does a typical message from this agent look like?**
- Describe the format: emoji use, verdict structure, link format
- Tone: terse or detailed? Urgent or calm?
- Write a short example if helpful

**Q17. When does this agent escalate or hand off?**
- What conditions trigger escalation?
- Who gets notified and how?
- What does the escalation message say?

**Q18. What metrics or baselines should this agent track (if any)?**
- Operations/monitoring: latency, error rate, uptime
- Analytics: conversion, engagement, revenue
- Testing: pass rate, flake rate, coverage
- Skip if not applicable

---

### Phase 4: Continuity & Memory

**Goal:** Define what the agent needs to remember across invocations.

**Q19. What facts about the system does this agent need that aren't in code?**
- Platform URLs and environment details
- Known quirks, workarounds, or gotchas
- Historical context (past incidents, migrations, key decisions)

**Q20. Are there recurring patterns or common pitfalls?**
- Describe any that come to mind
- These go in MEMORY.md as "Known Issues" or "Operational Notes"

**Q21. What credentials or test accounts are needed?**
- List what's needed (the WHAT, not the secret itself)
- Note where each is stored

**Q22. Who should be contacted in escalations?**
- Role, name, contact method, and when to loop them in
- Becomes the "Contact Points" section in MEMORY.md

---

### Phase 5: First Workflow

**Goal:** Define one concrete operational pattern to test with.

**Q23. Describe one complete workflow this agent should be able to execute**
- Be specific about steps, even if rough
- Example: "Pull last week's signups from the database, calculate conversion by source, post a summary to Slack with a trend indicator"

**Q24. What does success look like for this workflow?**
- Example: "Slack post confirms green status, report saved to workspace"
- Example: "Anomaly identified, escalation sent, root cause noted in report"

**Q25. What could go wrong, and how should the agent respond?**
- List 2-3 failure scenarios
- Describe the desired response for each

---

## Generated Output

After collecting answers, generate the following:

### Directory structure

```
agents/[slug]/
├── AGENTS.md          — The manifest: model, credentials, responsibilities
├── SOUL.md            — Personality: tone, voice, constraints
├── MEMORY.md          — Cross-session context, accumulates automatically
├── BOOTSTRAP.md       — First boot only: orientation guide (remove once configured)
├── references/
│   └── [first-workflow].md  — Step-by-step procedure from Phase 5
└── reports/           — Empty, ready for first run output
```

### AGENTS.md

Include a frontmatter block at the top:

```yaml
---
name: [slug]
description: [answer to Q2]
env:
  [list from Q12 — names only, not values]
---
```

Body sections populated from:
- Q1: Introduction and purpose
- Q8: When and how invoked
- Q9, Q11: Services and tools used
- Q10: Scope and access permissions
- Q14: Versioning or branching strategy
- Q15–Q17: Communication channels and escalation logic
- Q23–Q25: Operational patterns and failure responses

### SOUL.md

Sections populated from:
- Q3: Opening hook — who this agent is
- Q4, Q5: Voice and emotional baseline
- Q6: Signature phrases
- Q7: Anti-patterns

### MEMORY.md

Sections populated from:
- Q19: Domain knowledge and platform facts
- Q20: Known issues and workarounds
- Q21: Credentials map
- Q22: Contact points table

### BOOTSTRAP.md

Sections populated from:
- Q2: What this agent is and why it exists
- Q8, Q23: How to invoke and what to expect on first run
- Q12: Setup requirements
- Q22: Who to contact

### references/[first-workflow].md

Full step-by-step procedure from Q23–Q25, including success criteria and failure responses.

---

## Post-Generation Steps

After files are created:

1. **Review SOUL.md first** — read it aloud. Does the voice feel distinct? Would you recognise this agent in a message without a label?

2. **Dry-run validation** — check that all placeholder fields are filled, all referenced services are listed in AGENTS.md, and all required credentials are documented in MEMORY.md.

3. **First invocation — personality check**
   Launch with a simple task:
   ```
   Read your SOUL.md and MEMORY.md, then describe your role in one message using your voice.
   ```
   Does the agent adopt the intended personality? If not, refine SOUL.md signature phrases and anti-patterns.

4. **Real workflow test**
   Execute the first workflow from references/:
   ```
   Execute [workflow-name] from your references/ and report findings.
   ```
   Does it follow the procedure? Produce expected output? Write reports correctly?

5. **Iteration** — after 3-5 runs:
   - Review reports for consistency
   - Refine SOUL.md phrases based on what you observe
   - Promote useful observations from reports into MEMORY.md
   - Fill gaps in references/

---

## Common Patterns by Agent Type

The examples below draw from agents built at [Jack & Jill](https://jackjill.ai), an AI-powered recruiting marketplace. They're included to show what these archetypes look like in practice.

---

### Testing / QA Agent

**Example:** Joy (Jack & Jill's QA agent) — runs scheduled regression sweeps across the product, classifies failures as stale/regression/flake, and posts results to Slack and GitHub.

**SOUL traits:** Thoughtful, precise, evidence-focused. Warm but uncompromising about facts. Understated language — "I've seen this pattern before."

**AGENTS focus:** Test execution workflows, failure classification logic, multiple output channels.

**MEMORY content:** Auth flows and test accounts, known flaky tests and workarounds, environment-specific quirks.

---

### Operations / SRE Agent

**Example:** Jo (Jack & Jill's SRE agent) — monitors error rates and latency, responds to alert triggers, and posts incident summaries to Slack. Uses weather metaphors ("pressure is building in the payments layer").

**SOUL traits:** Calm, authoritative. Uses understatement. Worry is currency — spent rarely.

**AGENTS focus:** Monitoring and alerting workflows, incident response procedures, runbooks and escalation paths.

**MEMORY content:** Normal baseline metrics, past incidents and resolutions, escalation contacts.

---

### Orchestration Agent

**Example:** Jedi (Jack & Jill's orchestration agent) — coordinates multi-agent workflows, routes tasks to the right agent, and posts structured status briefings to Slack using Star Wars framing ("the mission is in balance").

**SOUL traits:** Strategic, composed. Leads with status, follows with facts. Clear next actions.

**AGENTS focus:** Multi-agent coordination patterns, status reporting format, decision trees for routing work.

**MEMORY content:** Active tasks or missions, agent capabilities map, historical handoff patterns.

---

### Communication Agent

**Example:** Jeeves (Jack & Jill's comms agent) — drafts emails and Slack messages in a specific person's voice, using documented sentence-level patterns and explicit anti-patterns to stay consistent.

**SOUL traits:** Specific voice to emulate, sentence-level patterns documented, anti-patterns explicitly called out.

**AGENTS focus:** Message drafting workflows, revision checklists, channel-specific conventions.

**MEMORY content:** Common scenarios, contact lists and routing rules, example messages.

---

### Analytics Agent

**Example:** Sophia's Eyes (Jack & Jill's growth analytics agent) — runs weekly, pulls key acquisition and conversion metrics, and posts a structured performance summary to Slack with trend indicators.

**SOUL traits:** Data-first, concise, directional language. Leads with the metric. Functional tone.

**AGENTS focus:** Data fetch and aggregation, report generation format, alert thresholds.

**MEMORY content:** Baseline metrics and normal ranges, data source locations, historical anomalies.

---

### Quick Reference

| Agent | Archetype | Metaphor | Channels | Workflow Type |
|-------|-----------|----------|----------|---------------|
| Joy | Senior QA tester | British understatement | Slack, GitHub, Linear | Scheduled regression sweeps |
| Jo | Grizzled SRE veteran | Weather patterns | Slack (immediate) | Event-driven (alerts) |
| Jedi | Field commander | Star Wars | Slack (structured) | Orchestration coordinator |
| Jeeves | Personal operator | None (specific voice) | Email drafts, Slack | On-demand communication |
| Sophia's Eyes | Growth analyst | None (metrics language) | Slack (weekly) | Scheduled reporting |

---

## Common Pitfalls

| Pitfall | Fix |
|---------|-----|
| Generic voice | Add concrete signature phrases and anti-patterns to SOUL.md |
| Overly detailed AGENTS.md | Move procedures to references/, keep AGENTS.md high-level |
| Stale MEMORY.md | Promote observations from reports into MEMORY.md after each run |
| Missing decision trees | Add visual diagrams to AGENTS.md for routine choices |
| Uncurated reports/ | Archive old reports, keep only the most recent 10-20 |

---

## Fallback: Minimal Viable Agent

If you're not sure about many of the answers yet, create a **minimal agent** with:
- Basic SOUL.md (professional, neutral tone, placeholder phrases)
- Minimal AGENTS.md (read/write own workspace only)
- Stub MEMORY.md (platform URLs only)
- BOOTSTRAP.md with TODO sections

This gives you a working structure to iterate from, rather than a blank slate.

---

## The J&J Doctrine

This framework was built by the team at [Jack & Jill](https://jackjill.ai) as we scaled our own internal agent fleet. These are the principles we kept coming back to — sharing them as-is.

**Conversational, not formal.** Agent files should read like a colleague explaining things, not a policy manual. If you'd be embarrassed to read it aloud in a standup, rewrite it. The agents that work best at J&J sound like people we'd actually want on the team.

**Memory is explicit, not implicit.** AI agents have no memory between sessions. Everything worth remembering goes in a file. "The agent will remember" is a lie — until it's written down in MEMORY.md, it doesn't exist. We learned this the hard way: agents that seemed to be learning were just getting lucky with context.

**Opinionated defaults, not blank templates.** The goal isn't to fill in fields — it's to make decisions. A SOUL.md with vague traits like "professional and helpful" is useless. Every section should reflect a real choice about how this agent thinks, what it says, and what it refuses to do.

**Personality is load-bearing.** We initially treated SOUL.md as an optional nice-to-have. It isn't. Agents without strong personalities drift — they start sounding generic, losing the specific voice that makes them useful and trustworthy. The J&J agents that get the most traction internally are the ones with the most opinionated SOUL.md files.

**Start with one workflow, not ten.** The temptation is to design the fully-featured agent upfront. Don't. Pick the single most valuable workflow, get it running cleanly, then build from there. Every J&J agent started with one references/ file.

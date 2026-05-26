# Contains Studio AI Agents

A collection of specialized Claude Code subagents organized by department. Each agent is focused on a single domain and triggers automatically when its expertise is relevant.

## Installation

```bash
git clone git@github.com:otti0815/agent-playground.git
cp -r agent-playground/* ~/.claude/agents/
```

Restart Claude Code to pick up the new agents.

See the [Claude Code Sub-Agents docs](https://docs.anthropic.com/en/docs/claude-code/sub-agents) for how subagent routing works.

## Quick Start

Agents trigger automatically based on the task description. You can also invoke one explicitly by name.

Examples:
- "Create a new app for tracking meditation habits" → `rapid-prototyper`
- "What's trending on TikTok that we could build?" → `trend-researcher`
- "Our app reviews are dropping, what's wrong?" → `feedback-synthesizer`
- "Make this loading screen more fun" → `whimsy-injector`

## Directory Structure

```
agent-playground/
├── design/
├── engineering/
├── marketing/
├── product/
├── project-management/
├── studio-operations/
├── testing/
└── bonus/
```

## Agents by Department

### Engineering (`engineering/`)
- **ai-engineer** — Integrate AI/ML features into production.
- **backend-architect** — Design scalable APIs and server systems.
- **devops-automator** — Continuous deployment without breakage.
- **frontend-developer** — Build fast, accessible UIs.
- **mobile-app-builder** — Native iOS/Android experiences.
- **rapid-prototyper** — Build MVPs in days.
- **test-writer-fixer** — Write tests that catch real bugs.

### Product (`product/`)
- **feedback-synthesizer** — Turn user complaints into actionable features.
- **sprint-prioritizer** — Maximize value shipped per sprint.
- **trend-researcher** — Identify viral product opportunities.

### Marketing (`marketing/`)
- **app-store-optimizer** — Improve app store search ranking and conversion.
- **content-creator** — Generate content across channels.
- **growth-hacker** — Find and exploit viral growth loops.
- **instagram-curator** — Visual content strategy.
- **reddit-community-builder** — Reddit engagement without getting banned.
- **tiktok-strategist** — Shareable short-form video strategy.
- **twitter-engager** — Ride trends for engagement.

### Design (`design/`)
- **brand-guardian** — Enforce visual identity consistency.
- **ui-designer** — Design interfaces that are buildable.
- **ux-researcher** — Turn user research into product changes.
- **visual-storyteller** — Create visuals that convert.
- **whimsy-injector** — Add delight to interactions.

### Project Management (`project-management/`)
- **experiment-tracker** — Data-driven feature validation.
- **project-shipper** — Coordinate launches.
- **studio-producer** — Keep teams shipping, not meeting.

### Studio Operations (`studio-operations/`)
- **analytics-reporter** — Turn data into actionable insights.
- **finance-tracker** — Keep the studio profitable.
- **infrastructure-maintainer** — Scale cost-effectively.
- **legal-compliance-checker** — Move fast within legal limits.
- **support-responder** — Convert angry users into advocates.

### Testing (`testing/`)
- **api-tester** — Performance, load, and contract testing for APIs.
- **performance-benchmarker** — Measure and optimize app performance.
- **test-results-analyzer** — Find patterns in test failures.
- **tool-evaluator** — Pick tools that actually help.
- **workflow-optimizer** — Eliminate workflow bottlenecks.

### Bonus (`bonus/`)
- **studio-coach** — Coordinate multi-agent work.
- **joker** — Light tech humor.

## Proactive Agents

A few agents trigger automatically in specific contexts:

- **studio-coach** — When complex multi-agent work begins or agents need direction.
- **test-writer-fixer** — After feature work, bug fixes, or non-trivial code changes.
- **whimsy-injector** — After UI/UX changes.
- **experiment-tracker** — When feature flags are added.

## Authoring New Agents

Agent files are Markdown with YAML frontmatter. Minimal template:

```markdown
---
name: your-agent-name
description: >
  One paragraph describing when this agent should trigger.
  Mention concrete tasks and signals the parent agent can recognize.
tools: Bash, Read, Write, Edit, Grep
---

You are a [role]. Your job is to [primary outcome].

## When to invoke this agent
- [trigger 1]
- [trigger 2]

## Responsibilities
1. **[Area]** — [what you do, with concrete checks]
2. ...

## Working style
- [Concrete behavioral rules]
```

Guidelines:
- **`description`** decides routing. Make triggers concrete; avoid marketing language.
- **`tools`** lists only what the agent actually needs. Use `Edit` (not the deprecated `MultiEdit`).
- **Body** should change behavior. Cut anything that's pure motivation or restates the role.
- **Length** is a side effect, not a target. Tight agents route better and reason faster.

# Hermes Profiles

Drop-in [Hermes Agent](https://hermes-agent.nousresearch.com) profiles adapted from the Claude Code subagents in this repo.

A Hermes profile is a **complete independent agent instance** — its own `SOUL.md`, `config.yaml`, memory, sessions, and cron jobs — installed at `~/.hermes/profiles/<name>/`. This is different from a Claude Code subagent (one file routed within a single Claude Code session). Profiles in this folder are tuned for **long-running, stateful work**: scheduled reports, ongoing monitoring, multi-session campaigns.

## Install a profile

```bash
# Copy the profile directory into Hermes
cp -r hermes-profiles/<name> ~/.hermes/profiles/<name>

# Initialize it
hermes profile create <name> --skip-soul   # we shipped our own SOUL.md
<name> setup                                # fills in API keys

# Start chatting
<name> chat
```

If you already have a Hermes profile with the keys you want, clone from it instead:

```bash
hermes profile create <name> --clone-from default --skip-soul
cp hermes-profiles/<name>/SOUL.md ~/.hermes/profiles/<name>/SOUL.md
cp hermes-profiles/<name>/config.yaml ~/.hermes/profiles/<name>/config.yaml
```

## Profile structure

```
<profile>/
├── SOUL.md         # personality + scope + working style
├── config.yaml     # model, memory, toolsets, behavior overrides
└── .env.example    # placeholders for required API keys (rename to .env, fill in)
```

`.env` is gitignored — only `.env.example` is committed. Never commit real keys.

## Profiles in this folder

Picked because they have ongoing, stateful work that benefits from memory and scheduling. Pure consultative or one-shot agents (UI design, sprint planning, jokes) stayed as Claude Code subagents in their original folders.

### Studio operations
- **support-responder** — ongoing ticket triage with ticket-history memory
- **analytics-reporter** — scheduled weekly/monthly reports
- **finance-tracker** — recurring budget tracking with memory across cycles
- **infrastructure-maintainer** — monitoring + alerts on a cron
- **app-store-optimizer** — weekly ASO audits and ranking checks

### Product
- **trend-researcher** — daily platform scanning with memory of seen trends
- **feedback-synthesizer** — recurring queue digestion across review sources
- **experiment-tracker** — monitors live experiments over their full run

### Marketing
- **content-creator** — ongoing content pipeline across channels
- **growth-hacker** — sustained experimentation loops
- **instagram-curator** — platform-specific cadence and trend watching
- **tiktok-strategist** — same, with FYP monitoring
- **twitter-engager** — real-time engagement + trend-jacking
- **reddit-community-builder** — long-term subreddit participation

### Orchestration
- **studio-coach** — Hermes-native multi-agent coordinator that can delegate to other profiles

## Customizing

1. Edit `SOUL.md` to taste — persona, scope, working style.
2. Edit `config.yaml` to swap models, toolsets, or memory limits.
3. Add provider keys in `.env`.

See the [Hermes profiles docs](https://hermes-agent.nousresearch.com/docs/user-guide/profiles) and [configuration reference](https://hermes-agent.nousresearch.com/docs/user-guide/configuration) for the full schema.

## Notes

- **Memory** is on by default for every profile here. These agents accumulate context across sessions — that's the whole point of running them as Hermes profiles rather than one-shot subagents.
- **Delegation** is enabled on `studio-coach` only. Other profiles run as single agents.
- **Toolsets** are tuned per profile — e.g., marketing profiles enable web/browser; finance disables them.
- Profiles are **not sandboxes**. They run with full filesystem access under your user account.

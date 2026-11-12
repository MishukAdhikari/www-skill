# www — What, Where, Why

An agent skill (Claude Code, Codex, and other `SKILL.md`-compatible agents) that gives the full picture of a code path, PR, feature idea, or technology in three grounded passes:

1. **WHAT** — what it is and its quality, security, performance and architecture state
2. **WHERE** — where it lives, its blast radius, scope, and options
3. **WHY + FUTURE** — why it matters, the impact over time, and a decisive verdict

## Install

```bash
# Claude Code (personal)
git clone https://github.com/MishukAdhikari/www-skill /tmp/www-skill
mkdir -p ~/.claude/skills && cp -r /tmp/www-skill/skills/www ~/.claude/skills/

# Or with the skills CLI
npx skills add MishukAdhikari/www-skill
```

## Use

```
/www app/Services/Billing --depth deep
/www PR #123
/www should we adopt Redis streams for our queue?
```

## Prompt caching

The skill is written to be cache-friendly, so the first run pays the load cost once and later runs reuse it:

- `SKILL.md` is fully static: no dates, versions, or per-run text. Its bytes are identical every time, so providers that cache prompt prefixes (Anthropic prompt caching, OpenAI automatic caching) can reuse it.
- Your target and flags arrive after the skill text, at the end of the prompt, so they never break the cached prefix.
- Heavy guidance lives in `references/deep-mode.md` and loads only for `--depth deep`, keeping the always-loaded part small.

When you edit the skill, keep that rule: put stable instructions first and never add timestamps or run-specific text to `SKILL.md`.

## License

MIT

---
name: www
description: "What / Where / Why: analyze a subject (code, feature, PR, idea, or technology), map where it lives and what it touches, then give a grounded verdict on why it matters and its future impact. Use when asked for 'www', 'what where why', a full picture of a change, or impact analysis before deciding."
argument-hint: "[target: path, PR, feature idea, or technology] [--depth quick|deep]"
---

# WWW — What, Where, Why

Three passes, always in this order. Each pass feeds the next; never skip ahead.

| Pass | Question | Borrowed from |
|---|---|---|
| 1. WHAT | What is it, and what state is it in? | analyze (quality, security, performance, architecture) |
| 2. WHERE | Where does it live, what does it touch, where could it go? | brainstorm (scope, boundaries, options) |
| 3. WHY + FUTURE | Why does it matter, and what happens if we do / don't? | point-of-view (grounded, decisive verdict) |

## Rules that hold for every pass

- **Ground every claim.** Cite `file:line`, a command's output, a PR, or a doc. A claim the conversation makes is a pointer to check, not evidence.
- **Read-only.** This skill never edits code. It ends with a recommendation; changes need the user's go-ahead.
- **No interview up front.** Work out the target from the request and the repo. Ask one question only if a missing fact would change the verdict and cannot be found.
- **Size to the subject.** `--depth quick` (default for a file or small PR): a few bullets per pass. `--depth deep`: read `references/deep-mode.md` first.

## Pass 1 — WHAT

1. Identify the target type: code path, PR/diff, feature idea, or external technology.
2. Discover: list the files, entry points, and dependencies involved (Glob/Grep/Read, `gh pr diff` for a PR).
3. Assess across four domains, only where relevant: **quality** (smells, tests), **security** (input, auth, secrets), **performance** (queries, loops, I/O), **architecture** (coupling, layering).
4. Output: a one-line definition, then findings ranked by severity (critical / high / medium / low), each with evidence.

## Pass 2 — WHERE

1. **Blast radius:** callers, routes, jobs, UIs, APIs, data, and users that this touches. Show the chain, not just the file.
2. **Boundaries:** what is in scope and explicitly out of scope.
3. **Options:** 2–3 directions it could go (keep, change, replace), each with its cost in one line. Skip when the subject is not a decision.

## Pass 3 — WHY + FUTURE IMPACT

1. **Why it exists / why it matters:** the problem it solves, from evidence (commit messages, issues, docs), not guesses.
2. **Future impact:** for the recommended option and for doing nothing, state the effect at roughly 1 month, 6 months and 1+ year: maintenance cost, risk, scale, team load, lock-in.
3. **Verdict:** one decisive recommendation with a confidence level (high / medium / low) and the condition that would flip it. If evidence is too thin, say **Blocked — missing context** and name what would resolve it.

## Output shape

```
## WHAT  — <one-line definition>
<severity-ranked findings with evidence>

## WHERE — <blast radius summary>
<touch map> · <scope in/out> · <options>

## WHY   — <verdict in one sentence> (confidence: X)
<why it matters> · <impact table: now / 6 mo / 1 yr+, do vs don't> · <what would flip it>
```

Keep it short. A reader should get the decision from the three headings alone.

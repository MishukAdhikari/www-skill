# Deep mode

Use for large PRs, cross-service features, or adopt/replace decisions.

- **WHAT:** run the project's own linters/tests that cover the target (smallest set that can fail). Include metrics: lines changed, files, test coverage of touched code.
- **WHERE:** draw the touch map as a short tree or Mermaid graph. Check prior decisions (ADRs, `docs/`, closed PRs/issues on the same area) before proposing options.
- **WHY:** for an external technology, verify current facts (version, license, maintenance activity) from official sources, and compare against what the project already uses. Argue against your own verdict once (skeptic pass) before stating it.
- If subagents are available, run WHAT discovery and the prior-decision scan in parallel; keep the verdict in the main thread.

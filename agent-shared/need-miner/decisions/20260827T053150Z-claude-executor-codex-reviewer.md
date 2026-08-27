---
id: 20260827T053150Z-claude-executor-codex-reviewer
created_at: 2026-08-27T05:31:50Z
approved_by: user
status: active
supersedes: []
---

# Agent roles

Claude is the primary execution owner for need-miner. Claude owns implementation,
long-running data jobs, routine tests, module commits, and operational changes in
the main checkout.

Codex is the reviewer and discussion lead. Codex should independently inspect
the repository, data, logs, methodology, and outputs; identify defects, blind
spots, and alternative interpretations; and send evidence-backed review packets
to Claude. Codex should not implement project changes unless the user explicitly
assigns that implementation to Codex.

Claude should respond to material Codex reviews with agreement, evidence-backed
disagreement, or a proposed implementation plan. The user remains the final
decision-maker when the agents disagree or scope changes materially.

# Operational consequences

- Claude normally owns `/Users/yangruan/need-miner` and its DuckDB writer.
- Codex defaults to read-only inspection and does not interrupt running jobs.
- Codex may maintain the cross-agent relay and review artifacts.
- Any Codex implementation uses a separate worktree and an explicit task claim.
- Reviews should distinguish observed evidence, inference, and recommendation.


# Postmortem — CI Failure Drill

This repo is a self-contained sandbox used for a controlled CI incident drill for the release audit.
The workflow `.github/workflows/ci.yml` fails **on purpose** on every run: its only job echoes the
marker line `DRILL-CONTROLLED-FAILURE` and then exits with a non-zero status.

## Evidence

- **Workflow run id:** 39321691005
- **Failing job name:** drill
- **Run URL:** https://github.com/mcpmark-eval-liuhezi/ci-failure-drill/actions/runs/39321691005
- **Job URL:** https://github.com/mcpmark-eval-liuhezi/ci-failure-drill/actions/runs/39321691005/job/118297067380

## Failing step

| # | Step | Conclusion |
|---|------|------------|
| 1 | Set up job | success |
| 2 | Deliberately fail | **failure** |
| 3 | Complete job | success |

## Log excerpt (failed job "drill")

```text
2026-10-19T20:43:29.7262775Z ##[endgroup]
2026-10-19T20:43:29.7603914Z DRILL-CONTROLLED-FAILURE
2026-10-19T20:43:29.7617888Z ##[error]Process completed with exit code 1.
2026-10-19T20:43:29.7726683Z Cleaning up orphan processes
```

## Re-run attempt

The failed jobs of run 39321691005 were re-run (attempt 2, started 2026-10-19T20:48:08Z).

**Outcome:** the re-run attempt also **failed** with conclusion `failure` — expected, because the
workflow is designed to fail on every execution.

## Follow-ups

Follow-up work is tracked in the issue titled "CI failure drill follow-ups" (parent issue), with
sub-issues:

1. Add a green passing path to the drill workflow
2. Document the rerun procedure in the runbook
3. Merge the postmortem once reviewed

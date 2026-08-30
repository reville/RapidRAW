# RapidRAW Patch Manifest

Patch order matters for the combined build. Update this file whenever a branch is accepted upstream, intentionally dropped, or replaced by a newer snapshot.

| Order | Modification | Feature branch | Preserved commit | State | Upstream/PR status | Validation |
| ---: | --- | --- | --- | --- | --- | --- |
| 1 | macOS HEIC/HEIF import support | `codex/heic-import` | `82f690de` | keep | [Open PR #1643](https://github.com/CyberTimon/RapidRAW/pull/1643) | Committed and pushed |
| 2 | Hide unavailable zero-byte placeholders | `codex/hide-unavailable-placeholders` | `44dd0479` | keep | [Open PR #1644](https://github.com/CyberTimon/RapidRAW/pull/1644) | Committed and pushed |
| 3 | Cameras and Locations library views | `codex/cameras-locations` | `c2a43e96` | keep | [Open PR #1646](https://github.com/CyberTimon/RapidRAW/pull/1646) | Frontend production build passed 2026-08-30; full typecheck has pre-existing repository failures |
| 4 | Editor toolbar in the custom titlebar | `codex/move-editor-buttons-top-bar` | `0c0ffbcc` | keep | [Open PR #1645](https://github.com/CyberTimon/RapidRAW/pull/1645) | Frontend production build passed 2026-08-30; full typecheck has pre-existing repository failures |
| 5 | Prioritize editor rendering over thumbnail refreshes | `codex/prioritize-editor-rendering` | `35151a72` | keep | [Open PR #1647](https://github.com/CyberTimon/RapidRAW/pull/1647) | 10 Rust tests, strict Clippy, and frontend production build passed 2026-08-30 |

## Combined branch

- Branch: `personal/current`
- Base at setup: `origin/main` at `7ac8d50d`
- Canonical feature commits, in order: `82f690de`, `44dd0479`, `c2a43e96`, `0c0ffbcc`, `35151a72`
- Combined equivalents: `67edf3ba`, `5595e84a`, `5097cb34`, `3d10e64c`, `9c7b47e4`
- Final feature-delta commits in the combined branch: `1acdb669` and `b20d9fbe`
- Combined-stack compatibility fix: `bb91f7e7` (unique Rust test-module names)
- Purpose: Nicholas's installable custom build; never use it as the source branch for an upstream PR.
- Combined validation: frontend production build and the full 22-test Rust suite passed 2026-08-30.

The Cameras and titlebar commits in `personal/current` have the same stable patch IDs as their canonical feature commits; they were assembled from non-disruptive safety snapshots while the original worktrees were active.

## Working directories

| Alias | Path | Notes |
| --- | --- | --- |
| `current` | `current/` | Combined personal branch |
| `heic` | `features/heic-import` | Link to the existing HEIC worktree; currently also contains uncommitted titlebar work, preserved separately |
| `placeholders` | `features/hide-unavailable-placeholders` | Link to existing clean feature worktree |
| `cameras` | `features/cameras-locations` | Link to existing dirty WIP worktree; snapshot preserved separately |
| `toolbar` | `features/move-editor-buttons-top-bar` | Link to the finished feature worktree |
| `priority` | `/Users/nicholasreville/CODING/agent/rapidraw-editor-priority` | Clean feature worktree for PR #1647 |

## Safety snapshots

- `backup/2026-08-30-cameras-locations` at `a5e6da15` is patch-equivalent to `6874bfef`.
- `codex/editor-toolbar-titlebar` at `3651a6f9` is patch-equivalent to `13fa0179` and has its own clean worktree at `features/editor-toolbar-titlebar`.
- `backup/2026-08-30-cameras-locations-followup` at `a038873f` preserves the later uncommitted navigation follow-up without changing its active worktree.
- `backup/2026-08-30-toolbar-followup` at `f1dd4750` preserves the later uncommitted toolbar-layout follow-up without changing its active worktree.

The follow-up snapshots were superseded by the finalized feature commits above. They remain only as recovery points; `personal/current` contains the final deltas.

## Safety rules

1. Never keep the only copy of a modification in an uncommitted worktree or an upstream PR.
2. Never mix two PR features on the same feature branch.
3. Run `bin/rapidraw-patches bundle` before a rebase or conflict resolution.
4. Keep `origin` as the official upstream and push only to `fork`.
5. Use `personal/current` only to combine active patches for Nicholas's custom build.

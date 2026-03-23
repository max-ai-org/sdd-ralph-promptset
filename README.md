# sdd-ralph-promptset

This repository holds **markdown prompts for specification-driven development (SDD)** when you drive work with a **Ralph Wiggum–style loop**: the model gets a fixed, repeatable instruction for each turn, works within clear completion rules, and ends with an explicit machine-readable success or failure signal (for example a `<promise>…</promise>` line). An outer loop can keep invoking that pattern until the signal says the step is done or you choose to stop. The prompts here cover spec and code sniff passes, gap analyses, a build-oriented loop, and a minimal sanity prompt.

**Source of truth:** edits to these prompts belong in this repository. How you install or upgrade them in your environment is entirely up to you (manual steps, your own automation, or other tooling).

## Layout

| Path | Purpose |
|------|---------|
| [`prompts/`](prompts/) | Prompt files (markdown). |

## Repo layout

| Path | Purpose |
|------|---------|
| `prompts/*.md` | Prompt definitions. |
| [`docs/release-notes.md`](docs/release-notes.md) | Where release notes live and how releases are produced. |
| [`.github/workflows/release.yml`](.github/workflows/release.yml) | CI: commitlint on PR/push; semantic-release on push to release branches; zips `prompts/*.md` for the release asset. |

## Development

- **Commits** — Conventional commits (validated by commitlint; husky `commit-msg` hook after `npm install`). See [docs/release-notes.md](docs/release-notes.md).
- **Releases** — Semantic-release on push to `main`, `rc`, `alpha`, or `beta`. The workflow writes `sdd-ralph-promptset.zip` at the repo root (ignored by git), then attaches it to the GitHub release. Run `npm run semantic-release` for a dry-run (local dry-runs do not create the zip unless you run the same `zip` step yourself).

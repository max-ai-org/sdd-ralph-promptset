# Release notes

This document describes **where to find release notes** for sdd-ralph-promptset and how releases are produced.

## Where to find release notes

- **Location:** GitHub Releases for this repository. Each tagged release (created by semantic-release on push to `main`, `rc`, `alpha`, or `beta`) has a release page with notes.
- **Content:** For each release, the notes are generated from conventional commits (feat, fix, docs, etc.). Pre-releases (`rc`, `alpha`, `beta` branches) produce prerelease tags; `main` produces stable versions.
- **Assets:** Each release attaches **`sdd-ralph-promptset.zip`**: a zip of the markdown files from `prompts/` at the archive root (no extra directory wrapper). The GitHub Actions release job creates it with `zip` immediately before semantic-release uploads it; nothing in the repository “builds” the prompts beyond that CI step.

## Release process

Releases are fully automated:

- **Conventional commits:** Use commit types such as `feat:`, `fix:`, `docs:`, `chore:` (and optional scope/body). Commit messages are validated in CI and locally via the husky `commit-msg` hook (after `npm install`).
- **Branches:** Pushes to `main` (stable), `rc`, `alpha`, or `beta` (prereleases) trigger semantic-release. It determines the next version from commits since the last tag, creates the tag, and publishes the GitHub release with generated notes.
- **Dry-run:** From the repo root, run `npm run semantic-release` to see what version would be released and which commits would be included (no tag or release is created).

## Development

- **Commits** — Conventional commits (validated by commitlint; husky `commit-msg` hook). See this doc and [commitlint.config.js](../commitlint.config.js).
- **Releases** — Semantic-release on push to `main`, `rc`, `alpha`, or `beta`. The zip is created in CI (see [`.github/workflows/release.yml`](../.github/workflows/release.yml)) and uploaded as a release asset.

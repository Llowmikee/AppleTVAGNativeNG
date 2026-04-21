# Repository Owner Release Guide

This guide describes the release and publishing process for AppleTV AgNative NG.

## Required Branches

- `main` (required): source of truth for code and pull requests.

No `gh-page` branch is required in this setup.

## Recommended Branch Policy

- Protect `main`.
- Require pull requests for direct updates.
- Require `Build` workflow to pass before merge.
- Use squash merge for community PRs.

## Community Contribution Flow

1. Contributors open PRs into `main`.
2. CI (`Build`) validates every PR.
3. Maintainers review and merge approved PRs.
4. Multiple merged PRs are batched into one release.

## Release Model

Publishing is release-driven.

- `Create Release` workflow (manual) builds the plugin, creates checksum, creates a git tag, and publishes a GitHub Release with assets.
- `Publish Pages from Release` workflow runs automatically when a release is published and deploys GitHub Pages from the release asset.

## Release Preparation Checklist

Before creating a release:

1. Ensure all target PRs are merged to `main`.
2. Ensure `Build` is green on latest `main`.
3. Confirm release version (`vX.Y.Z`).
4. Confirm release notes scope (what PRs/features are included).

## How to Create a Release

1. Open GitHub Actions.
2. Run workflow: `Create Release`.
3. Fill inputs:
- `version`: for example `v0.4.0`
- `prerelease`: `true` for beta/rc, otherwise `false`
4. Start workflow.

Workflow output:

- tag is created and pushed
- GitHub Release is created
- assets are attached:
  - `appletv_agnative.js`
  - `checksums.txt`

## How Pages Publishing Works

When release status becomes `published`:

1. Workflow reads release asset `appletv_agnative.js`.
2. Builds `pages-dist` package.
3. Deploys to GitHub Pages.
4. Writes deployed release version to `pages-dist/version.txt`.

## Rollback Procedure

If a release is bad:

1. Publish a new patch release from fixed `main`.
2. Or republish a previous known-good release asset.

Recommended approach: always publish a new patch release (`vX.Y.(Z+1)`) for traceability.

## Operational Notes

- Do not edit `release/*` manually.
- Always release from current `main`.
- Keep release tags immutable.
- Use semantic versioning for predictable updates.

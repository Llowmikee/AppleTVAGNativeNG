# AppleTV AgNative NG

A Lampa plugin that reshapes top navigation, content cards, and selected UI parts in Apple TV style.

## Repository Layout

- `src/` - plugin source code
- `release/appletv_agnative.js` - compiled artifact
- `appletv_agnative.js` - root-level copy of the build artifact (for compatibility)
- `.github/workflows/ci-build.yml` - CI build for `main` and pull requests
- `.github/workflows/release.yml` - manual release workflow
- `.github/workflows/publish-pages-from-release.yml` - Pages deployment from published release
- `docs/REPOSITORY_OWNER_RELEASE_GUIDE.md` - repository owner release playbook

## Branch Strategy

### `main`

Primary development branch.

All feature work, fixes, and refactoring should be done here through pull requests.

What runs automatically:
- `Build` workflow (`npm ci` + `npm run build`)

No `gh-page` branch is required.

## Local Development

### Requirements

- Node.js 22+
- npm

### First Run

```bash
git clone <repo-url>
cd AppleTVAGNativeNG
npm ci
```

### Development Modes

```bash
npm run dev
```

Starts Rollup in watch mode.

```bash
npm run build
```

Creates a production build.

After `npm run build`:
- `release/appletv_agnative.js` is updated
- root `appletv_agnative.js` is synchronized automatically

## Pull Request Flow

1. Update local `main`
```bash
git checkout main
git pull origin main
```

2. Create a feature branch
```bash
git checkout -b feature/<short-name>
```

3. Build after changes
```bash
npm run build
```

4. Commit
```bash
git add .
git commit -m "feat: short description"
```

5. Push branch
```bash
git push -u origin feature/<short-name>
```

6. Open PR: `feature/<short-name>` -> `main`

## Release and Pages Publishing

Release publishing is batched and manual.

1. Merge selected PRs to `main`.
2. Run `Create Release` workflow from GitHub Actions.
3. Workflow creates tag + GitHub Release with assets.
4. `Publish Pages from Release` is triggered automatically and updates GitHub Pages.

For maintainer steps and branch governance, see:

- `docs/REPOSITORY_OWNER_RELEASE_GUIDE.md`

## Quality Notes

- Source of truth is `src/`
- Do not edit `release/*` manually
- Always run `npm run build` before opening a PR

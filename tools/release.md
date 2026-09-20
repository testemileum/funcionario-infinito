# Release Runbook — funcionario-infinito

`dev` receives development PRs; `main` is the default, release-only branch.
Release by fast-forwarding `main` to a stamped commit on `dev`, then tag it.
No release branches, release PRs, merge commits, or back-merges are needed.
`main` stays an ancestor of `dev`. Only maintainers may push to `main`, with
required status checks and force-push/deletion blocked.

This is a hand-run process. It does not publish to npm; npm maintenance stays
on `V6.12`. Use Git, `uv`, and the Node version in `docs-site/.nvmrc`.
Pause other pushes and merges into `dev` until the next placeholder is pushed.
Do the release in one sitting. Stop on any failed command or unexpected diff.

## 1. Prepare

Start in a clean funcionario-infinito checkout with no unpublished commits:

```bash
git status --porcelain
git fetch origin
git switch dev
git pull --ff-only origin dev
test "$(git rev-parse HEAD)" = "$(git rev-parse origin/dev)"
git merge-base --is-ancestor origin/main dev

funcionario_release_version=6.13.0
funcionario_next_version=6.13.1-next
git show origin/main:skills/funcionario/module-manifest.toml
git tag --list "v$funcionario_release_version"
```

Choose the versions explicitly. The release must differ from what `main`
serves and must not reuse a tag. Use SemVer, optionally with a prerelease;
no `-dev` or build metadata (`+...`). The next placeholder is the next patch
with `-next`. The stamper enforces the version syntax, not release history.

## 2. Stamp and push dev

```bash
uv run --python 3.11 tools/stamp_release.py "$funcionario_release_version"
git diff
git add skills/*/module-manifest.toml
git commit -m "chore(release): v$funcionario_release_version"
funcionario_release_commit=$(git rev-parse HEAD)
uv sync --frozen && (cd docs-site && npm ci) && uv run --frozen tools/quality.py
git push origin dev
```

Review before committing: only the version in the 29 manifests should
change. Run the quality gate on committed `HEAD` in this checkout
before pushing; keep that tested commit checked out through promotion/tagging.
Wait for its required GitHub status checks to pass before promoting it.

## 3. Fast-forward main and tag

```bash
git fetch origin
test "$(git rev-parse HEAD)" = "$funcionario_release_commit"
test "$(git rev-parse origin/dev)" = "$funcionario_release_commit"
git merge-base --is-ancestor origin/main dev
git push origin dev:main
git fetch origin
test "$(git rev-parse origin/main)" = "$funcionario_release_commit"
git tag -a "v$funcionario_release_version" "$funcionario_release_commit" -m "Release v$funcionario_release_version"
git push origin "refs/tags/v$funcionario_release_version"
```

The tag identifies the same stamped commit on `dev` and `main`. Never force
a push or move a release tag. If `dev` moved, stop rather than including
unreviewed changes in the release.

## 4. Stamp the next placeholder

```bash
git fetch origin
test "$(git rev-parse origin/dev)" = "$funcionario_release_commit"
uv run --python 3.11 tools/stamp_release.py "$funcionario_next_version"
git diff
git add skills/*/module-manifest.toml
git commit -m "chore: bump placeholder version to $funcionario_next_version"
uv sync --frozen && (cd docs-site && npm ci) && uv run --frozen tools/quality.py
git push origin dev
```

Review the same version-only changes before committing. `main` and the tag
retain the release version; `dev` carries the next placeholder. Development
can resume. Nothing needs merging back.

## 5. Rebuild and verify

In the `funcionario-infinito/funcionario-plugins` checkout, confirm its release script sources
`funcionario-infinito/funcionario-infinito` `main`, then run `python3 release.py`. Follow that
repository's instructions to review, validate, commit, and push the plugins.
Verify the release through `npx skills add funcionario-infinito/funcionario-infinito` and both
the Claude and Codex marketplaces.

Installed copies check `main` through `raw.githubusercontent.com`, which caches
files for around five minutes. Verify the release through Git first, or wait
before trusting an update check that still reports the previous version.

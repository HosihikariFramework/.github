# AGENTS.md

Organization profile and default GitHub configuration for the Hosihikari Framework.

## Repository map

- `profile/README.md` — English organization profile.
- `profile/README.zh_hans.md` — Chinese organization profile.
- `.github/ISSUE_TEMPLATE/` — default issue forms for repositories without local templates.
- `.github/PULL_REQUEST_TEMPLATE.md` — default pull request template.
- `CONTRIBUTING.md` — default contribution workflow for repositories without their own.
- `SUPPORT.md` — default support and documentation links.
- `LICENSE.md` — license text used by the organization profile.

## Verification

There is no build. Before pushing:

```bash
git diff --check
npx --yes prettier --check ".github/ISSUE_TEMPLATE/*.yml"
```

GitHub validates issue forms when the pull request is rendered. Open the files in the GitHub
preview and confirm every form still appears under **New issue**.

## Invariants

- English is the primary profile; keep `README.zh_hans.md` in sync.
- Issue forms under `.github/ISSUE_TEMPLATE/` are organization defaults. A repository with
  its own `ISSUE_TEMPLATE` folder ignores the entire default folder, including `config.yml`.
- Default forms must not reference labels unless those labels exist in every consuming repository.
- `CONTRIBUTING.md` and `SUPPORT.md` are organization defaults; a repository's own file replaces the
  corresponding default.
- Do not add `SECURITY.md` until a private reporting channel exists. A public issue template must not
  point at a reporting path that does not work.
- Work on a branch, open a pull request, and squash merge. Do not push to `main`.

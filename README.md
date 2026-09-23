# Prbl Security Scan — GitHub Action

Find the security holes AI code generators leave behind. Prbl scans your repo on
every push and pull request and **comments the findings right in the PR**, so
issues get caught before they merge.

- Exposed API keys, disabled TLS checks, missing auth, and other AI-introduced flaws
- Inline PR comments (updated on every push)
- Free plan: scans every push and pull request and comments findings
- Pro plan: also fails the build on high-severity findings, and the AI rewriter applies and verifies fixes
- Get an API key at [getprbl.com](https://getprbl.com)

## Easiest: install the GitHub App

No workflow file, no API key. Install [Prbl Security](https://github.com/apps/prbl-security) on your account or org and every pull request gets a `prbl[bot]` comment with the findings, updated on each push. Free.

## Or: use this Action

Add `.github/workflows/prbl.yml`:

```yaml
name: Prbl security scan
on: [push, pull_request]
permissions:
  contents: read
  pull-requests: write
jobs:
  prbl:
    runs-on: ubuntu-latest
    steps:
      - uses: Get-Prbl/prbl-action@v1
        with:
          api-key: ${{ secrets.PRBL_API_KEY }}
          # fail-on-high: true   # Pro: block merges on high-severity findings
```

Then add your API key (dashboard → Settings) as a repo secret named `PRBL_API_KEY`
(Settings → Secrets and variables → Actions).

## Inputs

| Input | Required | Default | Description |
|---|---|---|---|
| `api-key` | yes | — | Your Prbl API key. Store as a secret. |
| `fail-on-high` | no | `false` | Fail the build when a high-severity finding is present. Pro plan; on free the Action warns instead. |

## Badge

```
[![Scanned by Prbl](https://prbl-dashboard.vercel.app/api/badge?repo=OWNER/REPO)](https://getprbl.com)
```

Made by [Prbl](https://getprbl.com).

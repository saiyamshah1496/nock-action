# Nock — Estate-aware Postgres DDL (GitHub Action)

```yaml
uses: saiyamshah1496/nock-action@v0.1.9
```

Approve or block Postgres DDL in PRs from your estate and policy. Never applies migrations — this Action only analyzes changes and sets PR status/comments accordingly.

- Root-level `action.yml` for GitHub Marketplace
- Bundled `dist/` checked in — no build step required
- Project home: https://github.com/saiyamshah1496/nock

## Inputs

- `github-token` (required): GitHub token for PR comments
- `migration-path` (optional): Path or glob for migration SQL files (default: `migrations/`)
- `estate-path` (optional): Path to `estate.json` for file mode (default: `.nock/estate.json`)
- `estate-api-url` (optional): GET URL for hosted estate API (Nock Team)
- `estate-api-token` (optional): Bearer token for hosted estate API
- `api-base-url` (optional): Override API base (defaults to origin from `estate-api-url`)
- `policy-path` (optional): Path to `policy.yml` (YAML or JSON) (default: `policy.default.yml`)
- `fail-on` (optional): `red`|`yellow` (default: `red`)

## Example

```yaml
name: Check Postgres DDL with Nock
on:
  pull_request:
    types: [opened, synchronize]

jobs:
  nock:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - name: Nock — Estate-aware Postgres DDL
        uses: saiyamshah1496/nock-action@v0.1.9
        with:
          github-token: ${{ secrets.GITHUB_TOKEN }}
          # migration-path: migrations/
          # estate-path: .nock/estate.json
          # estate-api-url: https://example.com/estate
          # estate-api-token: ${{ secrets.NOCK_ESTATE_TOKEN }}
          # api-base-url: https://api.example.com
          # policy-path: policy.default.yml
          # fail-on: red
```

## Note for existing users
This standalone Action is equivalent to the monorepo subdirectory Action. Existing references continue to work:

```yaml
uses: saiyamshah1496/nock/packages/action@v0.1.9
```

## License
MIT — see `LICENSE`.

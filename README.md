# dating-test-registry

Test pool registry for [dating.dev](https://dating.dev) — a decentralized, terminal-native dating platform.

## What is this?

This repo is a directory of dating pools. Pool operators register their pools here via Pull Requests. Users browse this registry to discover and join pools.

## Structure

```
pools/
  {pool-name}/
    pool.json       Pool metadata, operator public key, OAuth client IDs
    tokens.bin      Base64-encoded GitHub PAT for the pool repo
```

## pool.json

Each pool entry contains:

```json
{
  "name": "berlin-singles",
  "repo": "owner/berlin-singles",
  "description": "Dating pool for Berlin tech community",
  "operator_public_key": "abc123...",
  "github_client_id": "Iv1.xxx",
  "google_client_id": "123.apps.googleusercontent.com",
  "relay_url": "wss://relay.example.com",
  "created_at": "2026-03-14T12:00:00Z"
}
```

## tokens.bin

The `tokens.bin` file contains a base64-encoded JSON payload:

```json
{"gh_token": "github_pat_xxx"}
```

This token is used by the relay server to access the pool repo's GitHub API (avoids the 60 req/hr anonymous limit).

## For Users

```bash
# Install the CLI
curl -sSL https://dating.dev/install.sh | sh

# Browse pools
dating pool browse

# Join a pool
dating pool join berlin-singles
```

## For Pool Operators

```bash
# Create a pool and register it here
dating pool create my-pool \
  --repo owner/my-pool \
  --gh-token github_pat_xxx \
  --github-client-id Iv1.xxx \
  --relay-url wss://relay.example.com \
  --registry-token github_pat_yyy
```

This creates a PR to this registry with `pools/{name}/pool.json` and `pools/{name}/tokens.bin`. The maintainer reviews and merges it.

## Running Your Own Registry

Anyone can run their own registry. Fork this repo and point the CLI at it:

```bash
dating pool browse --registry your-org/your-registry
```

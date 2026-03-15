# dating-test-registry

Test pool registry for [dating.dev](https://dating.dev) — a decentralized, terminal-native dating platform.

## What is this?

This repo is a directory of dating pools. Pool operators register their pools here via Pull Requests. Users browse this registry to discover and join pools.

## Structure

```
pools/
  {pool-name}/
    pool.json       Pool metadata + operator public key
    tokens.bin      GitHub PAT encrypted to operator's pubkey (NaCl box)
```

## pool.json

```json
{
  "name": "berlin-singles",
  "repo": "owner/berlin-singles",
  "description": "Dating pool for Berlin tech community",
  "operator_public_key": "abc123...",
  "relay_url": "wss://relay.example.com",
  "created_at": "2026-03-14T12:00:00Z"
}
```

## tokens.bin

The pool's GitHub PAT, encrypted to the operator's public key using NaCl box. Only the relay server (which holds the operator's private key) can decrypt it.

The relay uses this token to access the pool repo's GitHub API for fetching user profiles during discovery.

## For Users

```bash
# Install the CLI
curl -sSL https://dating.dev/install.sh | sh

# Browse pools
dating pool browse

# Join a pool (uses your GitHub account via `gh` CLI or PAT)
dating pool join berlin-singles
```

## For Pool Operators

```bash
# Create a pool and register it here
dating pool create my-pool \
  --repo owner/my-pool \
  --gh-token github_pat_xxx \
  --relay-url wss://relay.example.com \
  --registry-token github_pat_yyy
```

This creates a PR to this registry with `pools/{name}/pool.json` and an encrypted `pools/{name}/tokens.bin`. The maintainer reviews and merges it.

## Running Your Own Registry

Anyone can run their own registry. Fork this repo and point the CLI at it:

```bash
dating pool browse --registry your-org/your-registry
```

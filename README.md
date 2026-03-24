# <3 dating registry

Pool registry for [dating.dev](https://dating.dev) — a directory of matching pools.

## Structure

```
registry.yaml        Registry metadata (name, tagline, accent, pools list)
```

## registry.yaml

```yaml
name: "<3 dating"
tagline: "terminal-native dating for developers"
accent: pink
version: 1

pools:
  - name: test-pool
    repo: vutran1710/dating-test-pool
```

## For Users

```bash
# Add this registry
dating registry add vutran1710/dating-test-registry

# Browse pools
dating pool browse
```

## For Pool Operators

Register your pool by submitting a PR that adds your pool to the `pools` list in `registry.yaml`.

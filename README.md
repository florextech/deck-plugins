# Deck Plugin Registry

Official plugin registry for [Deck](https://github.com/florextech/deck).

## Adding your plugin

1. Fork this repo
2. Add your plugin to `registry.json`
3. Open a PR

### Plugin entry format

```json
{
  "id": "my-plugin",
  "name": "My Plugin",
  "description": "What it does",
  "author": "Your Name",
  "version": "1.0.0",
  "url": "https://raw.githubusercontent.com/you/repo/main/plugin.js"
}
```

### Requirements

- Plugin must be a single `.js` file
- Must export `{ name, version, setup(deck) }`
- No malicious code
- Must work without additional dependencies (use Node.js built-ins)

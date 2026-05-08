# Deck Plugin Registry

Official plugin registry for [Deck](https://github.com/florextech/deck) — the open-source AI Command Center.

## Available Plugins

| Plugin | Description | Platforms |
|--------|-------------|-----------|
| 🕐 Clock | Live time and date widget | 🍎 🪟 🐧 |
| 📊 System Monitor | CPU, RAM usage and uptime | 🍎 🪟 🐧 |
| 🎵 Spotify | Playback control + now playing | 🍎 |
| 🍅 Pomodoro Timer | 25 min focus timer | 🍎 🪟 🐧 |

## Installing Plugins

Plugins are installed directly from the Deck app:

1. Open Deck → Settings → Plugins tab
2. Browse available plugins
3. Click **Install**
4. Restart Deck to activate

You can also **enable/disable** installed plugins without removing them using the toggle switch.

## Adding Your Plugin

1. Fork this repo
2. Add your plugin entry to `registry.json`
3. Open a PR

### Registry Entry Format

```json
{
  "id": "my-plugin",
  "name": "My Plugin",
  "description": "Short description",
  "readme": "Detailed markdown description shown in the store",
  "author": "Your Name",
  "version": "1.0.0",
  "official": false,
  "tags": ["widget", "utility"],
  "platforms": ["macos", "windows", "linux"],
  "url": "https://raw.githubusercontent.com/you/repo/main/my-plugin.js"
}
```

### Fields

| Field | Required | Description |
|-------|----------|-------------|
| `id` | ✅ | Unique identifier (used as filename) |
| `name` | ✅ | Display name |
| `description` | ✅ | One-line description |
| `readme` | ❌ | Detailed markdown shown in plugin details |
| `author` | ✅ | Author name |
| `version` | ✅ | Semver version |
| `official` | ❌ | `true` if maintained by Deck team |
| `tags` | ❌ | Array of category tags |
| `platforms` | ❌ | Supported platforms: `macos`, `windows`, `linux` |
| `url` | ✅ | Raw GitHub URL to the `.js` file |

### Plugin File Requirements

- Single `.js` file (CommonJS)
- Must export `{ name, version, setup(deck) }`
- No external dependencies (use Node.js built-ins only)
- No malicious code (`eval`, `child_process` for non-obvious purposes, etc.)

### Plugin API (`deck` object)

```js
module.exports = {
  name: 'my-plugin',
  version: '1.0.0',
  setup(deck) {
    // Register a custom action type
    deck.registerAction('my:action', (payload) => { /* ... */ });

    // Register a live widget (shown on deck grid)
    deck.registerWidget('my-widget', {
      interval: 5000, // update interval in ms
      getData: () => ({ value: 'hello' }),
    });

    // Send a notification to connected clients
    deck.notify('Plugin loaded!', 'success'); // levels: info, success, warning, error

    // Get current deck actions
    const actions = deck.getActions();
  }
};
```

## Platform Support

Plugins declare which platforms they support via the `platforms` field. Deck will:
- Show platform badges (🍎 🪟 🐧) in the plugin store
- Warn users before installing on an unsupported platform
- Allow enabling/disabling per-platform plugins without uninstalling

## License

MIT — [Florex Labs](https://github.com/florextech)

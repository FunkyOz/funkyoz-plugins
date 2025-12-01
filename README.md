# Claude Code Plugins Marketplace

A curated marketplace of powerful plugins to enhance your Claude Code experience.

## What is This?

This is a plugin marketplace for Claude Code that provides centralized access to high-quality plugins. Marketplaces allow you to easily discover, install, and manage Claude Code extensions from a single source.

## Available Plugins

### Software Engineer Plugin
**Version:** 1.0.0
**Author:** Lorenzo Dessimoni

A comprehensive Software Engineer plugin for Claude Code that enhances development workflows with specialized tools and capabilities.

## Installation

### Prerequisites

- Claude Code installed on your system
- Git (for cloning from GitHub)

### Quick Start

Add this marketplace to your Claude Code installation using one of the following methods:

#### Option 1: From GitHub (Recommended)

```bash
/plugin marketplace add funkyoz/funkyoz-plugins
```

#### Option 2: From Git URL

```bash
/plugin marketplace add https://github.com/funkyoz/funkyoz-plugins.git
```

#### Option 3: From Local Path

If you've cloned this repository locally:

```bash
/plugin marketplace add /path/to/funkyoz-plugins
```

Or directly reference the marketplace file:

```bash
/plugin marketplace add /path/to/funkyoz-plugins/.claude-plugin/marketplace.json
```

### Verify Installation

List all your configured marketplaces:

```bash
/plugin marketplace list
```

You should see `funkyoz-plugins` in the list.

## Installing Plugins

Once you've added the marketplace, you can install plugins in two ways:

### Interactive Installation

Browse and install plugins interactively:

```bash
/plugin
```

This will show you all available plugins from all your marketplaces. Select the one you want to install.

### Direct Installation

Install a specific plugin by name:

```bash
/plugin install software-engineer@funkyoz-plugins
```

The format is: `/plugin install <plugin-name>@<marketplace-name>`

## Updating Marketplace and Plugins

### Why Update?

Plugin marketplaces and their plugins receive regular updates that include:
- New features and capabilities
- Bug fixes and performance improvements
- Security patches
- New plugins added to the marketplace

It's recommended to periodically check for updates to ensure you have the latest versions.

### Update Marketplace Metadata

When the marketplace adds new plugins or updates plugin information, refresh the marketplace catalog:

```bash
/plugin marketplace update funkyoz-plugins
```

This command:
- Fetches the latest [marketplace.json](.claude-plugin/marketplace.json) file from the repository
- Updates the list of available plugins
- Refreshes plugin versions and descriptions
- Does **not** automatically update installed plugins

### Update Individual Plugins

After updating the marketplace metadata, you'll see if newer plugin versions are available. To update a specific plugin:

```bash
/plugin update software-engineer
```

This will:
- Check if a newer version is available in the marketplace
- Download and install the latest version
- Preserve your existing plugin configuration

### Update All Plugins

To update all installed plugins from all marketplaces at once:

```bash
/plugin update --all
```

### Check for Available Updates

To see which plugins have updates available without installing them:

```bash
/plugin list
```

This will show all installed plugins with their current versions. Compare these with the marketplace listing to identify outdated plugins.

### Update Workflow (Recommended)

Follow this workflow to stay current:

1. **Update marketplace metadata** (monthly or when you know updates are available):
   ```bash
   /plugin marketplace update funkyoz-plugins
   ```

2. **Check what's new**:
   ```bash
   /plugin
   ```
   Browse the marketplace to see new or updated plugins

3. **Update installed plugins**:
   ```bash
   /plugin update software-engineer
   ```
   Or update all at once:
   ```bash
   /plugin update --all
   ```

### Version Management

The marketplace tracks plugin versions in the [marketplace.json](.claude-plugin/marketplace.json) file. When you update:

- **Marketplace updates** pull the latest metadata from the git repository
- **Plugin updates** download the latest plugin code from their respective sources
- Updates are **non-breaking** - your configurations are preserved

### Auto-Update for Teams

If your team uses the marketplace configuration in `.claude/settings.json`, team members can stay synchronized:

```json
{
  "extraKnownMarketplaces": [
    {
      "source": "github",
      "repo": "funkyoz/funkyoz-plugins"
    }
  ]
}
```

When users run `/plugin marketplace update funkyoz-plugins`, they'll get the same marketplace version as the rest of the team.

## Managing the Marketplace

### List All Marketplaces

See all configured marketplaces:

```bash
/plugin marketplace list
```

### Remove Marketplace

If you need to remove this marketplace and all its installed plugins:

```bash
/plugin marketplace remove funkyoz-plugins
```

**Warning:** This will also uninstall any plugins installed from this marketplace.

## Team Configuration

If you're using this marketplace in a team setting, you can configure it to be automatically installed for all team members.

Add this to your project's `.claude/settings.json`:

```json
{
  "extraKnownMarketplaces": [
    {
      "source": "github",
      "repo": "funkyoz/funkyoz-plugins"
    }
  ]
}
```

When team members trust the repository, Claude Code will automatically install this marketplace and any specified plugins.

## Troubleshooting

### Marketplace Not Found

If you get an error when adding the marketplace:

1. **Check your internet connection** - Ensure you can access GitHub
2. **Verify the repository exists** - Visit [https://github.com/funkyoz/funkyoz-plugins](https://github.com/funkyoz/funkyoz-plugins)
3. **Check for typos** - Make sure you've entered the correct owner/repo name

### Plugin Installation Fails

1. **Update the marketplace** first:
   ```bash
   /plugin marketplace update funkyoz-plugins
   ```

2. **Check plugin availability**:
   ```bash
   /plugin
   ```
   Browse to see if the plugin appears in the list

3. **Check for permissions** - If using a private repository, ensure you have access

### Update Issues

If marketplace or plugin updates fail:

1. **Check git access** - Ensure you can pull from the repository
2. **Verify network connectivity** - Updates require internet access
3. **Check for local modifications** - If you've modified plugins locally, updates may conflict
4. **Remove and reinstall** - As a last resort:
   ```bash
   /plugin marketplace remove funkyoz-plugins
   /plugin marketplace add funkyoz/funkyoz-plugins
   ```

### Validation Errors

If you're developing or modifying plugins locally, validate them before sharing:

```bash
claude plugin validate .
```

## Support

For issues, questions, or contributions:

- **Email:** lorenzo.dessimoni@gmail.com
- **Issues:** Report problems via the repository's issue tracker

## Plugin Development

Want to contribute a plugin to this marketplace? Check out the [Claude Code Plugin Documentation](https://code.claude.com/docs/en/plugin-marketplaces) for detailed information on creating and submitting plugins.

## License

Please refer to individual plugin licenses for usage terms and conditions.

---

**Marketplace Maintainer:** Lorenzo Dessimoni (lorenzo.dessimoni@gmail.com)

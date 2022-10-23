# Ansible Role Discord
This is an Ansible role that installs Discord on Linux. It uses the tarball from the official website so this role is not dependent on any package manager.  
It can also optionally install BetterDiscord, a client mod that allows for plugin loading.

Tested on Fedora 36, should work on any Linux distribution that the Discord tarball supports.

## Requirements

### Base requirements
None  

### Installing BetterDiscord
An actively running desktop environment is needed. This is needed so that Discord can generate the necessary files for BetterDiscord to work.  

## Variables
| Variable | Default | Description |
|----------|---------|-------------|
| `discord_version` | `discord` | Version of Discord to install. Valid options are: `[discord, canary, ptb]` |
| `discord_install_betterdiscord` | `false` | Whether to install BetterDiscord or not. |
| `discord_user` | `{{ ansible_user }}` | User to install Discord for. |

## Installing plugins and themes
To install plugins and themes for BetterDiscord, define the `discord_betterdiscord_plugins` and `discord_betterdiscord_themes` variables.
```
discord_betterdiscord_plugins:
  - "https://example.com/plugin.plugin.js"
  - "https://example.com/another.plugin.js"

discord_betterdiscord_themes:
    - url: "https://betterdiscord.app/Download?id=ID"
      name: "Theme Name"
```

<details> <summary> Example </summary>

```
discord_betterdiscord_plugins:
  - "https://raw.githubusercontent.com/rauenzi/BetterDiscordAddons/master/Plugins/BetterRoleColors/BetterRoleColors.plugin.js"

discord_betterdiscord_themes:
  - url: https://betterdiscord.app/Download?id=124
    name: HorizontalServerList
```

</details>
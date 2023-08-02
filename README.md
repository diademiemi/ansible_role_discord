Ansible Role Discord
=========

[![Molecule Test](https://github.com/diademiemi/ansible_role_discord/actions/workflows/molecule.yml/badge.svg)](https://github.com/diademiemi/ansible_role_discord/actions/workflows/molecule.yml)

This is an Ansible role that installs Discord on Linux. It uses the tarball from the official website so this role is not dependent on any package manager.  
It can also optionally install BetterDiscord, a client mod that allows for plugin loading.  

Requirements
------------
These platforms are supported:
- Ubuntu 20.04
- Ubuntu 22.04
- Debian 10
- Debian 11
- EL 8 (Tested on Rocky Linux 8)
- EL 9 (Tested on Rocky Linux 9)
- Fedora 38
- openSUSE Leap 15.4

<!--
- List hardware requirements here  
-->

Role Variables
--------------

Variable | Default | Description
--- | --- | ---
`discord_version` | `discord` | Version of Discord to install. Valid options are: `[discord, canary, ptb]`
`discord_install_betterdiscord` | `false` | Whether to install BetterDiscord or not.
`discord_user` | `{{ ansible_user_id }}` | User to install BetterDiscord with.
`discord_betterdiscordctl_url` | `"https://raw.githubusercontent.com/bb010g/betterdiscordctl/master/betterdiscordctl"` | URL to download betterdiscordctl from.
`discord_betterdiscord_config_dir` | `"~/.config/BetterDiscord"` | Directory to install BetterDiscord plugins and themes to.
`discord_betterdiscord_plugins` | `[]` | List of BetterDiscord plugins to install.
`discord_betterdiscord_themes` | `[]` | List of BetterDiscord themes to install.

Dependencies
------------
An actively running desktop environment is needed. This is needed so that Discord can generate the necessary files for BetterDiscord to work.  


Installing plugins and themes
-----------------------------

To install plugins and themes for BetterDiscord, define the `discord_betterdiscord_plugins` and/or `discord_betterdiscord_themes` variables.
```yaml
discord_betterdiscord_plugins:
  - "https://example.com/plugin.plugin.js"
  - "https://example.com/another.plugin.js"

discord_betterdiscord_themes:
    - url: "https://betterdiscord.app/Download?id=ID"
      name: "Theme Name"
```

<details> <summary> Example </summary>

```yaml
discord_betterdiscord_plugins:
  - "https://raw.githubusercontent.com/rauenzi/BetterDiscordAddons/master/Plugins/BetterRoleColors/BetterRoleColors.plugin.js"

discord_betterdiscord_themes:
  - url: https://betterdiscord.app/Download?id=124
    name: HorizontalServerList
```

</details>

Example Playbook
----------------

```yaml
- name: Use diademiemi.discord role
  hosts: "{{ target | default('discord') }}"
  roles:
    - role: "diademiemi.discord"
      tags: ['diademiemi', 'discord', 'setup']    ```

```

License
-------

MIT

Author Information
------------------

- diademiemi (@diademiemi)

Role Testing
------------

This repository comes with Molecule tests for Docker on the supported platforms.
Install Molecule by running

```bash
pip3 install -r requirements.txt
```

Run the tests with

```bash
molecule test
```

These tests are automatically ran by GitHub Actions on push. If the tests are successful, the role is automatically published to Ansible Galaxy.

# Ansible Role: Tmux

[![CI](https://github.com/pluggero/ansible-role-tmux/actions/workflows/ci.yml/badge.svg)](https://github.com/pluggero/ansible-role-tmux/actions/workflows/ci.yml) [![Ansible Galaxy downloads](https://img.shields.io/ansible/role/d/pluggero/tmux?label=Galaxy%20downloads&logo=ansible&color=%23096598)](https://galaxy.ansible.com/ui/standalone/roles/pluggero/tmux)

An Ansible Role that installs a basic configuration of tmux.

## Requirements

None.

## Role Variables

Available variables are listed below, along with default values (see `defaults/main.yml`):

### `tmux_key_bindings`

Each entry supports `key` (required), `command` (required), and `flags` (optional, e.g. `-n`, `-r`, `-T copy-mode-vi`). Multi-step sequences use `\;` as separator in `command`.

```yaml
tmux_key_bindings:
  - key: "C-l"
    command: "send 'C-l'"
    flags: "-n"
  - key: "C-y"
    command: "copy-mode \\; send -X cursor-up"
    flags: "-n"
```

For multi-line readability, use YAML folded scalar (`>-`) **without** trailing backslashes—YAML collapses newlines automatically:

```yaml
- key: "C-y"
  flags: "-n"
  command: >-
    copy-mode \;
    send -X cursor-up \;
    send -X search-backward "$USER@$hostname"
```

Multi-step commands (containing `\;`) are automatically formatted with backslash line continuations (`\`) in the generated `tmux.conf` for readability.

## Dependencies

None.

## Example Playbook

```yaml
- hosts: all
  roles:
    - pluggero.tmux
```

## License

MIT / BSD

## Author Information

This role was created in 2025 by Robin Plugge.

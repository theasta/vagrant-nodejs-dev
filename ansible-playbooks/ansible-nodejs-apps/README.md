# ansible-nodejs-apps

An ansible role to bootstrap nodejs application using fovever


## Requirements

nodejs, npm. This requirements are not installed by the role.

## Role Variables

* `npm.global_packages` Npm global packages to install. Defaults to `grunt-cli`.
* `apps.enabled` Path to apps to boot. No defaults option.

## Example Playbook

    - hosts: servers
      roles:
        - role: ansible-nodejs-apps
          apps:
            enabled:
              - "/srv/myapp/"
              - "/srv/anotherapp/"

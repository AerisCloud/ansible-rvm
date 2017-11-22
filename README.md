Ansible RVM role
================

This Ansible role installs RVM and the required ruby version.
Installation is possible for system or for single user (without root privileges)

Requirements
------------
Tested with CentOS 6.4, 6.5, 7.0, Debian 6.0.10, 7.8, 8.1, Fedora 18, 19, 20, 21, Ubuntu 10.04, 12.04, 13.10, 14.04, 14.10

Role Variables
--------------

- `rvm_install_type` per default set to `system` (valid values: `system`, `user`)
- `rvm_default_ruby_version` per default set to `ruby-2.2.2`
- `rvm_auto_update_rvm` per default set to `true`
- `rvm_autolibs` per default set to `3` - controls automatic installation of dependencies of rvm and ruby (if needed)
  - `0` -> Do not do anything (not installing dependencies and ruby or rvm can be unusable after installation)
  - `1` -> Use available libs, ignore missing (ruby or rvm can be unusable after installation)
  - `2` -> Use libs, fail if some are missing (good option for local installation on user without package manager access)
  - `3` -> Use libs, install missing libs (works if you have package manager rights)
  - `4` -> Install missing package manager (only OSX, on Linux it's like 3)
- `rvm_url` per default set to `https://get.rvm.io`
- `rvm_root` per default set to `/usr/local/rvm`
- `rvm_init_script` per default set to `/etc/profile.d/rvm.sh`

The last two variables are set according to whether a `system`-wide install (Multi-User install), or a Single-User install has been chosen with `rvm_install_type`.

The palybook should runs on user with sufficient permissions:
- to install dependencies via `apt` or `yum` if you do not have installed `curl` and `gnupg2` pakages
- to install dependencies via `apt` or `yum` if you set `rvm_autolibs` to `3` or `4` (default `3`)
- to install in system path for example in `system` mode (`rvm_install_type`  variable) 

If you want to install on unprivileged user you should have system dependencies installed and set:
- `rvm_install_type` to `user`
- `rvm_autolibs` prefably to `2`

When the playbook is run with `rvm_install_type = user`, the playbook will install RVM to the home directory of the `ansible_ssh_user`.
The defaults for the last two variables are then:

- `rvm_root`: `~/.rvm`
- `rvm_init_script`: `~/.rvm/scripts/rvm`

License
-------
Licensed under [MIT](https://github.com/newmen/rvm/blob/master/LICENSE). Do what you want with it.

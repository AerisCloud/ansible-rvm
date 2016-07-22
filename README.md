Ansible RVM role
===

This Ansible role installs RVM as root and the required ruby version. If user isn't root (executing without sudo) then RVM will be installed to the user home directory, but you need to change pathes to it own RVM through variables `rvm_root` and `rvm_init_script`.

Requirements
------------
Tested with CentOS 6.5, Debian 6, 7, Fedora 18, 19, 20, 21, Ubuntu 10.04, 12.04, 13.10

Role Variables
--------------
- `rvm_ruby_version` per default set to `ruby-2.2.0`
- `rvm_auto_update_rvm` per default set to `true`
- `rvm_url` per default set to `https://get.rvm.io`
- `rvm_root` per default set to `/usr/local/rvm`
- `rvm_init_script` per default set to `/etc/profile.d/rvm.sh`
- `rvm_autolibs` per default set to `3` - controls automatic installation of dependencies of rvm and ruby (if needed)
  - `0` -> Do not do anything (not installing dependencies and ruby or rvm can be unusable after installation)
  - `1` -> Use available libs, ignore missing (ruby or rvm can be unusable after installation)
  - `2` -> Use libs, fail if some are missing (good option for local installation on user without package manager access)
  - `3` -> Use libs, install missing libs (works if you have package manager rights)
  - `4` -> Install missing package manager (only OSX, on Linux it's like 3)

The `rvm_root` and `rvm_init_script` have presented values because installation runs with root permissions by default (if you passed `-s` option when you're running your playbook)

License
-------
Licensed under [MIT](https://github.com/newmen/rvm/blob/master/LICENSE). Do what you want with it.

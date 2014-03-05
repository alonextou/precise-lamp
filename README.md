# Ubuntu 12.04 64-bit LAMP Environment
## Local development environment
### Requirements
1. VirtualBox
2. Vagrant
### Instructions
1. Add `192.168.33.33 web.dev` to your hosts file.
2. Copy "config.yml.dist" to "config.yml" and, and update your working directory.
3. Add your application cookbooks to Berksfile.
4. `vagrant up`
## Remote staging environment
### Requirements
1. Ruby
2. RubyGems [knife-solo]
### Instructions
1. Copy "nodes/site.json.dist" to "your.domain.json" and update parameters.
2. `knife solo bootstrap user@domain`

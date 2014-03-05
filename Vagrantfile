require 'yaml'
vconfig = YAML::load_file('config.yml')

Vagrant.configure("2") do |config|

  config.vm.hostname = "joomla.jw.dev"
  config.vm.box = "precise64"
  config.vm.box_url = "http://files.vagrantup.com/precise64.box"
  config.vm.network :public_network
  config.vm.network :private_network, ip: "192.168.33.33"
  config.vm.network :forwarded_port, guest: 80, host: 8080
  config.vm.synced_folder vconfig['webroot'], "/var/www"

  config.omnibus.chef_version = :latest
  config.berkshelf.enabled = true

  config.vm.provision :chef_solo do |chef|
    chef.cookbooks_path = "cookbooks"
    chef.add_recipe "apt"
    chef.add_recipe "build-essential"
    chef.add_recipe "git"
    chef.add_recipe "php"
    chef.add_recipe "apache2"
    chef.add_recipe "apache2::mod_php5"
    chef.add_recipe "apache2::mod_rewrite"
    chef.add_recipe "mysql"
    chef.add_recipe "mysql::server"
    chef.add_recipe "database"
    chef.add_recipe "precise64-lamp"
    chef.json = {
      :build_essential => {
        :compiletime => true
      },
      :mysql => {
        :allow_remote_root => true,
        :server_root_password => 'password',
        :server_debian_password => 'password',
        :server_repl_password => 'password'
      },
      :apache => {
        :user => 'vagrant',
        :group => 'vagrant',
        :default_site_enabled => true
      },
      :php => {
        :directives => {
          :upload_max_filesize => "128M",
          :post_max_size => "128M"  
        }
      }
    }
  end
end
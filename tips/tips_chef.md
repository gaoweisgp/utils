* chef-apply <file.rb> 
  Run the resources in file.rb. But it doesn't know how to apply cookbooks.
  That's done by chef-client

* mkdir chef/cookbooks
* cd chef/cookbooks
* chef generate cookbooks workstation
* chef generate cookbooks apache
* chef generate recipe apache server

* Run chef-client in --local-mode
  __cd cookbooks directory__
  __sudo chef-client --local-mode -r "recipe[apache::server]"__

* Run multiple recipes
  __sudo chef-client --local-mode -r "recipe[workstation::setup],recipe[apache::server]"__

* Run the default recipe from a cookbook
  __sudo chef-client --local-mode -r "recipe[COOKBOOK(::default)]"__

* Include recipe include_recipe
  **include_recipe 'apache::server'**

* Under cookbooks/<cookbook>/recipes/default.rb you can include_recipe


## Test Kitchen
* 4 stages of test kitchen
  1. kitchen create
  2. kitchen converge
  3. kitchen verify
  4. kitchen destroy

* Test are in cookbooks/<cookbook>/test/integration/default/serverspec/default_spec.sh

* Download chef-server from chef.io

**Use the link to setup the chef-server**

https://docs.chef.io/release/server_12-6/install_server.html#standalone

* chef-server-ctl reconfigure
  * This will take some time as it re-configures the server
* sudo chef-server-ctl user-create chef CHEF Automation chef@kellynoah.com 'PASSWORD' --filename /users/chef/chef.pem
* sudo chef-server-ctl org-create larrymasc 'Larry Mascarenhas' --association_user chef --filename larrymasc-validator.pem
   * NOTE: Uppercase in org name is not supported

**Install additional packages from https://packages.chef.io**
* sudo chef-server-ctl install chef-manage
* sudo chef-server-ctl reconfigure
* sudo chef-manage-ctl reconfigure --accept-license

**Install the Opscode Jobs Push Server**
**It allows you to push jobs independant of the chef-client run**
* Download from https://downloads.chef.io/push-jobs-server/ubuntu/
* sudo dpkg -i opscode-push-jobs-server_1.1.6-1_amd64.deb
* sudo chef-server-ctl install opscode-push-jobs-server
* sudo chef-server-ctl reconfigure
* sudo opscode-push-jobs-server-ctl reconfigure
* 

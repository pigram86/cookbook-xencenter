# xencenter cookbook
This cookbook installs XenCenter 6.2

# Requirements
This cookbook depends on the 'windows' cookbook

# Usage
Use this cookbook as a standalone run or as part of a role

# Attributes
The following attributes exist:
default[:xc][:url] - source
default[:xc][:file] - installed location for not-if

# Recipes
xencenter::default
# install xencenter 6.2
windows_package "xencenter" do 
  source node[:xc][:url]
  action :install
  not_if {::File.exists?(node[:xc][:file])}
  not_if {reboot_pending?}
end

# reboot if reboot_pending
windows_reboot 60 do
  reason 'reboot needed'
  only_if {reboot_pending?}
end 

# Author

Author:: Todd Pigram (<todd@toddpigram.com>)

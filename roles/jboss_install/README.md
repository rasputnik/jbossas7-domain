This is a 'base role' for jboss DCs and HCs.

It handles common elements like

* jboss install
* very basic config (jboss_home, console.log etc)
* log directories
* system account

More useful roles should add this as a dependency
and then use their own tasks/vars to

* write their own init scripts
* set their own configs

vars from this role should be visible to dependants;
see defaults/main.yml for a list.

**important:** to work well you should define a 'bounce jboss'
handler that will be called when e.g. RPMs upgrade.

# OpenShift Ruby Cartridge
This cartridge is documented in the [Cartridge Guide](http://openshift.github.io/documentation/oo_cartridge_guide.html#ruby).

# Modification Guide

- Installed RVM Multi-User from sys-admin: `curl -sSL https://get.rvm.io | sudo bash -s stable`
- sudo usermod -a -G rvm sys-admin
- rvm list known
- rvm install 2.1.2
- gem install passenger bundler rake
- passenger-install-apache2-module

`````
   LoadModule passenger_module /usr/local/rvm/gems/ruby-2.0.0-p481/gems/passenger-4.0.48/buildout/apache2/mod_passenger.so
   <IfModule mod_passenger.c>
     PassengerRoot /usr/local/rvm/gems/ruby-2.0.0-p481/gems/passenger-4.0.48
     PassengerDefaultRuby /usr/local/rvm/gems/ruby-2.0.0-p481/wrappers/ruby
   </IfModule>
`````

# Cartridge Update

`````
cd /usr/libexec/openshift/cartridges/ruby
git fetch
git reset --hard origin/master
oo-admin-cartridge -a install -s .
oo-admin-ctl-cartridge -c import-node --activate
oo-admin-ctl-cartridge -c migrate
oo-admin-ctl-cartridge -c deactivate --name OLD_VERSION
oo-admin-ctl-cartridge -c clean
oo-admin-upgrade upgrade-node --version NEW_VERSION
`````

# Passenger Update

- rvm use 2.1.2
- gem update passenger
- passenger-install-apache2-module

`````
cd /var/lib/openshift
sudo find . -name 'openshift.conf' -exec sed -i 's/4\.0\.50/4\.0\.53/' '{}' \;
sudo find . -name 'PASSENGER_*' -exec sed -i 's/4\.0\.50/4\.0\.53/' '{}' \;
`````

Then restart all Ruby gears.

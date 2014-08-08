# OpenShift Ruby Cartridge
This cartridge is documented in the [Cartridge Guide](http://openshift.github.io/documentation/oo_cartridge_guide.html#ruby).

# Modification Guide

- Installed RVM Multi-User from sys-admin: `curl -sSL https://get.rvm.io | sudo bash -s stable`
- sudo usermod -a -G rvm sys-admin
- rvm list known
- rvm install 2.0
- gem install passenger
- passenger-install-apache2-module

`````
   LoadModule passenger_module /usr/local/rvm/gems/ruby-2.0.0-p481/gems/passenger-4.0.48/buildout/apache2/mod_passenger.so
   <IfModule mod_passenger.c>
     PassengerRoot /usr/local/rvm/gems/ruby-2.0.0-p481/gems/passenger-4.0.48
     PassengerDefaultRuby /usr/local/rvm/gems/ruby-2.0.0-p481/wrappers/ruby
   </IfModule>
`````

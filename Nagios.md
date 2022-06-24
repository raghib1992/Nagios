# Pre-requisite
## apache php  gcc compiler and gd development libraries

```
yum install http php -y
yum install -y gcc glibc glibc-common
yum install -y gd gd-devel
```
# Create User
```
useradd -m nagios
passwd nagios
groupadd nagioscmd
usermod -aG nagioscmd nagios
usermod -aG nagioscmd apache
```
# Nagios download core and plugins, Create a directory for storing downaload
```
mkdir ~/download
cd ~/download
```
# Dowanload the source code tarballs of both nagios and nagios plugin
```
wget https://sourceforge.net/projects/nagios/files/nagios-4.x/nagios-4.0.8/nagios-4.0.8.tar.gz
wget http://nagios-plugins.org/download/nagios-plugins-2.0.3.tar.gz
```
# Compile and install Nagios extract the nagios source code 
```
tar xzvf nagios-4.0.8.tar.gz
cd nagios-4.0.8
```
# run configuration script with the name of the group
```
./configure --with-command-group=nagioscmd
```
# compile
```
make all
```
# Install binaries 
```
make install
make install-init
make install-config
make install-commandmode
```
# configure web interface
```
make install-webconf
```
# Create a nagiosadmin account for login into the nagios web interface 
```
htpasswd -c /usr/local/nagios/etc/htpassword.users
```
## set password 
# start service
```
service httpd restart
```
*************************************************************
# Compile and install the nagios plugins. Extract the Nagios plugins source code tarball
```
cd ~/downlaod 
tar zxvf nagios-plugins-2.0.3.tar.gz
cd nagios-plugins-2.0.3
```
# Compile and Install the plugins
```
./configure --with-nagios-user=nagios --with-nagios-group=nagios
make
make install
```
# start nagios
```
chkconfig --add nagios
chkconfig nagios on
```
# verify the sample nagios conf file
```
/usr/local/nagios/bin/nagios -v /usr/local/nagios/etc/nagios.cfg
```
# If no errors, start nagios
```
service nagios start 
service httpd start
```
# Copy public ip and paste into browser
```
http://192.168.10.11/nagios/
username nagiosadmin
password admin123
```
# security-group
```
22
80
```
# How to install Softaculous in ISPConfig 3 on Ubuntu 16.04

Related Blog Post is here: https://www.georgenicolaou.me/add-softaculous-ispconfig3-ubuntu-16-04/



I installed Softaculous on ISPConfig 3 so I thought I would post this. Assuming you are root if not do sudo su and enter your password before issuing these commands

For 64Bit x86_64 Linux:

1. cd /tmp
2. wget http://downloads3.ioncube.com/loader_downloads/ioncube_loaders_lin_x86-64.tar.gz
3. tar xfz ioncube_loaders_lin_x86-64.tar.gz

For 32Bit i386 Linux:

1. cd /tmp
2. wget http://downloads3.ioncube.com/loader_downloads/ioncube_loaders_lin_x86.tar.gz
3. tar xfz ioncube_loaders_lin_x86.tar.gz

Then type

php -v it should show something like

7.0.xxx that's fine

Now type php -i | grep extension_dir

You should get

extension_dir => /usr/lib/php/20151012 => /usr/lib/php/20151012 if this looks different the next command need too reflect that difference

So now do

cp /tmp/ioncube/ioncube_loader_lin_7.0.so /usr/lib/php/20151012

Now for Apache mod_php do

nano /etc/php/7.0/apache2/php.ini and after the [PHP] in the first line add zend_extension = /usr/lib/php/20151012/ioncube_loader_lin_7.0.so

Now for Command line PHP (CLI) do

nano /etc/php/7.0/cli/php.ini and after the [PHP] in the first line add zend_extension = /usr/lib/php/20151012/ioncube_loader_lin_7.0.so

Now for PHP CGI (used for CGI and Fast_CGI modes) do

nano /etc/php/7.0/cgi/php.ini and after the [PHP] in the first line add zend_extension = /usr/lib/php/20151012/ioncube_loader_lin_7.0.so

Now for PHP FPM do

nano /etc/php/7.0/fpm/php.ini and after the [PHP] in the first line add zend_extension = /usr/lib/php/20151012/ioncube_loader_lin_7.0.so

Now do these in sequence

1. service apache2 restart
2. service php7.0-fpm restart
If you have now errors/warnings do

php -v
You should see something like

PHP 7.0.22-0ubuntu0.16.04.1 (cli) ( NTS )
Copyright (c) 1997-2017 The PHP Group
Zend Engine v3.0.0, Copyright (c) 1998-2017 Zend Technologies
with the ionCube PHP Loader (enabled) + Intrusion Protection from ioncube24.com (unconfigured) v10.0.0 (), Copyright (c) 2002-2017, by ionCube Ltd.
with Zend OPcache v7.0.22-0ubuntu0.16.04.1, Copyright (c) 1999-2017, by Zend Technologies

If you like to test the PHP of a website, create an "info.php file with this content:

<?php
phpinfo();
?>

This should also show that Ioncube is installed etc.

So now you need to go into ISPConfig3--->System-->Remote Users add a username and password tick all the boxes that are available

When you are done go to your ssh windows as root and do

1. wget -N http://files.softaculous.com/install.sh
2. chmod 755 install.sh
3. ./install.sh
It will ask for a username and password. Use the data you added to ISPConfig3 when you create your remore user in the previous step.

Let the script finish and you should be good to go. You can find Softuculous under ISPConfig3-->Tools->Softaculous

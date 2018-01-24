# Mosquitto-Library-Module-Installation-in-PHP
Installing the Mosquitto PHP library module on Raspberry Pi



To connect to Mosquitto MQTT broker from your PHP code, you need to have the Mosquitto PHP library module enabled on your server. This post explains steps to get the Mosquitto PHP library installed.

These steps have been verified on Ubuntu desktop as well as on RaspberryPi (Raspbian), running Apache2 and PHP 7 ( Lastest Version released)
You need to be connected to internet to complete these steps.

Follow them in the order given.


1. sudo apt-get install php-pear
2. sudo apt-get install php-dev
3. sudo apt-get install libmosquitto-dev
4. sudo pecl install Mosquitto-alpha


NOTE: In step 4, you will be prompted to add “extension=mosquitto.so” to php.ini. This message is misleading. Actually, you need to create mosquitto.ini file in the mods-available directory and then enable the module with php.
Follow below steps (6-10) to achieve this:-


5. sudo su
6. cd /etc/php/mods-available  (Go to mods-available directory).


7. Create file: “mosquitto.ini” using any text editor like vi and add following line:

extension=mosquitto.so

Save the file and quit the editor.

8. Check if the library is installed using dpkg

dpkg -l | grep mosquitto

You will get a result similar to the one given below. You must see mosquitto library listed.

oot@pi:/etc/php/mods-available# dpkg -l | grep mosquitto
ii  libmosquitto-dev                              1.3.4-2+deb8u1                             all          MQTT version 3.1 client library, development files
ii  libmosquitto1                                 1.3.4-2+deb8u1                             armhf        MQTT version 3.1 client library
ii  mosquitto                                     1.3.4-2+deb8u1                             armhf        MQTT version 3.1/3.1.1 compatible message broker
ii  mosquitto-clients                             1.3.4-2+deb8u1                             armhf        Mosquitto command line MQTT clients
ii  python-mosquitto                              1.3.4-2+deb8u1                             all          MQTT version 3.1 Python client library

9. Now enable the mosquitto module

sudo phpenmod mosquitto


10. Restart apache server :-

sudo service apache2 restart


NOTE: Sometimes, you may get a warning as below. If this happens, just restart the computer.

root@pi:/etc/php/mods-available# sudo service apache2 restart
Warning: Unit file of apache2.service changed on disk, 'systemctl daemon-reload' recommended.

11. Using a text editor, create “phpinfo.php” file inside “/var/www/html” directory (default web root for apache server)
Insert the following line into “phpinfo.php”, save and quit the text editor:-

 <?php phpinfo(); ?>
 
 12. Open your browser and navigate to http://localhost/phpinfo.php
You must see mosquitto module listed among the php modules

Once you complete all these steps, you must have your mosquitto php library ready.


Good Luck !!!


Odilon HEMA NGONGO

FullStack Developper 


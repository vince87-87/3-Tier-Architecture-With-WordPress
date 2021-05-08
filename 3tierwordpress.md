# 3 Tier Architecture With WordPress
# Setup Web Server
# Provision Web Server using red hat ami

![image](https://user-images.githubusercontent.com/49937302/117527959-5bb5db00-b002-11eb-9a2a-74287c3d896d.png)

# Create 3 volume of 10GB & attached to web server
 
![image](https://user-images.githubusercontent.com/49937302/117527970-63757f80-b002-11eb-91ac-9088bd44b63a.png)

![image](https://user-images.githubusercontent.com/49937302/117527973-6a03f700-b002-11eb-9261-0f0d4a3d6840.png)

![image](https://user-images.githubusercontent.com/49937302/117527975-6e301480-b002-11eb-99e1-e29311a84802.png)

# Checked that ebs is attached on the os & existing volume free space
 
![image](https://user-images.githubusercontent.com/49937302/117527978-74be8c00-b002-11eb-823a-ec0ac8cb9ee5.png)

# Create 3 partition 

![image](https://user-images.githubusercontent.com/49937302/117527982-7c7e3080-b002-11eb-9c4a-fed48dcbda73.png)

# To view newly created partition using lsblk

![image](https://user-images.githubusercontent.com/49937302/117527985-830ca800-b002-11eb-8a2b-0b064c11c239.png)

# install lvm2 and check for available partition using  “lvmdiskscan” command

![image](https://user-images.githubusercontent.com/49937302/117527991-8acc4c80-b002-11eb-9c6d-6f513b927052.png)

![image](https://user-images.githubusercontent.com/49937302/117528000-9a4b9580-b002-11eb-9b26-4553b82f61b4.png)

# marked 3 disk as physical volume & verify pv have been created
 
![image](https://user-images.githubusercontent.com/49937302/117528010-a46d9400-b002-11eb-97d4-90a185f57ba1.png)

# create volume group and verify its has been created

![image](https://user-images.githubusercontent.com/49937302/117528012-a899b180-b002-11eb-932d-5c3e781ab6ca.png)

# create 2 logical volume-> apps , logs and verify lv created

![image](https://user-images.githubusercontent.com/49937302/117528028-bb13eb00-b002-11eb-9a4d-cc1ec4f3415a.png)


# verify the entire setup

![image](https://user-images.githubusercontent.com/49937302/117528032-c36c2600-b002-11eb-8cee-e481f255be51.png)

# format physical volume to ext4 filesystem

![image](https://user-images.githubusercontent.com/49937302/117528039-cbc46100-b002-11eb-9d6f-a57097293d08.png)

# create 2 directory to store websites file and backup log files
 
![image](https://user-images.githubusercontent.com/49937302/117528045-d0891500-b002-11eb-8e5d-801c37ea44e4.png)

# Mount /var/www/html on apps-lv 

![image](https://user-images.githubusercontent.com/49937302/117528052-d7178c80-b002-11eb-86ad-11d896dd1267.png)

# Use rsync utility to backup all the files in the log directory /var/log into /home/recovery/logs 
sudo rsync -av /var/log/. /home/recovery/logs/

![image](https://user-images.githubusercontent.com/49937302/117528059-de3e9a80-b002-11eb-993d-8535af92c2cb.png)

# Mount /var/log on logs-lv 

![image](https://user-images.githubusercontent.com/49937302/117528064-e4cd1200-b002-11eb-9ac9-02269ad6261e.png)

# restore log file to /var/log
 
![image](https://user-images.githubusercontent.com/49937302/117528071-eac2f300-b002-11eb-8b16-327bc7025a68.png)

# update /etc/fstab to persist mount after reboot
 
![image](https://user-images.githubusercontent.com/49937302/117528073-f0b8d400-b002-11eb-9448-637417963082.png)

![image](https://user-images.githubusercontent.com/49937302/117528080-fb736900-b002-11eb-952a-3741c95bb0b9.png)

# test configuration & reload daemon

![image](https://user-images.githubusercontent.com/49937302/117528085-01694a00-b003-11eb-9bf4-f73ff1dd3bfa.png)

# Setup Database Server
# Launch new Instance for db servers

![image](https://user-images.githubusercontent.com/49937302/117528092-0928ee80-b003-11eb-9bf6-a74903e2f7c3.png)

# Create 3 volume , attached each volume to db server and verify on db server
 
![image](https://user-images.githubusercontent.com/49937302/117528112-1e9e1880-b003-11eb-85e7-855c97d4c11a.png)
 
![image](https://user-images.githubusercontent.com/49937302/117528116-26f65380-b003-11eb-9030-eef70a988b6b.png)

![image](https://user-images.githubusercontent.com/49937302/117528142-3fff0480-b003-11eb-8523-a2f6a7d0a4b2.png)

# create partition for each volume using gdisk
 
![image](https://user-images.githubusercontent.com/49937302/117528149-48efd600-b003-11eb-9d5d-d387fa5362b6.png)
 
# change to physical volume

![image](https://user-images.githubusercontent.com/49937302/117528154-55742e80-b003-11eb-854c-a859975a3d8a.png)


# Create volume group

![image](https://user-images.githubusercontent.com/49937302/117528160-5dcc6980-b003-11eb-9398-914c249f5a9a.png)
 
# create logical volume

![image](https://user-images.githubusercontent.com/49937302/117528166-64f37780-b003-11eb-863e-aa6cb65feb7e.png)


# format physical volume to ext4
 
![image](https://user-images.githubusercontent.com/49937302/117528169-69b82b80-b003-11eb-82a6-a1445cbc0075.png)

# create 2 directory for db , logs file & mount /db to db-lv 

![image](https://user-images.githubusercontent.com/49937302/117528175-72106680-b003-11eb-9194-239cf907169d.png)


# Use rsync utility to backup all the files in the log directory /var/log into /home/recovery/logs

![image](https://user-images.githubusercontent.com/49937302/117528182-78064780-b003-11eb-82bd-7c9161e71057.png)


# Mount /var/log on logs-lv 

![image](https://user-images.githubusercontent.com/49937302/117528185-7d639200-b003-11eb-8c86-7ab74ab2f1ca.png)

# restore log file to /var/log

![image](https://user-images.githubusercontent.com/49937302/117528196-88b6bd80-b003-11eb-8ff8-7e568dad6dbc.png)


# update /etc/fstab to persist mount after reboot
 
![image](https://user-images.githubusercontent.com/49937302/117528201-8f453500-b003-11eb-9a80-46483615f79e.png)

![image](https://user-images.githubusercontent.com/49937302/117528212-9e2be780-b003-11eb-9b50-c80289cf4ec0.png)

# test configuration & reload daemon

![image](https://user-images.githubusercontent.com/49937302/117528218-a6842280-b003-11eb-8c14-397afb82e1a4.png)

# Install Wordpress on web server
# update the repo & install wget,httpd,php,php-mysqlnd,php-fpm,php-json
Sudo yum update -y
sudo yum -y install wget httpd php php-mysqlnd php-fpm php-json 

![image](https://user-images.githubusercontent.com/49937302/117528259-e814cd80-b003-11eb-9195-1f9ed471c5cd.png)

# Start apache

![image](https://user-images.githubusercontent.com/49937302/117528269-f19e3580-b003-11eb-876f-df82b2b5be3c.png)


# Install php
sudo yum install https://dl.fedoraproject.org/pub/epel/epel-release-latest-8.noarch.rpm

sudo yum install yum-utils http://rpms.remirepo.net/enterprise/remi-release-8.rpm

sudo yum module list php

sudo yum module reset php

sudo yum module enable php:remi-7.4

sudo yum install php php-opcache php-gd php-curl php-mysqlnd

sudo systemctl start php-fpm

sudo systemctl enable php-fpm

sudo setsebool -P httpd_execmem 1
 
![image](https://user-images.githubusercontent.com/49937302/117528276-f82cad00-b003-11eb-99fe-f29f3f67ba4d.png)


# restart apache service 

![image](https://user-images.githubusercontent.com/49937302/117528289-02e74200-b004-11eb-9a2a-87e90642f7d1.png)


# download wordpress and cp wordpress to var/www.html
mkdir wordpress

cd   wordpress

sudo wget http://wordpress.org/latest.tar.gz

sudo tar xzvf latest.tar.gz

sudo rm -rf latest.tar.gz

sudo cp wordpress/wp-config-sample.php wordpress/wp-config.php

sudo cp -R wordpress /var/www/html/

![image](https://user-images.githubusercontent.com/49937302/117528292-08dd2300-b004-11eb-80c1-55aa1df90818.png)


# configure SELINUX policies
sudo chown -R apache:apache /var/www/html/wordpress

#change file selinux security contest

sudo chcon -t httpd_sys_rw_content_t /var/www/html/wordpress -R 

sudo setsebool -P httpd_can_network_connect=1
 
![image](https://user-images.githubusercontent.com/49937302/117528299-11cdf480-b004-11eb-9575-dd2af7ddf212.png)


# Install mysql on DB Server
# update repo & install mysql

![image](https://user-images.githubusercontent.com/49937302/117528302-185c6c00-b004-11eb-9882-ec0dc3c56a6d.png)


# verify mysql service is running

![image](https://user-images.githubusercontent.com/49937302/117528305-1db9b680-b004-11eb-8779-b59c591ba09d.png)


# Configure DB to work with wordpress
sudo mysql

CREATE DATABASE wordpress;

CREATE USER `vincent`@`172.31.19.26` IDENTIFIED BY 'mypass';

GRANT ALL ON wordpress.* TO 'vincent'@'172.31.19.26';

FLUSH PRIVILEGES;

SHOW DATABASES;

Exit

![image](https://user-images.githubusercontent.com/49937302/117528309-24482e00-b004-11eb-8e47-3ea62a8c5e1b.png)

![image](https://user-images.githubusercontent.com/49937302/117528319-2d38ff80-b004-11eb-8bf9-278b05bed3dd.png)


# Configure WordPress to connect to remote database



# allow port 3306 on security group of the db server

![image](https://user-images.githubusercontent.com/49937302/117528320-332ee080-b004-11eb-8783-f1dda26b014c.png)


# install mysql on web server

![image](https://user-images.githubusercontent.com/49937302/117528325-37f39480-b004-11eb-9a42-84aae848a02a.png)

# configure wp-config.php
Cd /var/www/html/wordpress
Change the db connection detail under wp-config.php

![image](https://user-images.githubusercontent.com/49937302/117528330-404bcf80-b004-11eb-97da-2c98e284849c.png)


# Restart apache

![image](https://user-images.githubusercontent.com/49937302/117528338-4641b080-b004-11eb-922e-9d9d8505bd51.png)


# Verify can connect to db server
Sudo mysql -u vincent -p -h 172.31.27.38

![image](https://user-images.githubusercontent.com/49937302/117528345-4b9efb00-b004-11eb-8578-82cc1af76832.png)


# allow any ip to port 80 on security group of the web server and access the web server from the internet
 
 ![image](https://user-images.githubusercontent.com/49937302/117528349-4fcb1880-b004-11eb-9a8f-0366c4bf60ee.png)

![image](https://user-images.githubusercontent.com/49937302/117528355-578abd00-b004-11eb-9792-2c37e6e6bf21.png)

![image](https://user-images.githubusercontent.com/49937302/117528358-5bb6da80-b004-11eb-9815-4e528abca0b6.png)

![image](https://user-images.githubusercontent.com/49937302/117528362-5f4a6180-b004-11eb-930e-3b23e8341df7.png)






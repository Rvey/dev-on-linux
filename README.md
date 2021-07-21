#   Setup a development environment on  POP OS (Laravel , VueJs)


## grub for Dual boot Pop os and win

#### partition

| file Sys | space | name |
| :---: | :---: | :---: |
| fat32 | 800MiB | bootEfi |
| ext4 | as you please | root(/) |
| linux-swap | 4GiB | swap |


#### update the system 
```sudo apt update && sudo apt upgrade``` 
#### install grub 
`sudo apt install grub-efi grub2-common grub-customizer`
#### install grub bootloader 
``` sudo grub-install```
output > `no error reported`

#### copy the grub efi to the pop folder 
```
sudo cp /boot/grub/x86_64-efi/grub.efi /boot/efi/EFI/pop/grubx64.efi
```
#### run grub-customiser 

`File` > `change Environment` > OUTPUT_FILE : `/boot/efi/EFI/pop/grub.cfg` > `Apply` > `Save`


##### Reboot


# Setup VueJS and Laravel in Popos/ Ubuntu 


## VueJS

### NodeJs 



####  via official repo
https://github.com/nodesource/distributions#debinstall

####  via snaps 
https://github.com/nodejs/snap

#### via PPA
```curl -sL https://deb.nodesource.com/setup_14.x -o nodesource_setup.sh```

#### check the installation 
`node -v`
`npm -v`

### install Vue CLI

```
sudo npm i  @vue/cli -g
```

#### verify 
```
vue --version
```

#### create vue project 
```
vue create ae > cd ae > npm run serve 
```
Output > 
```
    App running at:
    - Local: http://localhost:8080/
    - Network: http://192.168.0.106:8080/

    Note that the development build is not optimized.
    To create a production build, run npm run build.
```

## Laravel 

### PHP 8 

#### Enabling PHP Repository 

```
sudo apt install software-properties-common
sudo add-apt-repository ppa:ondrej/php
```
#### installing PHP 8 with Apache


```
sudo apt update

sudo apt install php8.0 libapache2-mod-php8.0
```

#### restart Apache for the PHP module tp get loaded 
```
sudo systemctl restart apache2
```

#### Test 
```
php -v
```
output `PHP 8.0.8 (cli) (built: Jul  1 2021 15:27:21) ( NTS )
Copyright (c) The PHP Group
Zend Engine v4.0.8, Copyright (c) Zend Technologies
    with Zend OPcache v8.0.8, Copyright (c), by Zend Technologies
`

### Composer 
Download and install Composer

```cd ~
curl -sS https://getcomposer.org/installer -o composer-setup.php
```
check the downloaded installer match the latest hash code ckeck here  https://composer.github.io/pubkeys.html

```
HASH=`curl -sS https://composer.github.io/installer.sig`

```
## Test 
```
php -r "if (hash_file('SHA384', 'composer-setup.php') === '$HASH') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;"

```

Output  > 
`Installer verified`

this command gonna install composer as sys command `composer`

```
sudo php composer-setup.php --install-dir=/usr/local/bin --filename=composer

```

output > `All settings correct for using Composer
Downloading... 
Composer (version 1.10.5) successfully installed to: /usr/local/bin/composer
Use it: php /usr/local/bin/composer`

### check ur installation  
```
$ composer 
```


## MySQL

### install 

```
sudo apt install mysql-server

```

### configuring Mysql
```
sudo mysql_secure_installation

```
follow the instruction 

#### change the hashed password to password we can acess (nukers hash the first password as you will see when execute the command  so now we need to alter it with a new one)


```
sudo mysql
```

```
select user, authentication_string, plugin from mysql.user;
```
```
Alter USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password by 'YOUR_PASSWORD123';
```
### CONFIRM
``` 
FLUSH PRIVILEGES; 
```

mysql>`quit`

### TEST
```
sudo mysql -u root -p
```
output > `Enter password : 'YOUR_PASSWORD'` 
output > ``` Welcom to the mysql ... ```

### Enable `pdo_mysql` extension

```
sudo apt install php-mysql
```
### then restart apache2 : 

```
sudo systemctl restart apache2
```

## Usefull links 
### https://github.com/erik1066/pop-os-setup

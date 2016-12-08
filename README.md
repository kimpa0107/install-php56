# Ubuntu 14.04 编译安装php5.6

### 0. 预装软件
```bash
sudo apt-get update

sudo apt-get install libxml2-dev
sudo apt-get install libjpeg-dev
sudo apt-get install libpng12-dev
sudo apt-get install libfreetype6-dev
sudo apt-get install libcurl4-openssl-dev
```
![安装libxml2-dev](./images/libxml2-dev.png)

![安装libjpeg-dev](./images/libjpeg-dev.png)

![安装libpng12-dev](./images/libpng12-dev.png)

![安装libfreetype6-dev](./images/libfreetype6-dev.png)


### 1. 下载PHP5.6.28源码
```bash
wget http://cn2.php.net/distributions/php-5.6.28.tar.gz
```

![下载PHP5.6源码](./images/download_php5.6.png)

### 2. 解压并安装

- 安装路径：`/usr/local/php`

    ```bash
    tar -zxf php-5.6.28.tar.gz
    cd php-5.6.28
    ./configure --prefix=/usr/local/php --with-config-file-path=/usr/local/php --enable-mbstring --enable-ftp --with-gd --with-jpeg-dir=/usr --with-png-dir=/usr --with-mysql=mysqlnd --with-mysqli=mysqlnd --with-openssl-dir=/usr --with-openssl --with-pdo-mysql=mysqlnd --with-pear --enable-sockets --with-freetype-dir=/usr --enable-gd-native-ttf --with-zlib --with-libxml-dir=/usr --with-xmlrpc --enable-zip --enable-fpm --enable-fpm --enable-xml --enable-sockets --with-gd --with-zlib --with-iconv --enable-zip --with-freetype-dir=/usr/lib/ --enable-soap --enable-pcntl --enable-cli
    ```

![编译](./images/configure_php5.6.png)

![编译结果](./images/configure_result.png)

![安装](./images/install.png)

![安装结果](./images/install_result.png)


### 3. 配置

- 复制PHP.INI文件(在PHP源码根目录下)
    ```bash
    sudo cp ./php.ini-development /usr/local/php/

    vim /usr/local/php/php.ini
    include_path = /usr/local/php/lib/php
    ```

- 复制启动脚本(在PHP源码根目录下)：
	```bash
	sudo cp ./sapi/fpm/init.d.php-fpm /etc/init.d/php-fpm
	sudo chmod+x /etc/init.d/php-fpm
	```

- 复制PHP-FPM配置文件：
	```bash
	cd /usr/local/php/etc
	sudo cp php-fpm.conf.default php-fpm.conf
	sudo mv php-fpm.conf.default php-fpm.conf.default.bak
	```

- 配置PHP-FPM文件

    ```bash
    vim php-fpm.conf

    pid = run/php-fpm.pid
    pm.max_children = 5
    pm.start_servers = 2
    pm.min_spare_servers = 1
    pm.max_spare_servers = 3

    ```

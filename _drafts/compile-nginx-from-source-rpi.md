Up at top... kill apache2!
sudo apt-get remove apache2 && sudo apt-get autoremove

Continued... nginx compile from source

sudo make install

Since we didn't change any options, the install defaults to /usr/local/nginx (fine with us)

Check the nginx version, and the configure options you selected. (Note the -V switch is good to check later what options you used to compile)

vholowiski@vpi:~/nginx_compile/nginx-1.14.0 $ sudo /usr/local/nginx/sbin/nginx -v
nginx version: nginx/1.14.0
vholowiski@vpi:~/nginx_compile/nginx-1.14.0 $ sudo /usr/local/nginx/sbin/nginx -V
nginx version: nginx/1.14.0
built by gcc 6.3.0 20170516 (Raspbian 6.3.0-18+rpi1+deb9u1)
built with OpenSSL 1.1.0h  27 Mar 2018
TLS SNI support enabled
configure arguments: --user=nginx --group=nginx --with-http_ssl_module --with-http_realip_module --with-openssl=../openssl-1.1.0h --with-openssl-opt=enable-ec_nistp_64_gcc_128 --with-openssl-opt=no-nextprotoneg --with-openssl-opt=no-weak-ssl-ciphers --with-openssl-opt=no-ssl3 --with-pcre=../pcre-8.42 --with-pcre-jit --with-zlib=../zlib-1.2.11 --with-http_gunzip_module --with-http_gzip_static_module

Now create the nginx user:
sudo useradd -s /bin/false nginx
false means it can't log in

Test the configuration (should be fine we haven't deleted anything yet)
vholowiski@vpi:~/nginx_compile/nginx-1.14.0 $ sudo /usr/local/nginx/sbin/nginx -t
nginx: the configuration file /usr/local/nginx/conf/nginx.conf syntax is ok
nginx: configuration file /usr/local/nginx/conf/nginx.conf test is successful

Create a systemd service file
sudo vim /etc/systemd/system/nginx.service

[Unit]
Description=A high performance web server and a reverse proxy server
After=network.target

[Service]
Type=forking
PIDFile=/usr/local/nginx/logs/nginx.pid
ExecStartPre=/usr/local/nginx/sbin/nginx -t -q -g 'daemon on; master_process on;'
ExecStart=/usr/local/nginx/sbin/nginx -g 'daemon on; master_process on;'
ExecReload=/usr/local/nginx/sbin/nginx -g 'daemon on; master_process on;' -s reload
ExecStop=-/sbin/start-stop-daemon --quiet --stop --retry QUIT/5 --pidfile /usr/local/nginx/logs/nginx.pid
TimeoutStopSec=5
KillMode=mixed

[Install]
WantedBy=multi-user.target

Start and enable NGINX service:

sudo systemctl start nginx.service && sudo systemctl enable nginx.service

Now, if you don't have any firewall enabled you should be able to go to your pi's ip address in your web browser and get welcome to nginx spash screen


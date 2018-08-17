install requirements
sudo apt-get install libmysqlclient-dev libxml2-dev libevent-dev build-essential php-gd php-bcmath php-xml php-mbstring php-gettext php-mysql libpcre3 libcurl4-openssl-dev fping 
Download the latest zabbix file from https://www.zabbix.com/download_sources
cd ~
mkdir zabbix_compile
cd zabbix_compile
Somehow get the downloaded file here!
tar -zxvf *.gz
sudo groupadd --system zabbix

do stuff until configure
./configure --enable-server --enable-agent --with-mysql --enable-ipv6 --with-libcurl --with-libxml2


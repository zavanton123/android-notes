### Proxy VS Reverse Proxy
### Proxy: 
- client makes request to the server via proxy server
- the server does not know who the client is

Benefits:
- Anonymity of clients
- Caching
- Blocking unwanted websites
- GeoFencing


### Reverse Proxy
- client makes request to the server via reverse proxy server
- the client does not know who the server is

Benefits:
- Load Balancing
- Isolated internal traffic
- Logging
- Canary Deployment



### NGINX vs Apache
- Apache is in 'prefork' mode
- synchronous







# Install Nginx on Ubuntu via apt
sudo su
apt-get update
apt-get install nginx -y

### check the folder with configuration
ls -la /etc/nginx

### apt package automatically starts nginx
### check nginx is running
ps aux | grep nginx

### now the page is available at
http://public-ip-here:80










# Install on CentOS via yum
yum install -y epel-release
yum install -y nginx

### check the folder with configuration
ls -la /etc/nginx

### yum package does not automatically start nginx
### check nginx is not running
ps aux | grep nginx

### start the nginx
service nginx start














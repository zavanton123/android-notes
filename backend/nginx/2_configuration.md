# NGINX Configuration

### Main terminology:
- Context (i.e. scope that contains directives)
- Directive (key value pairs)





## Set up a basic virtual host
```
mkdir -p /sites/demo
```

### Add the files
### index.html
```
<html>
<head>
  <title>Hello</title>
  <link rel="stylesheet" href="style.css" type="text/css" />
</head>
<body>
  <h1>Hello world</h1>
</body>
</html>
```

### style.css
```
h1 {
  color: red;
}
```

### Update the configuration file:
### /etc/nginx/nginx.conf
```
events {}

http {

  include mime.types

  server {
    listen 80;
    server_name 54.93.123.207;

    root /sites/demo;
  }
}
```

### Check if the updated config is ok
```
nginx -t
```

### Check the type of style.css returned by nginx
### Note: it should be 'text/css', because we have loaded the 'mime.types'
```
curl -I http://54.93.123.207/style.css
```

### reload nginx to enable the new configuration
```
sudo systemctl reload nginx
```












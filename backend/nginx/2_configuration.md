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





## Location Blocks
### make a custom location '/greet' that returns a string
### reload the nginx for the new config to take effect (sudo systemctl reload nginx)

```
events {}

http {

  include mime.types

  server {
    listen 80;
    server_name 54.93.123.207;

    root /sites/demo;

    location /greet {
      return 200 "hello from here...";
    } 
  }
}
```


### You can use prefix match
```
location /greet {
  return 200 "this is prefix match";
} 
```

### You can use exact match
```
location = /greet {
  return 200 "this is exact match";
} 
```

### You can use regex match
### Case Sensitive
```

location ~ /greet[0-9] {
  return 200 "this is regex match";
} 
```

### You can use regex match
### Case Insensitive
```

location ~* /greet[0-9] {
  return 200 "hello from here...";
} 
```

### You can use preferential prefix match
### (i.e. its priority is higher than regex priority)
```

location ^~ /Greet2 {
  return 200 "this is preferenctial prefix match";
} 
```


### Location matching priorities
- Exact match (i.e =)
- Preferential prefix match (i.e. ^~)
- REGEX match (i.e. ~ or ~*)
- prefix match







## Nginx Variables

### Some build-in variables
```
location /inspect {
  return 200 "$host - $uri - $args";
}
```

### You can extract arguments

```
location /inspect {
  return 200 "Age: $arg_age, name: $arg_name";
}
```


### Use conditionals
```
http {
  server {
    if ( $arg_apiKey != 1234 ) {
      return 401 "Incorrect API key";
    }
  }
}
```

### Create your own variables
```
http {
  server {
    set $weekend "No";

    if ( $date_local ~ "Saturday|Sunday" ) {
      set $weekend "Yes";
    }

    location /is_weekend {
      return 200 $weekend;
    }
  }
}
```









## Rewrites
- rewrite some-pattern some-URI
- return some-status some-URI

### redirect with 'return' statement
### client makes the first request
### then the client makes the second request
```
location /logo {
  return 307 /thumb.png;
}
```

### redirect with 'rewrite' statement
### client makes only one request
### the server redirects internally
```
http {
  server {
    rewrite ^/user/\w+ /greet;

    location /greet {
      return 200 "Greeting to user";
    }
  }
}
```


### with 'rewrite' we can capture the parts of the original path
```

http {
  server {
    rewrite ^/user/(\w+) /greet/$1;

    location /greet {
      return 200 "Greeting to user";
    }

    location = /greet/john {
      return 200 "Greeting to John";
    }
  }
}
```



















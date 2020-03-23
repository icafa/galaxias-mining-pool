## How to Run the Mining Pool Web UI 

Jan 2018

The Web UI (aka frontend) is a single-page Ember.js application that polls the pool API to render miner stats.

### Pre-requisites 

Install and configure the mining pool as instructed in InstallAndRun.md

Install nodejs. Author suggests using LTS version >= 4.x from https://github.com/nodesource/distributions or from your Linux distribution or simply install nodejs on Ubuntu Xenial 16.04.

### Edit UI Environment 

```
$ nano www/config/environment.js
```

#### For development/testing/localhost: 

* Change ENV.APP.ApiURL to match the domain name you will be viewing the web UI from.  (Example: 'http://localhost:8080/')

#### For Public Internet: 

* Change ApiURL to match your domain name and port

* Change HTTPHost to match your mining endpoint domain name

* Change StratumHost to match your stratum endpoint domain name

### Build the Web UI 

As root:

```
# npm install -g ember-cli
```

```
# npm install -g bower
```

As user:

```
$ cd www
```

```
$ npm install
```

```
$ bower install
```

```
$ ./build.sh
```

The output should say "Building" and then:

```
Built project successfully. Stored in "dist/".
File sizes
 - intl-.....
..
..
..
```

##### Run the Development Server (localhost) 

From www/ directory:

```
$ ember server --port 8082 --environment development
```

Now you can view your mining stats on http://localhost:8082/

**Don't use built-in web server in production.**

### Remotely Connect to Development Server as localhost 

Connecting to your server is beyond the scope of this project but here is a suggestion.  If you are running the mining pool on a VPS or other remote server but are not ready to expose it to the public internet, this SSH command may help:

```
$ ssh -N -L 8082:localhost:8082 -L 8080:localhost:8080 -L 49152:localhost:49152 username@hostname
```

This provides access to the following ports from the remote server:

8082: ember server development port
8080: stats API
49152: for livreload

If your configuration uses different ports, change your SSH command accordingly.


### Production / Public Web Access 

The ember server can be invoked in "development" or "production" mode but should not actually be used in production.  For production, use another web server.  Because sammy007 tests on nginx, that is what we have used here.  

#### Configuring nginx for the OOP 

1. Make sure /etc/nginx/nginx.conf includes the following line (usually set by default):

```
include /etc/nginx/sites-enabled/*;
```

2. Move or comment out values in /etc/nginx/sites-enabled/default.  Specifically, if you want to view your pool at the / location of your URL, you will want to make sure this line is not in the default file:

```
root /var/www/html;
```

Alternatively, you can delete /etc/nginx/sites-enabled/default or move it to /etc/nginx/default-config.

3. Create a new config file /etc/nginx/sites-enabled/miningpool and have it read as follows:

```
server {
        listen 80;
        listen [::]:80;

        server_name mypool.com;

        root /home/openethereumpool/open-ethereum-pool/www/dist;
        index index.html;

        location / {
               try_files $uri $uri/ =404;
        }
        
        location /api {
                proxy_pass http://api;
        }
}

upstream api {
    server 127.0.0.1:8080;
}
```

Change the "listen" port from "80" to another port if you prefer, change "mypool.com" to your pool's URL, and change "root /home/openethereumpool/open-ethereum-pool/www/dist" to match the actual location of the open-ethereum-pool/www/dist directory.

4. Restart nginx

```
service nginx restart
```

5. Make sure port 80 (or whichever port you configured above) is not firewalled.

6. View the OOP front end from your public website (ex: mysite.com).

##### Modifying the Front-end HTML/CSS 

To customize the front end, modify the files in www/app/templates.  Then return to www and re-run ./build.sh.

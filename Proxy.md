### Reverse Proxy ###
This is a configuration for an nginx reverse proxy on an apache web server.

*Before starting we must configure SELinux so it doesnt cause any behind the scenes errors by using this command*

`setsebool -P httpd_can_network_connect 1`

- First of all install the LAMP stack and using a virtualhost in this lab is optional.
- Edit the /etc/httpd/conf/httpd.conf config file to make the apache webserver work on any port for example 8080 and to listen to the 127.0.0.1:8080 socket
- Add index.html and index.php to the document root of the apache webserver for test purposes

*Now we are ready to install nginx and configure it*
- After installing nginx > head to /etc/nginx/nginx.conf file 
- Edit the user to apache 
- The following configurations part must be written in this context

```
    server {
        listen       80;
        server_name  192.168.234.132;

        # Load configuration files for the default server block.
        include /etc/nginx/default.d/*.conf;

        location / {
        root /var/www/amrsioufy1710.com/;
        proxy_pass http://127.0.0.1:8080/;
        proxy_redirect off;
        proxy_set_header Host $http_host;
        }
```
- server_name specifies the ip address of the nginx proxy
- proxy_pass simply tells nginx to forward requests to / to the server listening on http://127.0.0.1:8080. *port 8080 is for the apache. if we want to run an application at the same time to be connected to nginx we must use another port and add location and proxy_pass directives*
- root is our testing material from the apache webserver

lastly we need to create a config file in /etc/nginx/conf.d
```
# Proxy headers
proxy_set_header Upgrade           $http_upgrade;
proxy_set_header Connection        "upgrade";
proxy_set_header Host              $host;
proxy_set_header X-Real-IP         $remote_addr;
proxy_set_header X-Forwarded-For   $proxy_add_x_forwarded_for;
proxy_set_header X-Forwarded-Proto $scheme;
proxy_set_header X-Forwarded-Host  $host;
proxy_set_header X-Forwarded-Port  $server_port;

# Proxy timeouts
proxy_connect_timeout              60s;
proxy_send_timeout                 60s;
proxy_read_timeout                 60s;
```

- The above configs are just some adjustments to our proxy features
*Now we must reload and restart nginx and httpd*

*Using a browser or elinks we can test our reverse proxy by visitng http://localhost which will show the contents of the index.html working on the apache through the nginx*.

##### References #####
https://docs.nginx.com/nginx/admin-guide/web-server/reverse-proxy/
https://stackoverflow.com/questions/23948527/13-permission-denied-while-connecting-to-upstreamnginx
https://gist.github.com/soheilhy/8b94347ff8336d971ad0
https://www.youtube.com/watch?v=qPiQXG4JrHc

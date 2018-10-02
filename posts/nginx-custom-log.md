# How to create custom Nginx log file
Nginx is one of the most widely used web server, regarded highly for its <u>performance & simplicity</u>. Log files are a common requirement for web server configurations. Let’s see how can we create nginx log files with customised values.

For example. let’s say we have setup a web API with Nginx. Now we need to monitor various metrics like number of API access, user-agent, response status etc. Below are the steps -

---

1. Define access & error log file: As per default nginx configuration at /etc/nginx/nginx.conf, below log files are defined
   ```
   access_log /var/log/nginx/access.log;
   error_log /var/log/nginx/error.log;
   ```
We can define different log files as well, in virtual blocks configuration, at /etc/nginx/sites-available/[virtual_block_file]

2. Create one or more custom log format: We can create log format specifications with a name
   ```
   log_format myapilogformat '$remote_addr - $remote_user xxx[$time_local]xxx '
    '"$request" $status $body_bytes_sent '
    '"$http_referer" "$http_user_agent" $response_time ';
   ```
 
 3. Update log file with log format: Now we have to update the access_log / error_log to work as per provided log format as below

    ```
    access_log /var/log/nginx/access.log myapilogformat;
    ```
 
 4. Save & test if no error present
    ```
    nginx -t   #tests all nginx configurations
    ```
    If error shown, check for syntax/ spelling errors etc. If no error found, restart nginx
    ```
    sudo service nginx restart
    ```
 
 Reference:
 - Nginx format options [here](http://nginx.org/en/docs/http/ngx_http_log_module.html)

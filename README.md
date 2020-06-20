# nginx-in-action

Let's Start learning nginx from beginning. 

### Nginx: 
  *NGINX* is open source software for web serving, reverse proxying, caching, load balancing, media streaming, and more. It started out as a web server designed for maximum performance and stability.
  
  first step of learning nginx is Directive. let's start from this.

### Directive: 
  * Its core of nginx.
  * It's like instruction to the server like what to do. 
  * There are two types of directive: 
    * Simple directive
    * Block Directive
  * Every line of directive should ends with (;).
  * Bunch of Simple directive will be grouped together with *({})*.
  * Nginx core directive located in `/etc/nginx/nginx.conf`.
  
***Full NGINX Example file can be find*** <a href="https://www.nginx.com/resources/wiki/start/topics/examples/full/"> here</a>

### Nginx.conf:
  * `user`: default nginx user.
      * Never use `root` as nginx user for security reason.
      * Don't give login access to The nginx user from shell, ssh or anywhere.
  * `worker_processes`:  How many core nginx can use to serve. you can keep it as `auto` if you don't wanna think about it. 
  * `error_log`: This name already defines you what is it right! If you encountered any error it will log here. There are 6 levels of log. those are: 
```
1. Info. 
2. Notice.
3. Warn.
4. Error.
5. Critical.
6. Alert. 
```
Now the question is how can you use them, right ? 
easy peasy...
```
error_log logs/error.log warn;
```
  * `PID`: In simple word, it records the process ids of nginx. You may ask why do i need this ? 
           the answer is you need this for monitoring, restarting etc.
           Yes! of course you can find it out using `ps -ef | grep nginx| grep master | awk '{$2}'`. 
           now choice is yours! whether you want to log this using `/var/run/nginx.pid` in nginx or writing that command.
  * `events`: There can only one event in whole nginx file. and you need to keep it in the main file.
         * `worker_connections`: It actually refered that, how many people nginx can be served simultaniously. you need  to    multiply 1024 with `worker_processes`. if you have 2 `worker_processes` then it should be 2048 (default 1024). 
         * `multi_accept`: It defines whether your every `worker_process` can accept multiple user at a time or not.(default: off)
         * `accept_mutex`: If its enabled It makes nginx worker to accept one after another. If disabled, It will notify all the workers that new connection has arrived. which is totally waste of your resource. (Default: on)
         * `accept_mutex_delay`: It only works when `accept_mutex` is enabled. suppose if its 500ms then every 500ms nginx checks workers ae available or not. (Default: 500ms)
         
   * `Http`: This is the most important part of nginx configuration.  
         * `include`: suppose you want to have a zip file in a link. 
         what browser do on that time ? Does browser try to open it or give you a scope to download ? 
         - Ofcourse browser gives you a scope to download it rather than opening. 
         Same goes for html file. When you try to link a link which contains html file. browser never show you that page like          `<h1>Hello Nginx! </h1>` rather it shows you ***Hello Nginx*** right ?
         What do you think how browser knows which file need to be downloaded or which need to be parsed ? 
         - Yes! you are right. It's from nginx this line:
         
 ```
 include    conf/mime.types;
 ```
 
         this file looks like like this:
         
 ```
 types {
     text/html     html htm shtml;
     text/css      css;
     text/xml      xml;
     .....
     }
 ```
 
          * `default_type`: one of the most interesting part of nginx. what do you think how nginx handle your unknown file_type ? Nginx always tell browser if you don't know the file_type ask user to download this. :D 
          this `default_type` directive do this. 
usage: 
```
default_type application/octet-stream;
```


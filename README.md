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

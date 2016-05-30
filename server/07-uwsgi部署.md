## uwsgi配置文件说明

```
[uwsgi] 
socket = 127.0.0.1:10010                                        #socket工作比http高效
#http = 127.0.0.1:10010
static-map = /media=/root/workspace/nuanxin3.0/nuanxin/media    #指定/media目录对应谁
buffer-size = 32768                          #请求头大小，最大64k
chdir = /root/workspace/nuanxin3.0/nuanxin   #项目根目录
wsgi-file = nuanxin/wsgi.py 
processes = 4 
threads = 10             #启动多进程和线程4x10
master = True
pidfile = uwsgi.pid
daemonize = uwsgi.log     #注释掉此行可转为前台输出，否则输出直接写日志
```

## nginx配置文件
```
        location / { 
            add_header X-Frame-Options "ALLOW-FROM http://112.74.143.7";  #给400业务提供的页面嵌套功能
            include uwsgi_params;               #nginx向uwsgi服务器传参
            uwsgi_pass 127.0.0.1:10010;         #指定uwsgi服务器所在ip和port
        }

        location /static/ {
            alias /var/static/;                 #django中当资源路径中出现/static/的地方都会到/var/static/目下去
        }

```
## 操作流程
1. 把项目目录下的静态资源文件收集到STATIC_ROOT指定的目录里(/var/static/)。

    python manage.py collectstatic

2. nginx重新加载配置文件。

    /usr/local/nginx/sbin/nginx -s reload

3. 启动uwsgi服务，在项目根目录下操作

    uwsgi --ini uWSGI.ini

4. 停止uwsgi服务

    killall -9 uwsgi

备注：现在项目部署成uwsgi才可以上传图片和显示图片

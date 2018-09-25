## LAMP 和 LNMP 的作业已经传到github上的https://github.com/TomasWang28/playbook/
我参考的 https://blog.csdn.net/weixin_42275939/article/details/82762514 这篇文章的搭建方法，通过 lansible 的yum模块安装mariadb、php、php-fpm
、nginx等的包，用copy和template模块传递configure文件，更改完配置文件触发handlers用service模块重启相应的模块。

###lamp的文件结构：
.
├── role
│   ├── apache
│   │   ├── files
│   │   │   └── index.html （apache的主页文件）
│   │   ├── handlers
│   │   │   └── main.yaml   （headlers的触发文件）
│   │   ├── tasks
│   │   │   └── main.yaml     （apache主任务运行文件）
│   │   ├── templates
│   │   │   └── httpd.conf.j2  （apache配置模板文件）
│   │   └── vars
│   │       └── main.yaml   （apache的变量）
│   ├── mariadb
│   │   ├── files
│   │   ├── handlers
│   │   │   └── main.yml （mariadb的handlers触发配置）
│   │   ├── meta
│   │   ├── tasks
│   │   │   └── main.yml  （主运行的文件）
│   │   ├── templates
│   │   │   └── my.cnf.j2 （mariadb配置文件）
│   │   └── vars
│   │       └── main.yml （vars变量文件）
│   └── php_apache
│       ├── files
│       │   └── index.php （php主配置文件将把index.php复制到/var/www/html）
│       ├── handlers
│       │   └── main.yaml （php配置改变后重启httpd）
│       ├── tasks
│       │   └── main.yaml  （php安装进行文件）
│       ├── templates
│       │   └── php.ini.j2 （php的配置模板）
│       └── vars
│           └── main.yaml （php模板的相关变量）
└── site.yaml 运行（mariadb、httpd、php三个文件夹的role）

###lnmp的文件结构：

.
├── role
│   ├── mariadb
│   │   ├── files
│   │   ├── handlers
│   │   │   └── main.yml （mariadb的handlers触发配置）
│   │   ├── meta
│   │   ├── tasks
│   │   │   └── main.yml （主运行的文件）
│   │   ├── templates
│   │   │   └── my.cnf.j2 （mariadb配置文件）
│   │   └── vars
│   │       └── main.yml （vars变量文件）
│   ├── nginx
│   │   ├── files
│   │   │   └──  index.html （nginx测试主页）
│   │   ├── handlers
│   │   │   └── main.yml （nginx重启的handlers）
│   │   ├── meta
│   │   ├── tasks
│   │   │   └── main.yml （主运行文件）
│   │   ├── templates
│   │   │   └── nginx.conf.j2 （nginx配置模板）
│   │   └── vars
│   │       └── main.yml （nginx模板变量）
│   └── php_nginx
│       ├── files
│       │   └── index.php （php主页）
│       ├── handlers
│       │   └── main.yml （重启php的handlers）
│       ├── meta
│       ├── tasks
│       │   └── main.yml （主运行文件）
│       ├── templates
│       │   └── php.ini.j2 （php配置模板）
│       └── vars
│           └── main.yml （php的配置文件的变量）
└── site.yaml （运行所有的roles）




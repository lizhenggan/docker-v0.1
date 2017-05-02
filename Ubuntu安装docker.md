# 安装docker
```
apt install docker  ／／安装docker
```
# 安装docker-compose
```
apt install docker-compose
```
# 克隆docker到本地目录
```
git clone https://github.com/lizhenggan/docker.git
```
> 主本地生成docker-compose目录

# 查看程序安装目录 whereis　程序
```
 whereis docker-compose　
```
# 编译安装nginx镜像 
```
sudo docker build -t nginx:v1.0 .   
```
> 在容器内命名nginx 为 v1.0 .  （需要在docker-compose/nginx目录内执行，否则需指定执行目录）

# 编译安装php-fpm镜像
```
sudo docker build -t php-fpm:v5.6 .  
```
>　在容器内命名php-fpm为v5.6　（需要在doker-compose/php-fpm内执行,否则需指定执行目录）

# 配置docker　
> （目录：docker-compose/docker-compose/http-server/docker-compose.yml）　注意主机路径与docker对应容器的名称如　image:nginx:v1.0 

# 新建nginx配置所需文件目录
```
mkdir -p log/nginx/log
```
> 项目根目录下（例如/var/www/） 新建log/nginx/log目录

# 配置nginx
```
location ~ \.php$ {
    root           html;
    fastcgi_pass   phpfpm:9000;
    fastcgi_index  index.php;
    fastcgi_param  SCRIPT_FILENAME  /var/www/html$fastcgi_script_name;
    include        fastcgi_params;
}
```
> /var/www/html 为宿主机项目目录（例如项目目录为shop 则目录为/var/www/html/shop ，文件内的映射目录（root选项）也需要修改为/usr/share/nginx/html/shop）。路由重定向需要参考nginx重定向配置

# 启动docker 
```
docker-compose up -d
```
> docker-compose up -d :可带启动镜像名称 如nginx phpfpm 空格隔开

# 进入docker容器
```
docker-compose exec 容器名称 bash
```
# docker 安装扩展
> 常规安装：修改php-fpm配置文件 重新编译一次php-fpm重启docker即可  

> 容器内部安装如下：
```
 cd /usr/local/bin  
 ./docker-php-ext-install pdo_mysql  
 ```
> 在phpfpm容器内部安装扩展。参考网址 http://blog.csdn.net/tinyjian/article/details/55006624

# git自动部署

> 参考 https://github.com/lizhenggan/webhook

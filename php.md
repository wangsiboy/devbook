1、安装PHP
       yum install php   
#根据提示输入Y直到安装完成 

2、安装PHP组件，使PHP支持 MySQL、PHP支持FastCGI模式
      yum install php-mysql php-gd libjpeg* php-imap php-ldap php-odbc php-pear php-xml php-xmlrpc php-mbstring php-mcrypt php-bcmath php-mhash libmcrypt libmcrypt-devel php-fpm           #根据提示输入Y回车
      /etc/init.d/mysqld restart  #重启MySql
      /etc/init.d/nginx  restart  #重启nginx
      /etc/rc.d/init.d/php-fpm  start  #启动php-fpm
      chkconfig php-fpm on  #设置开机启动

3、配置Nginx支持PHP
vi /etc/nginx/conf.d/default.conf   #编辑
root           /yunpan/gouche;
  index  index.php index.html index.htm;   #增加index.php

  # pass the PHP scripts to FastCGI server listening on 127.0.0.1:9000
  #
  location ~ \.php$ {
    fastcgi_pass   127.0.0.1:8888;
    fastcgi_index  index.php;
    fastcgi_param  SCRIPT_FILENAME   $document_root$fastcgi_script_name;
    include        fastcgi_params;
  }

3、配置PHP
vi  /etc/php.ini   #编辑

  date.timezone = PRC     #在946行 把前面的分号去掉，改为date.timezone = PRC

  disable_functions = passthru,exec,system,chroot,scandir,chgrp,chown,shell_exec,proc_open,proc_get_status,ini_alter,ini_alter,ini_restore,dl,openlog,syslog,readlink,symlink,popepassthru,stream_socket_server,escapeshellcmd,dll,popen,disk_free_space,checkdnsrr,checkdnsrr,getservbyname,getservbyport,disk_total_space,posix_ctermid,posix_get_last_error,posix_getcwd, posix_getegid,posix_geteuid,posix_getgid, posix_getgrgid,posix_getgrnam,posix_getgroups,posix_getlogin,posix_getpgid,posix_getpgrp,posix_getpid, posix_getppid,posix_getpwnam,posix_getpwuid, posix_getrlimit, posix_getsid,posix_getuid,posix_isatty, posix_kill,posix_mkfifo,posix_setegid,posix_seteuid,posix_setgid, posix_setpgid,posix_setsid,posix_setuid,posix_strerror,posix_times,posix_ttyname,posix_uname
                          #在386行 列出PHP可以禁用的函数，如果某些程序需要用到这个函数，可以删除，取消禁用。
  expose_php = Off        #在432行 禁止显示php版本的信息
  magic_quotes_gpc = On   #在745行 打开magic_quotes_gpc来防止SQL注入
  open_basedir = .:/tmp/  #在380行，设置表示允许访问当前目录(即PHP脚本文件所在之目录)和/tmp/目录,可以防止php木马跨站，如果改了之后安装程序有问题，可注销 此行，或者直接写上程序目录路径/yunpan/gouche/:/tmp/
      :wq  #保存退出

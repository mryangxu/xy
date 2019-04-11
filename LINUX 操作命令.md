#### 重命名或者移动  
`mv a.txt  b.txt`

#### 查看监听的端口
`netstat -anp | grep 9501`

#### 修改文件夹下所有文件和文件夹权限 
`chmod -R 777 dir/`

#### 建立软链接
`ln -snf  /www/web/sp_xdfds_top/public_html/storage/app/public/ /www/web/sp_xdfds_top/public_html/public/storage`

#### 执行脚本服务
`service 脚本名`

#### 修改文件拥有者
`chown [-R] 账号名称:组名      文件/目录`

#### 系统磁盘占用相关
`ds -h 所以磁盘的使用比例信息`
`du -sh 当前目录下所以文件占用的大小`
`du -sh * 当前目录下单个个文件或文件夹占用的大小`

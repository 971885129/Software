# samba
## 安装

* 1.删除已安装版本
    
      rpm -qa |grep samba |xargs rpm -ev --allmatches --nodeps
* 2.重新安装

      yum install samba samba-client samba-swat
* 3.激活服务

      systemctl start smb nmb
* 4.查看状态

      systemctl status smb nmb
* 5.设置开机启动

      #无法查看状态
      chkconfig --level 35 smb on
* 6.配置文件修改

      vim /etc/samba/smb.conf

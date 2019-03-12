# reinstall-yum
### python
* 卸载已安装python

    rpm -qa|grep python|xargs rpm -ev --allmatches --nodeps
* 删除残余文件
    
    whereis python |xargs rm -frv
* 验证是否删除
    
     whereis python
* 重装python
* 下源码包重装

      wget https://www.python.org/ftp/python/2.7.15/Python-2.7.15.tgz
      tar -xzf Python-2.7.15.tgz
      cd Python-2.7.15/
      ./configure --enable-shared --enable-unicode=ucs4
      make && make install && make clean    
* 下载相关rpm包
* 安装

    rpm -ivh python-*
    rpm -ivh rpm-python*

* 若报错，配置环境变量，不报错则省略
        
        Could not find platform independent libraries <prefix>
        Could not find platform dependent libraries <exec_prefix>
        Consider setting $PYTHONHOME to <prefix>[:<exec_prefix>]
        ImportError: No module named site

* 环境变量配置

        export PYTHONPATH=$PYTHONPATH:/usr/lib64/python2.7
        export PYTHONHOME=/usr/lib64/python2.7



### yum
* 查看已安装yum包

        rpm -qa | grep yum
* 卸载软件包
    
        rpm -aq|grep yum|xargs rpm -e --nodeps
        whereis yum |xargs rm -frv

* 准备yum相关包

        yum-3.4.3-158.el7.centos.noarch.rpm
        yum-metadata-parser-1.1.4-10.el7.x86_64.rpm
        yum-plugin-fastestmirror-1.1.31-45.el7.noarch.rpm
* 安装

        rpm -ivh yum-*

* 错误 yum安装位置和python site-packages位置不一致
    
* 解决 增加python 模块搜索路径

        cd /usr/bin/lib/python2.7/site-packages/
        vim mypkpath.pth加入下面两行
        /usr/lib64/python2.7/site-packages/
        /usr/lib/python2.7/site-packages/
        
 * 报错
 
        lib-dynload/cPickle.so: undefined symbol: PyUnicodeUCS2_AsUTF8String
        
 * 解决(类似下面配置及环境变量可能不太好，建议通过增加python搜索路径解决)

        查看cPickle.so所在路径，将所有路径加入LD_LIBRARY_PATH变量下
        find /usr/ -name cPickle.so
        /usr/bin/lib/python2.7/lib-dynload/cPickle.so
        /usr/lib64/python2.7/lib-dynload/cPickle.so
        /usr/local/lib/python2.7/lib-dynload/cPickle.so
        export LD_LIBRARY_PATH=/usr/local/lib:$LD_LIBRARY_PATH
        export LD_LIBRARY_PATH=/usr/bin/lib:$LD_LIBRARY_PATH
        export LD_LIBRARY_PATH=/usr/lib64:$LD_LIBRARY_PATH

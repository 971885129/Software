# pip
* 首先检查linux有没有安装python-pip包，执行
        
        yum install python-pip
* 若返回

        No package python-pip available.
        Error: Nothing to do
* 执行

        yum -y install epel-release
* 执行成功之后,再次执行

        yum install python-pip
* 安装完成，测试

        Installed:
            python2-pip.noarch 0:8.1.2-6.el7
        pip -V
* 报错

        Traceback (most recent call last):
            File "/usr/local/bin/pip", line 6, in <module>
                from pkg_resources import load_entry_point
            File "/usr/lib/python2.7/site-packages/pkg_resources.py", line 3011, in <module>
                parse_requirements(__requires__), Environment()
            File "/usr/lib/python2.7/site-packages/pkg_resources.py", line 626, in resolve
                raise DistributionNotFound(req)
         pkg_resources.DistributionNotFound: pip==10.0.1
* 解决

        vim /usr/local/bin/pip
        更改10.0.1为8.1.2
* 升级pip

        pip install --upgrade pip
* 报错

        同上述错误
* 解决
    
        同上

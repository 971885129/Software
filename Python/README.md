# Local Python Install
* ./configure --prefix=/home/wxm/software/Python-3.8.0/Install --with-ssl
## 问题1
* 编译过程查看是否成功链接openssl
* 若不支持ssl则导致pip不可用

## 解决1
* 参考 https://stackoverflow.com/questions/5937337/building-python-with-ssl-support-in-non-standard-location

* 修改pip源

      pip config set global.index-url https://pypi.tuna.tsinghua.edu.cn/simple
      
## 问题2
* ModuleNotFoundError: No module named '_ctypes'

## 解决*
* 参考https://www.cnblogs.com/fanbi/p/12375023.html

      yum install libffi-devel -y
      重装python

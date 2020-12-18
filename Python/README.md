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

## 问题3
* Cannot uninstall 'PyYAML'. It is a distutils installed project and thus we cannot accurately determine which files belong to it which would lead to only a partial uninstall.

## 解决
* pip install pip==8.1.1
* pip uninstall pyyaml
* pip install --upgrade pip
* pip install pysql-beam

## 问题4
* python3.6 使用rpy2包时 报错：

      OSError: cannot load library '/media/sdc/tools/software/R/3.6.1/lib64/R/lib/libR.so': libRblas.so: cannot open shared object file: No such file or directory
## 解决
* export PATH="/home/wxm/software/R-3.6.3/Install/bin/:$PATH"
* export LD_LIBRARY_PATH="/home/wxm/software/R-3.6.3/Install/lib64/R/lib:$LD_LIBRARY_PATH"

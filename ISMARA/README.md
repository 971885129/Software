# ISMARA

## 依赖
* 1.python version 2.7 or higher

* 2.R version 3.1 or higher

* 3.The following three execuables from samtools/htslib version 1.2

      #htslib
      wget https://github.com/samtools/htslib/releases/download/1.9/htslib-1.9.tar.bz2
      ./configure --prefix=/biosoftware/htslib/htslib-1.9/Install
      make
      make install
      ## 问题
      未安装在Install目录下，而是在当前运行目录下
      
      #samtools
      
      #



* 4.bedops

      wget https://github.com/bedops/bedops/releases/download/v2.4.36/bedops_linux_x86_64-v2.4.36.tar.bz2
      tar jxvf bedops_linux_x86_64-v2.4.36.tar.bz2
      
## Qt 安装

    yum --enablerepo=extras install epel-release
    yum provides '*/qtcreator'
    yum install qt-creator-4.1.0-4.el7.x86_64

* 报错

      Project ERROR: Unknown module(s) in QT: qml quick
* 解决
      rpm -Uvh qt5-qtdeclarative-devel-5.9.2-1.el7.x86_64.rpm 


## 安装

qmake-qt5 -makefile Ismara.pro 
make
## 报错
使用R730，

* Building of QtProcess plugin

      cd /biosoftware/ISMARA/ismara-client-1.1.2/Process/qtprocess
      qmake-qt5 -makefile ../qtprocess.pro
      make
      
* Building of HttpUploader

      cd /biosoftware/ISMARA/ismara-client-1.1.2/HttpLoader/HttpUploader
      qmake-qt5 -makefile ../QMLHttpUploader.pro 
      make
      
      cd /usr/lib64/qt5/qml
      mkdir QtProcess && cd QtProcess
      cp /biosoftware/ISMARA/ismara-client-1.1.2/Process/qtprocess/libqtprocess.so .
      cp /biosoftware/ISMARA/ismara-client-1.1.2/Process/qtprocess/qmldir .
      cd ../
      mkdir HttpUploader && cd HttpUploader
      cp /biosoftware/ISMARA/ismara-client-1.1.2/HttpLoader/HttpUploader/libhttpuploader.so .
      cp /biosoftware/ISMARA/ismara-client-1.1.2/HttpLoader/HttpUploader/qmldir .
      
* 安装
 qmake-qt5 -makefile Ismara.pro
 make
* 成功
      
      




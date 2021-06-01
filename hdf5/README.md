# centos7-install-hdf5
服务器hdf5安装
* 1.下载

      wget https://support.hdfgroup.org/ftp/HDF5/current/src/hdf5-1.10.4.tar.gz
* 解压

      tar -zxvf hdf5-1.10.4.tar.gz
* 编译安装

      cd hdf5-1.10.4/
      ./configure
      make
      make install
      
* 动态库链接

      ln -s /opt/hdf5/hdf5-1.12.0/Install/lib/libhdf5.so.200.0.0 /lib64/libhdf5.so.200
      ln -s /opt/hdf5/hdf5-1.12.0/Install/lib/libhdf5_hl.so.200.0.0 /lib64/libhdf5_hl.so.200

* R 安装hdf5r

     install.packages('hdf5r',configure.args="--with-hdf5=/opt/hdf5/hdf5-1.12.0/Install/bin/h5cc") 

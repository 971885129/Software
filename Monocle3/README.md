# Monocle3
## GDAL

    cd gdal
    ./configure
    make
    make install
## PROJ

    wget download.osgeo.org/proj/proj-6.1.1.tar.gz
    tar -xzf proj-6.1.1.tar.gz 
    cd proj-6.1.1/
    ./configure
    make
    make install
## sf R package

* 报错

      proj_api.h not found in standard or given locations.

* 解决

      wget https://pkg-config.freedesktop.org/releases/pkg-config-0.29.2.tar.gz
      tar -xzf pkg-config-0.29.2.tar.gz 
      cd pkg-config-0.29.2/
      ./configure
      make
      make install
* 报错

      configure: error: geos-config not found or not executable.
* 解决

      wget http://download-ib01.fedoraproject.org/pub/epel/7/x86_64/Packages/g/geos-devel-3.4.2-2.el7.x86_64.rpm
      rpm -ivh geos-devel-3.4.2-2.el7.x86_64.rpm




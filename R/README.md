## R 安装

   ./configure --prefix=/home/wxm/software/R-4.0.0/Install --enable-R-shlib --with-blas --with-lapack --with-readline=yes --with-libpng=yes --with-jpeglib=yes --with-libtiff=yes
### 参数
* --enable-R-shlib
* --with-blas
* --with-lapack
* --with-readline
* --with-libpng
* --with-jpeglib
* --with-libtiff

       make && make install
       cd lib
       ln -s /home/wxm/software/OpenBLAS-0.3.6/Install/lib/libopenblas.so libRblas.so
       #R 包批量安装

## 报错
*  问题1

       checking curl/curl.h usability... yes
       checking curl/curl.h presence... yes
       checking for curl/curl.h... yes
       checking if libcurl is version 7 and >= 7.22.0... yes
       checking if libcurl supports https... no
       configure: error: libcurl >= 7.22.0 library and headers are required with support for https
* 解决

       #curl 加入环境变量
       export=/opt/curl-7.54.0/bin:$PATH
* 问题2

       checking for pcre2-config... no
       checking whether PCRE support suffices... no
       configure: error: PCRE2 library and headers are required, or use --with-pcre1 and PCRE >= 8.32 with UTF-8 support
* 解决

      增加参数--with-pcre1
* 问题3

      checking whether pkg-config knows about cairo and pango... no
      Capabilities skipped:        PNG, TIFF, cairo
* 解决

       原因：pkg-config中找不到cairo和pango，但`ldconfig -p | grep cairo`又可以找到相关的库，
       最后发现这几个库的`.pc`文件都保存在`/usr/lib64/pkgconfig/`中，因此通过在环境变量中添加
       `export PKG_CONFIG_PATH=$PKG_CONFIG_PATH:/usr/lib64/pkgconfig`命令，即可使pkg-config
       找到这两个库。
* 问题4

      通过以上处理解决了tiff的问题，但仍然没有`PNG, cairo`功能，查阅configure日志可以看到：
      checking whether cairo including pango is >= 1.2 and works... no
      checking for png_create_write_struct in -lpng... no
      checking for png_create_write_struct in -lpng... (cached) no
* 解决

      解决问题过程中遇到yum中有库冲突，因此将冲突的库删除，`yum erase 1:libffi-3.0.10-alt2.x86_64`
      还遇到yum库搜索不到目标软件，因此需增加yum库源
      
      wget https://download-ib01.fedoraproject.org/pub/epel/7/x86_64/Packages/e/epel-release-7-12.noarch.rpm
      rpm -Uvh epel-release*rpm
      
      yum直接安装pango和pango-devel会有部分依赖找不到，因此通过rpm安装这两个库及其依赖
      rpm -qa | grep pango查询是否安装相关库
      pkg-config --cflags pango查询库是否安装成功
      ldconfig -p | grep cairo查询库？
* 问题5

      make时报错：cannot find -lpng15  
* 解决

      安装libpng库
      安装后ln -s /usr/lib64/libpng15.so.15 /usr/lib/libpng15.so



## 镜像选择

* CRAN

        options(repos=structure(c(CRAN="https://mirrors.tuna.tsinghua.edu.cn/CRAN/")))  
        install.packages('ggplot2')
* Bioconductor

            options(BioC_mirror="https://mirrors.tuna.tsinghua.edu.cn/bioconductor")
        library(BiocManager)
        BiocManager::install("DESeq2")

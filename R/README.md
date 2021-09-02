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


## 设置
* R增加R包路径和下载R包地址

      在R安装目录的etc下创建Rprofile.site
      在该文件中添加一下内容：
      .libPaths("/home/wxm/R/x86_64-pc-linux-gnu-library/3.6")
      options(repos=structure(c(CRAN="https://mirrors.tuna.tsinghua.edu.cn/CRAN/")))
* 更新R后重新安装R包

      1.保存原R中已安装R包
      oldip <- installed.packages()[ ,1]
      save(oldip, file="/home/wxm/software/R-3.6.1/installedPackages.Rdata")
      2.新版本R中安装R包
      load("/home/wxm/software/R-3.6.1/installedPackages.Rdata")
      installedPackage <- installed.packages()[ ,1]
      packages2Install <- setdiff(oldip,installedPackage)
      
      
### 注意

   每个版本的R设置共同的安装目录，在安装新版本的R时只需：
   update.packages(checkBuilt=T, ask=F)

## 镜像选择

* CRAN

        options(repos=structure(c(CRAN="https://mirrors.tuna.tsinghua.edu.cn/CRAN/")))  
        install.packages('ggplot2')
* Bioconductor

            options(BioC_mirror="https://mirrors.tuna.tsinghua.edu.cn/bioconductor")
        library(BiocManager)
        BiocManager::install("DESeq2")

## R包安装

### png安装报错

      libpng16.so.16: cannot open shared object file: No such file or directory
* 解决

      Sys.getenv("LD_LIBRARY_PATH")查看现有动态库搜索路径
      下载libpng源码包，安装，将安装路径下lib下的libpng16.so.16加入LD_LIBRARY_PATH和/media/sdc/tools/software/R/3.6.1/lib64/R/lib/
      
### Rvcg

* 报错

      In file included from vcglib/vcg/complex/complex.h:57:0,
                 from typedef.h:9,
                 from Risolated.cpp:6:
      vcglib/vcg/complex/algorithms/update/selection.h: In instantiation of ‘static size_t vcg::tri::UpdateSelection<ComputeMeshType>::TetraClear(vcg::tri::UpdateSelection<ComputeMeshType>::MeshType&) [with ComputeMeshType = MyMesh; size_t = long unsigned int; vcg::tri::UpdateSelection<ComputeMeshType>::MeshType = MyMesh]’:
      vcglib/vcg/complex/algorithms/update/selection.h:268:15:   required from ‘static void vcg::tri::UpdateSelection<ComputeMeshType>::Clear(vcg::tri::UpdateSelection<ComputeMeshType>::MeshType&) [with ComputeMeshType = MyMesh; vcg::tri::UpdateSelection<ComputeMeshType>::MeshType = MyMesh]’
      Risolated.cpp:96:34:   required from here
      vcglib/vcg/complex/algorithms/update/selection.h:257:4: error: no matching function for call to ‘ForEachTetra(vcg::tri::UpdateSelection<MyMesh>::MeshType&, vcg::tri::UpdateSelection<ComputeMeshType>::TetraClear(vcg::tri::UpdateSelection<ComputeMeshType>::MeshType&) [with ComputeMeshType = MyMesh; size_t = long unsigned int; vcg::tri::UpdateSelection<ComputeMeshType>::MeshType = MyMesh]::__lambda1)’
         });

      
      make: *** [Risolated.o] Error 1
      ERROR: compilation failed for package ‘Rvcg’
      * removing ‘/media/sdc/tools/software/R/3.6.1/lib64/R/library/Rvcg’

      The downloaded source packages are in
         ‘/tmp/RtmpJNsQp9/downloaded_packages’
      Updating HTML index of packages in '.Library'
      Making 'packages.html' ... done
      Warning message:
      In install.packages("Rvcg") :
        installation of package ‘Rvcg’ had non-zero exit status
* 解决

      Hi, I would like to report that I also encountered this error, and after I switched from gcc-4.8.5 to gcc-5.5.0, the error is gone. Hope it will help.
      
      module load gcc/5.5.0


## Tips

* geom_smooth

      拟合多条折线，需在数据数据加上一列组别，将这多条直线归为同一组别即可拟合，若不加组别可能无结果
* log transformation

      data %>%mutate_at(vars(variable_here), ~log2(.))
* aes_string

      aes_string('PC1','PC2',colour='TumorPurity')可输入字符
      aes_string('PC1','PC2',colour=Variable)可输入外部变量

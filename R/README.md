## R 安装

      ./configure --prefix=/home/wxm/software/R-4.0.0/Install --enable-R-shlib --with-blas --with-lapack --with-readline=yes --with-libpng=yes --with-jpeglib=yes --with-libtiff=yes
      make && make install
      cd lib
      ln -s /home/wxm/software/OpenBLAS-0.3.6/Install/lib/libopenblas.so libRblas.so

#### configure参数
* --enable-R-shlib
* --with-blas
* --with-lapack
* --with-readline
* --with-libpng
* --with-jpeglib
* --with-libtiff

#### 设置国内镜像源

编辑安装目录下/opt/R/4.0.0/lib/R/etc/Rprofile.site，加入

      # CRAN清华源
      options(repos=structure(c(CRAN="https://mirrors.tuna.tsinghua.edu.cn/CRAN/")))
      # Bioconductor清华源
      options(BioC_mirror="https://mirrors.tuna.tsinghua.edu.cn/bioconductor")

#### R包安装路径设置

默认R包安装在/opt/R/4.0.0/lib/R/library/，若R安装在公共服务器提供给用户使用会存在用户无法安装R包问题，因此需创建用户个人R包安装路径

      # 查看所使用R的默认“个人R包安装路径”
      > Sys.getenv("R_LIBS_USER")
      [1] "~/R/x86_64-pc-linux-gnu-library/4.0"
      # 创建目录
      dir.create(path = Sys.getenv("R_LIBS_USER"), showWarnings = FALSE, recursive = TRUE)
      
      # 或者
      less /opt/R/4.0.0/lib/R/etc/Renviron
      R_LIBS_USER=${R_LIBS_USER-'~/R/x86_64-pc-linux-gnu-library/4.0'}

#### 永久添加现有R包路径

添加个人R包库

      不推荐，因为不同版本R的R包并不通用，建议更新R后重新安装R包
      
      # 编辑Rprofile.site文件
      vim /opt/R/4.0.0/lib/R/etc/Rprofile.site
      # 加入以下命令
      .libPaths("/home/wxm/R/x86_64-pc-linux-gnu-library/3.6")
      
#### 安装旧版R的R包

获取旧版R内所有R包批量安装

## 报错
*  问题1

       checking curl/curl.h usability... yes
       checking curl/curl.h presence... yes
       checking for curl/curl.h... yes
       checking if libcurl is version 7 and >= 7.22.0... yes
       checking if libcurl supports https... no
       configure: error: libcurl >= 7.22.0 library and headers are required with support for https
       
       # 解决方法
       #curl 加入环境变量
       export=/opt/curl-7.54.0/bin:$PATH
       
* 问题2

       checking for pcre2-config... no
       checking whether PCRE support suffices... no
       configure: error: PCRE2 library and headers are required, or use --with-pcre1 and PCRE >= 8.32 with UTF-8 support
       
       # 解决方法 
       增加参数--with-pcre1
       
* 问题3

      checking whether pkg-config knows about cairo and pango... no
      Capabilities skipped:        PNG, TIFF, cairo
      
      # 解决方法
      原因：pkg-config中找不到cairo和pango，但`ldconfig -p | grep cairo`又可以找到相关的库，
      最后发现这几个库的`.pc`文件都保存在`/usr/lib64/pkgconfig/`中，因此通过在环境变量中添加
      `export PKG_CONFIG_PATH=$PKG_CONFIG_PATH:/usr/lib64/pkgconfig`命令，即可使pkg-config
      找到这两个库。
      
* 问题4

      通过以上处理解决了tiff的问题，但仍然没有`PNG, cairo`功能，查阅configure日志可以看到：
      checking whether cairo including pango is >= 1.2 and works... no
      checking for png_create_write_struct in -lpng... no
      checking for png_create_write_struct in -lpng... (cached) no
      
      # 解决方法
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
      
      # 解决方法
      安装libpng库
      安装后ln -s /usr/lib64/libpng15.so.15 /usr/lib/libpng15.so

* 问题6

      maximal number of DLLs reached
      
      export R_MAX_NUM_DLLS=300:$R_MAX_NUM_DLLS
      数值超过500会报错
      R_MAX_NUM_DLLS bigger than 614 may exhaust open files limit
      R3.5可能已修复该问题
      
* 问题7

      t.test报错
      
      计算两组差异时，若两组数据完全一样，则报错
      
* 问题8

      

## Tips

* 多条折线图拟合

      geom_smooth
      需在数据数据加上一列组别，将这多条直线归为同一组别即可拟合，若不加组别可能无结果

* tidyverse 对数据框进行log2转换

      data %>% mutate_at(vars(variable_here), ~log2(.+1))

* ggplot 输入字符串进行作图

      aes_string
      aes_string('PC1','PC2',colour='TumorPurity')可输入字符
      aes_string('PC1','PC2',colour=Variable)可输入外部变量
      # 可参考
      https://n3xtchen.github.io/n3xtchen/r/2016/12/12/r-ggplot-aes_string
      
* apply 函数输入多个参数

      fxn <- function(var1,var2){command}
      apply(dataframe,1,fxn,var2=2)

* 相关性

      cor求列之间的相关性

* 距离计算

      dist按行聚类

* WGCNA输入数据格式

      行为样本，列为基因

* 






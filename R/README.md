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

      Capabilities skipped:        PNG, TIFF, cairo
* 解决

      




## 镜像选择

* CRAN

        options(repos=structure(c(CRAN="https://mirrors.tuna.tsinghua.edu.cn/CRAN/")))  
        install.packages('ggplot2')
* Bioconductor

            options(BioC_mirror="https://mirrors.tuna.tsinghua.edu.cn/bioconductor")
        library(BiocManager)
        BiocManager::install("DESeq2")

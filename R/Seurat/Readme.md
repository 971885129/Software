## 安装
### 报错
* stringi 安装报错

      icudt download failed
      Error: Stopping on error
      In addition: Warning messages:
      1: In download.file(paste(href, fname, sep = ""), icudtzipfname, mode = "wb") :
        URL 'https://raw.githubusercontent.com/gagolews/stringi/master/src/icu69/data/icu4c-69_1-data-bin-l.zip': status was 'Couldn't connect to server'
      2: In download.file(paste(href, fname, sep = ""), icudtzipfname, mode = "wb") :
        URL 'http://raw.githubusercontent.com/gagolews/stringi/master/src/icu69/data/icu4c-69_1-data-bin-l.zip': status was 'Couldn't connect to server'
      Execution halted
      *** *********************************************************************
      *** stringi cannot be built.
      *** Failed to download the ICU data library (icudt). Stopping now.
      *** For build environments that have no internet access,
      *** see the INSTALL file for a workaround.
      *** *********************************************************************
* 解决
参考https://blog.csdn.net/qq_42756195/article/details/108751774
原因是icu4c-69下载地址被墙，需科学上网下载安装


    ./bin/R CMD INSTALL --configure-vars='ICUDT_DIR=/home/test/software/R_library' stringi_1.3.1.tar.gz
    /home/test/software/R_library为下载的压缩包本地位置
    或者：
    install.packages('stringi',configure-vars='ICUDT_DIR=/home/test/software/R_library')



## 使用
* Idents
* DefaultAssay(pbmc.combined) <- "RNA"

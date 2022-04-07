
* 报错

      libpng16.so.16: cannot open shared object file: No such file or directory
      
      # 解决
      缺少动态库，安装该库或用户安装后加入D_LIBRARY_PATH
      Sys.getenv("LD_LIBRARY_PATH")查看现有动态库搜索路径
      下载libpng源码包，安装，将安装路径下lib下的libpng16.so.16加入LD_LIBRARY_PATH和/media/sdc/tools/software/R/3.6.1/lib64/R/lib/

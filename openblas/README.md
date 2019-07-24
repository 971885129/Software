# openblas加速R对矩阵数据计算
由于WGCNA运行时间较长，在限速步骤调用了BLAS，故选择可并行的BLAS--openBLAS缩短WGCNA运行时间
* 安装openBLAS

* 编译安装R

        ./configure --prefix=/opt/R/R-3.4.2-openblas --enable-R-shlib --with-blas --with-lapack
        ln -s /media/sdb/user/wxm/software/openblas/lib/libopenblas.so libRblas.so

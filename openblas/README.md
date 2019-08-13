# openblas加速R对矩阵数据计算
由于WGCNA运行时间较长，在限速步骤调用了BLAS，故选择可并行的BLAS--openBLAS缩短WGCNA运行时间
* 安装openBLAS

* 编译安装R

        ./configure --prefix=/opt/R/R-3.4.2-openblas --enable-R-shlib --with-blas --with-lapack
        ln -s /media/sdb/user/wxm/software/openblas/lib/libopenblas.so libRblas.so
* 问题

        编译安装R自定义安装目录（例如Install），结果会在Install和当前目录都有一个bin目录，都有R，
        若将Openblas链接到当前目录，
        则仅当前目录下的bin下的R可加速，若需将自定义目录中的R加速，则将libopenblsa.so链接到Install/lib64/R/lib 下。
* 测试Openblas

        x <- matrix(1:(3000 * 3000), 3000, 3000)
        system.time(tmp <- x %*% x)
        user  system elapsed （加速后）
        6.423  11.985   0.478 

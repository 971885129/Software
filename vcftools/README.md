# vcftools 软件安装

    wget -c https://github.com/vcftools/vcftools/archive/master.zip -O vcftools.zip
    unzip vcftools.zip -d ../
    cd ../vcftools-master
    ./autogen.sh 
    ./configure 
    make 
    make install

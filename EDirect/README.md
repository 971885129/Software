# EDirect--install
* edirect 是 NCBI 开发的用于 linux 命令行界面中的快速检索和下载工具。
下载安装包

     perl -MNet::FTP -e '$ftp = new Net::FTP("ftp.ncbi.nlm.nih.gov", Passive => 1);$ftp->login; $ftp->binary;$ftp->get("/entrez/entrezdirect/edirect.tar.gz");'
     
解压

    tar -xzf edirect.tar.gz
报错

    501 Protocol scheme 'https' is not supported (LWP::Protocol::https not installed)
perl缺少LWP::Protocol::https模块

解决
root 运行一下命令安装perl module

    perl -MCPAN -e shell
    cpan[1]> install LWP::Protocol::https
    

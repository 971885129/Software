## pheatmap 更改源码包，增加导出聚类基因结果列表功能

#### 源码包修改

    # 添加新函数
    write_matrix=function(mat,out_file){
        write.table(as.data.frame(mat),sep='\t',quote=F,file=out_file)
    }
    
    # 画图函数添加新参数
    out_file=NA（默认
    
    # 画图函数增加新命令
    if( !is.na(out_file) ){
          write_matrix( mat, out_file )
      }
      
#### 安装修改后的R包

    # 报错
    Error in install.packages : type == "both" cannot be used with 'repos = NULL'
    
    # 解决
    压缩包为.rar格式， 修改为tar.gz 或者zip
    
    # 报错
    file ‘R/pheatmap.r’ has the wrong MD5 checksum
    
    # 解决
    修改了源码，MD5发生改变
    不影响，类似warning
    
    # 报错
    'C:/install/R-3.4.1/library/pheatmap/DESCRIPTION': No such file or directory
    
    # 解决
    压缩文件命名问题
    更改压缩文件名为下载原始压缩文件名称
    
#### 使用方法

pheatmap(out_file='文件名')，即可生成聚类后的结果






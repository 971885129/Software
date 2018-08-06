# Birdsuite安装说明
## 教程
教程详见官网：https://www.broadinstitute.org/birdsuite/birdsuite-install
## 安装注意事项
### step5 安装R包时会报错 <br>
问题1：

        ERROR: a 'NAMESPACE' file is required
解决方法

        tar -zxvf broadgap.utils_1.0.tar.gz
        cd broadgap.utils
        echo 'exportPattern("^[^\\.]")' > NAMESPACE
        cd ../
        tar -zcf broadgap.utils_1.0.tar.gz  broadgap.utils
问题2：

        Error in parse_Rd("/tmp/RtmpSQtp6t/R.INSTALL93473942656f/broadgap.utils/man/commandLineArg.Rd",  : 
        Unexpected end of input (in " quoted string opened at commandLineArg.Rd:35:31)
解决方法

        删除broadgap.utils/man/commandLineArg.Rd  文件内多余的引号
### 安装完成后，运行测试命令报错<br>
问题1：

        /media/sdb/user/wxm/software/Birdsuite/EXEDIR/birdsuite.sh: 
        line 40: /media/sdb/user/wxm/software/Birdsuite/EXEDIR/getAbsPath: No such file or directory
解决方法：
        
参考：https://www.linuxquestions.org/questions/linux-newbie-8/getabspath-attempting-to-run-birdsuite-833691/

        下载getAbsPath：http://sourceforge.net/projects/getabspath/
        安装
        make 然后将getabspath复制到EXEDIR
问题2：

        EXEDIR/apt-probeset-summarize.64: Permission denied
解决方法：

        cp ../../APT/apt-1.21.0-x86_64-intel-linux/bin/apt-probeset-summarize apt-probeset-summarize.64
        chmod 755 apt-probeset-summarize.64
 问题3：
        
        FATAL ERROR:Don't recognize option: 'mem-usage'可能APT版本更新，参数发生改变
        
解决方法：无法解决
        

        

        

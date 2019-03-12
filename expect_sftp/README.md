# expect_sftp
* linux expect安装

      yum install expect
* 基本语法

      set
      spawn 启动一个进程，后接要执行的命令
      expect 进程返回字符由该命令进行判断，是否与目标命令一致，若一致则继续
      send 向进程发送字符串，后接'\r'
      
* 示例

      #!/usr/bin/expect
      #执行期间有时间限制，该命令设置不限时间
      set timeout -1
      #链接sftp服务器
      spawn sftp -oPort=9910 971885129@hgsc-sftp1.hgsc.bcm.tmc.edu
      #判断返回字符
      expect "Password:"
      #输入密码
      send "011894Wang\n"
      #判断返回字符
      expect "sftp>"
      #输入现在命令
      send "get case_006/TCRBOA6-T-WGS.lane3.read2.fastq.bz2\n"
      #判断返回字符，若出现则代表下载完成
      expect "sftp>"
      #断开链接
      send "exit\n"
      #退出except
      expect eof

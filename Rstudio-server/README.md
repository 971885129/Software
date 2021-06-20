## 报错
### 问题1
* Ubuntu 18.4 Rstudio-server 启动报错

        缺少libssl.so.1.0.2
### 解决
* 安装新版openssl并将libssl.so 链接到/bin
* 安装rstudio-server 1.3

### 问题2
* 可打开rstudio登录界面，但无法登录
* 解决后登入，又无法安装R包，安装会导致崩溃
## 解决
* 删除~/.local/share/rstudio
* 删除~/.config/rstudio 
* 解决无法登入问题
* 对于无法安装R包，可能由于R版本问题，更换R4.1为R4.0（原使用R版本，后不知为何被4.1覆盖）
* 更换R版本后，将原R包安装路径加入环境变量

        查看当前Rstudio环境 Sys.getenv()[ grep("LIB|PATH", names(Sys.getenv())) ]
        创建~/.Renviron
        修改R包路径：R_LIBS_USER=/home/SXT/R/x86_64-pc-linux-gnu-library/4.0

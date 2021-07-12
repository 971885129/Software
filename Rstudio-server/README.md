## 使用
RStudio-server通过在两个配置文件中添加自定义语句进行配置（默认情况下，这两个配置文件可能不存在，则需要自己创建）

        /etc/rstudio/rserver.conf
        /etc/rstudio/rsession.conf
### 更改网络端口和地址
默认情况下，RStudio server的连接端口是8787，可以通过在rserver.conf中更改

        ## In /etc/rstudio/rserver.conf
        ## 更改端口为80
        www-port=80
默认情况下，RStudio绑定到地址0.0.0.0（接受来自任何远程IP的连接）。可以使用www-address条目修改此行为。例如：

        www-address=127.0.0.1
在更改/etc/rstudio/rserver.conf后，都需要重启server以更改配置

        $ sudo rstudio-server restart
### 外部库
通过修改rsession-ld-library-path 添加系统的库路径作为外部库以供RStudio server调用。有时候R需要依赖系统的一些库的时候，就可以添加上系统库的路径让R也可以调用到，例如：

        rsession-ld-library-path=/opt/local/lib:/opt/local/someapp/lib
### 更改RStudio-server使用的R版本
有时候系统上会装了多个版本的R，当我们想使用某个特定版本的R的时候就可以通过修改配置文件实现，例如

        rsession-which-r=/usr/local/bin/R
### 更改R包安装地址
通过修改r-libs-user可以更改用户的默认R包安装地址。这样的好处是确保最终用户安装的R包在路径中没有R版本号。 反过来，这使管理员可以在服务器上升级R版本而不用重置用户安装的软件包（如果安装的R包位于R版本派生的目录中，则会发生这种情况）。例如：

        r-libs-user=~/R/packages
### 更改默认镜像

        r-cran-repos=https://mirrors.nics.utk.edu/cran/

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

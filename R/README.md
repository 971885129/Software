#R 安装

## 报错

    checking curl/curl.h usability... yes
    checking curl/curl.h presence... yes
    checking for curl/curl.h... yes
    checking if libcurl is version 7 and >= 7.22.0... yes
    checking if libcurl supports https... no
    configure: error: libcurl >= 7.22.0 library and headers are required with support for https
* 解决

    #curl 加入环境变量
    export=/opt/curl-7.54.0/bin:$PATH

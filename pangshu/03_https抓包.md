


charles 与 fiddler 占用端口相同
    只能用其一，或者改端口





客户端 所在的 手机 系统代理 设置为 charles 帮助中的 localhost 地址

    proxy -> ssl proxy settings
        include
            add
                *
                443


    客户端(https) -> charles(https) -> 服务端(https)
        中间人
            证书
                help -> ssl -> install ...

    安装证书
        本地计算机
            自定义
                受信任的根证书颁发机构
                    确定
                        完成

    重启 charles





客户端(https) -> charles(http) -> 服务端(http)
    解包 -> 
        https -> http
        重新打包

    方便抓包



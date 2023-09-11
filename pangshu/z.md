
apktool
    d
    b
        注: 还没有签名


jadx-gui
    dex2jar

    jd-gui



App名称和图标的修改



包名 和 签名



应用入口壳
    EntryActivity -> MainActivity

    手写 smali
    手写 java -> smali -> 修改



https 抓包
    charles




如果没有签名校验
    1.通过加壳的形式或者log插桩获取
        类似添加入口类

    2.直接抽取so文件然后构建一个新app
        无法正确解压 apk
        新app的签名 与 原来app的签名 不一样，因为这是在没有签名检验的情况下
        包名 必须保持与原来一致，因为 so 中的函数名规则


如果app或者so库有签名校验
    1.使用ida工具静态分析so库
    2.使用xposed工具动态获取
        必须root

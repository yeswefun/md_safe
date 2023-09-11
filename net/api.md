


数据加密
    对称加密
        des, aes

    非对称加密
        rsa
        
        基于 非对称加密 算法生成 公钥 和 私钥
            公钥是通过私钥生成的
            私钥只能自己持有，公钥可以对外分发
            公钥加密只能由私钥解密
            私钥加密只能由公钥解密





客户端第一次身份验证
    account: 手机/邮箱/用户名
    secret: .... ....

    抓包 -> 明文，必须 加密


服务端
    "code": 0,
    "data": {
        "uid": 10000,
        "token": "63A9F0EA7BB98050796B649E85481845"
    }


客户端在身份验证成功后，第二次请求
    method: get
    api: http://域名/api/test
    uid
    ts
    sign

    使用 token 进行签名，必须保证 token 安全
    使用 签名 这种方式，可以在 客户端 接收 token 后，不再传输 token


服务端
    通过 uid 找到服务端 redis 中的 token







http://域名/api/test


客户端
    1.获取所有请求参数
        id=10000
        page=16
        size=32

    2.加入时间戳
        ts=123456

    3.将参数名称按照字母顺序排序
        id=10000&page=16&size=32&ts=123456

    4.在上一步得到字符串的最后拼接私钥
        appsecret=haha
        id=10000&page=16&size=32&ts=123456

        id=10000&page=16&size=32&ts=123456&appsecret=haha

    5.对上一步得到的字符串生成md5摘要
        签名信息 == md5(id=10000&page=16&size=32&ts=123456&appsecret=haha)

    6.将 签名信息 添加到请求参数字符串的最后
        签名信息 = md5(id=10000&page=16&size=32&ts=123456&appsecret=haha)
        id=10000&page=16&size=32&ts=123456

        id=10000&page=16&size=32&ts=123456&sign=签名信息
            注意: appsecret=haha 不在参数列表


服务端
    1.获取参数字符串
        id=10000&page=16&size=32&ts=123456&sign=签名信息

        id=10000&page=16&size=32&ts=123456
        sign=签名信息

    2.判断 签名 是否 过期
        当前ts - 参数ts > 30
            签名过期，返回响应

    3.拼接私钥
        appsecret=haha
        id=10000&page=16&size=32&ts=123456

        id=10000&page=16&size=32&ts=123456&appsecret=haha

    5.对上一步得到的字符串生成md5摘要
        服务端签名信息 == md5(id=10000&page=16&size=32&ts=123456&appsecret=haha)

    6.比较 服务端签名信息 和 sign的值 是否相等
        相等，ok
        不等, 签名错误





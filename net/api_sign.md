
http://域名/api/product/search?category=1000&hot=1


1 确保参数不被修改

2 确保接口访问者的合法性

3 确保请求的唯一性
    不能重复调用





确保参数不被修改
    算法A(category, hot, page, size) -> sign_value
        相同的输入，得到相同的输出 - 确保参数不被修改，category=1000&hot=1

        http://域名/api/product/search?category=1000&hot=1
            &sign=sign_value




确保接口访问者的合法性

    http://域名/api/product/search?category=1000&hot=1
        &appKey=abc
        &sign=sign_value

    客户端
        appKey=abc

    服务端
        appSecret=123
        对应客户端的 appKey=abc


    AccessKey: 客户端唯一标识
    SecretKey: 客户端密钥
        典型的是AppKey&AppSecret，或者ClientId&ClientSecret等





确保请求的唯一性

    http://域名/api/product/search?category=1000&hot=1
        &appKey=abc
        &ts=12345678
        &sign=sign_value

    ts=12345678
        时效性
        有效期: 30秒

    nonce=xxx
        30秒以内有效的 nonstr
            redis




签名(Signature) 放到 请求头(Header)



AppID：应用的唯一标识
AppKey：公匙（相当于账号）
AppSecret：私匙（相当于密码）
token：令牌（过期失效）




1、将全部请求的参数（包括GET和POST参数，和公共参数），并 排除sign参数
2、按参数名称按字母顺序排序
3、将排序好的参数对应的值，全部用字符串依次拼接起来
4、在最后追加app_secrect
5、进行md5
    并全部转换成大写
6、得到签名sign




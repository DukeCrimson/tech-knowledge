Token协议 JWT
JWT全称 json web token，适用于现在流行的分布式环境中。

传统的session是保存在服务器或者内存数据库中，JWT则是保存在客户端中。
JWT由三个部分组成，用.分隔。
Header Payload Signature

JWT通常看起来像这样： xxxxxx.yyyyyy.zzzzzz

①Header是请求头，由两部分组成，alg（算法）与typ（类型）。
    eg:{"alg":"HS256","typ":"JWT"}
②Payload是主体信息，用来存储JWT基本信息，或者是我们的信息。
    eg:{"sub":"123456789","name":"John Doe","admin":true}
③Signature主要是给第一部分和第二部分进行签名使用的，用来验证是否是我们服务器发起的Token，secret是我们的密钥。
    eg:使用HMAC SHA256算法进行签名
    HMACSHA256(
        base64UrlEncode(header) + "." +
        base64UrlEncode(payload),
        secret
    )
真正的JWT看起来像下面例子一样
eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJmb28iOiJiYXIiLCJpYXQiOjE1MTIyOTg4MDZ9.76mzRRk8CQfusjwxUMnIrME5ITyAPnNMdieJZhzaMc8

JWT工作原理：
1.Browser -> Server: post /users/login with username and password
2.Server:            creates a JWT with a secret
3.Server -> Browser: returns the JWT to the Browser
4.Browser -> Server: Sends the JWT on the Authorization Header
5.Server:            check JWT signature.Get user information from the JWT
6.Server -> Browser: sends response to the client



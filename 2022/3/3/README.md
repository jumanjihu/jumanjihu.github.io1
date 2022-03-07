
# sso原理推演
## 前置知识
### cookie-session机制
web单系统登录主要通过cookie-session机制，客户端登录后，服务端创建会话id , set到cookie中，并返回给web浏览器，后续浏览器带着会话id请求即代表处于这个登录会话中，不需要再次登录.

### http 302状态码
浏览器会自动识别并跳转http 302状态码报文指定的目标url。

### 自动跳转访问 
浏览器对302状态码http报文的处理行为，英文为redirect，专业词称为 重定向。

## 单系统登录机制
多系统登录需要借助单系统能力，单系统不做升级改造的情况下是这样.
(假设客户通过浏览器访问a.com域名url https://sample.a.com)
![image](https://user-images.githubusercontent.com/8491534/157072000-cf9f2d4c-f48e-472f-9952-c91cd56cbc4b.png)


## 多系统自动sso登录机制
对比多系统登录机制，我们需要增加一层职责服务统一管理登录状态，并且由于涉及多个域名的自动跳转，需要借助http 302状态码能力。
那么系统链路演化为（增加b.com域名服务以说明多系统场景）
![image](https://user-images.githubusercontent.com/8491534/157084639-7ab853af-c1aa-41ab-b84f-7cf3b5465880.png)
这就有个问题，就是第8步怎么sso登录成功后怎么知道跳转的url，需要把这个信息带到链路上来，因此有了下图
![image](https://user-images.githubusercontent.com/8491534/157087155-1c193073-e645-4205-a25a-b0c4c4df58af.png)

这里又有个问题，sso登录成功后跳转302的a.com的服务url怎么校验登录状态，需要把登录信息带到链路上，直观简单的做法带个参数?login=true，但这样很明显不安全，需要加密，可以通过一个随机字串识别登录身份。这样很自然的我们就想到了令牌共享校验登录信息，因此推演了下图
![image](https://user-images.githubusercontent.com/8491534/157087589-f7f526f1-6cd2-4153-9ac2-5f2acc9ada3a.png)


至此sso流程推演完毕



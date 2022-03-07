
# sso原理

## 单系统登录机制
### cookie-session机制
web单系统登录主要通过cookie-session机制，客户端登录后，服务端创建会话id set到cookie中，并返回给web浏览器，后续浏览器带着会话id请求即代表处于这个登录会话中，不需要再次登录

## 多系统登录机制
cookieA -- 系统A  --302---未登录sso cookie --sso是否登录 --登录--设置sso cookie--302--原地址
cookieB -- 系统B  --302-- 登录sso cookie  --sso是否登录 --是 --302--原地址

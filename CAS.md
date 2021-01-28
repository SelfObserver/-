# 开源单点登录系统CAS

## 单点登录Single Sign On
SSO的定义是在多个系统中，用户只需要登录一次就可以访问所有相互信任的应用系统。

## 什么是CAS
CAS是yale大学的发起的一个开源项目，旨在为web应用系统提供一种可靠的单点登录方法。

## CAS的特点

1. 开源的企业级单点登录解决方案
2. CAS Server为需要独立部署的Web应用
3. CAS Client支持非常多的客户端，包括JAVA,.Net,PHP,Ruby等。

## CAS Server和CAS Client
CAS Server需要独立部署，主要负责对用户的认证工作：CAS Client 负责对客户端受保护资源的访问请求，需要登录时，重定向到CAS Server。

## SSO 单点登录访问流程主要有以下步骤
1. 访问服务：SSO客户端发送请求访问应用系统提供的服务资源
2. 定向认证：SSO客户端会重定向用户请求到SSO服务器
3. 用户认证：用户身份认证
4. 发放票据：SSO服务器会产生一个随机的Service Ticket
5. 验证票据：SSO服务器验证票据Service的合法性，验证通过后，允许客户端访问服务。
6. 传输用户信息：SSO服务器验证票据通过后，传输用户认证结果信息给客户端

## CAS服务端部署

CAS服务端就是一个war包，配置到tomcat目录下，启动tomcat自动解压war包。

默认用户名和密码 casuer/Mello

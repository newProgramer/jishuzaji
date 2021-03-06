前后端分离是通过Nginx+Tomcat的方式\(也可以在中间加一个NodeJS\)进行有效的解耦

###### 核心思想是前端html页面通过ajax调用后端的restful api接口并使用json进行数据交互

### 目的

* 使前后端开发人员分离专注于自己的技术方向
* 减轻后端服务器的压力

### 正常的互联网架构

* web服务器集群
* 应用服务器集群
* 文件服务器集群
* 数据库服务器集群
* 消息队列集群
* 缓存集群等

### 前后端分离优势

* 动静分离,加快响应速度
* 快速定位问题
* 高并发
* 减少后端服务器压力
* 代码可维护性与易读性强
* 代码复用性强
* 扩展性强

### 注意事项

* 开会讨论需求要明确
* 制定好接口文档
* 后端工程师写好测试用例
* 前后端都能做的事尽量放在前端
* 前端需要机制应对后端请求超时以及宕机等情况
* 前后端是两个项目需要分开部署




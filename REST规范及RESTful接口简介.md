# REST规范及RESTFul接口简介

1、了解什么是接口？API（Application Program Interface）

2、REST restful

REST是一种规范，规定一种接口的标准、要素。
restful是遵守rest接口规范的接口程序。



API设计六要素

前端 资源路径（URI）-- http动词（METHOD）-- 过滤信息（query_string）
后端 响应状态码（status_code） -- 错误处理 （Error） -- 返回结果（Result）



3、资源路径（URI）
统一资源标识符
URI = URL + URN

URL统一资源定位符
URN统一资源名称

协议-主机名称（端口号）-路径-参数



4、http动词
GET              获取一项或多项数据记录
POST            新增数据
PUT 修改      修改数据
DELETE 删除 删除数据



5、过滤信息
参数



6、状态码
http状态码

下面列出了GET，DELETE，PUT和POST的典型用法：

```shell
200  OK 操作成功，返回数据
201  create 新建成功
204  not content 删除成功
400  bad request 请求语法错误
403  forbidden 没有权限访问资源
404  not found 资源不存在

GET
200（OK）- 操作成功，返回数据
204（无内容）- 资源有空表示
301（Moved Permanently）- 资源的URI已被更新
303（See Other）- 其他（如，负载均衡）
304（not modified）- 资源未更改（缓存）
400（bad request）- 指代坏请求（如，参数错误）
404（not found）- 资源不存在
406（not acceptable）- 服务端不支持所需表示
500（internal server error）- 通用错误响应
503（Service Unavailable）- 服务端当前无法处理请求

POST
200（OK）- 如果现有资源已被更改
201（created）- 如果新资源被创建
202（accepted）- 已接受处理请求但尚未完成（异步处理）
301（Moved Permanently）- 资源的URI已被更新
303（See Other）- 其他（如，负载均衡）
400（bad request）- 指代坏请求
404（not found）- 资源不存在
406（not accepted）- 服务端不支持所需表示
409（conflict）- 通用冲突
412（Precondition Failed）- 前置条件失败（如执行条件更新时的冲突） 
415（unsupported media type）- 接收到的表示不受支持
500（internal server error）- 通用错误响应
503（Service Unavailable）- 服务端当前无法处理请求

PUT
200（OK）- 如果已存在资源被更改
201（created）- 如果新资源被创建
301（Moved Permanently）- 资源的URI已更改
303（See Other）- 其他（如，负载均衡）
400（bad request）- 指代坏请求
404（not found）- 资源不存在
406（not accepted）- 服务端不支持所需表示
409（conflict）- 通用冲突
412（Precondition Failed）- 前置条件失败（如执行条件更新时的冲突） 
415（unsupported media type）- 接收到的表示不受支持
500（internal server error）- 通用错误响应
503（Service Unavailable）- 服务端当前无法处理请求

DELELE
200（OK）- 资源已被删除
301（Moved Permanently）- 资源的URI已更改
303（See Other）- 其他（如，负载均衡）
400（bad request）- 指代坏请求
404（not found）- 资源不存在
409（conflict）- 通用冲突
500（internal server error）- 通用错误响应
503（Service Unavailable）- 服务端当前无法处理请求
```





7、错误信息



8、结果集
{"code":200,"msg":"新增数据成功",data:{"id":1,......}}



9、Restful接口的路由格式
GET  http://www.test.com/news        数据列表
GET  http://www.test.com/news/:id   读取一条数据
POST http://www.test.com/news       添加一条数据
PUT  http://www.test.com/news/:id   修改一条数据
DELETE  http://www.test.com/news/:id   删除一条数据



10、tp5中的资源路由
以tp5.1的资源路由为例
具体看tp5.1手册资源路由文档



11、体验restful接口设计
用postman模拟请求tp5.1资源路由



12、会使用jQuery的ajax请求Restful接口
知道看浏览器的请求头和响应头
注意ajax的data和路由格式的匹配

```javascript
$("#update").click(function () {
    $.ajax({
        url: "http://www.test.com" + "/news/3",
        type: "put",
        dataType: "json",
        success: function (res) {
            console.log(res);
        }
    }) 
});

$("#delete").click(function () {
    $.ajax({
        url: "http://www.test.com" + "/news/3",
        type: "delete",
        dataType: "json",
        success: function (res) {
            console.log(res);
        }
    }) 
});
```





13、请求伪装
表单隐藏域

```html
<input type="hidden" name="_method" value="PUT">
```

```html
<form action="a.php" method="post">
    <input type="text" name="username" value="奔牛课堂" id="" />
    <input type="hidden" name="_method" value="PUT" />
    <input type="button" value="提交" />
</form>
```







ajax实现伪装
修改data即可
post-to-delete
data:"_method=delete"


# 接口规范   

M：怎么区别api请求和页面请求?

Z：以/api开头，普通请求体格式如下

```properties
POST http://{IP}:{PORT}/{PROJECT_CONTEXT}/api/user/add HTTP/1.1
Accept:application/json, text/plain, */*
Content-Type: application/x-www-form-urlencoded;charset=utf-8
name=jack&password=123456
```

三个必须：PAC        

M：普通的接口请求跟RESTful的接口请求有什么区别呢？

Z：一些三方不同

1. 最后一项Content-Type不同，RESTful的如下

   ```properties
   #请求体
   POST http://{IP}:{PORT}/{PROJECT_CONTEXT}/api/user HTTP/1.1
   Accept:application/json, text/plain, */*
   Content-Type: application/json;charset=utf-8
   {
      "name":"jack",
      "password":"123456"
   }
   ```

2. 前缀后缀的作用不同，普通的只有POST和GET，改变的是``{PROJECT_CONTEXT}/api/user/add``最后一个方法名

   ```properties
   GET http://{IP}:{PORT}/{PROJECT_CONTEXT}/api/user/detail?id=10001 HTTP/1.1
   ```

   ```properties
   GET http://{IP}:{PORT}/{PROJECT_CONTEXT}/api/user/list HTTP/1.1
   ```

   RESTful的前缀有多种，POST 、DELETE 、GET、PUT，后缀只有单个和多个的区别

   ```properties
   GET http://{IP}:{PORT}/{PROJECT_CONTEXT}/api/user/10001 HTTP/1.1
   ```

   ```properties
   GET http://{IP}:{PORT}/{PROJECT_CONTEXT}/api/user HTTP/1.1
   ```

3. Content-Type不同，编码方式从x-www-form-urlencoded到json

   ```properties
   Content-Type: application/x-www-form-urlencoded;charset=utf-8
   ```

   ```properties
   Content-Type: application/json;charset=utf-8
   ```

M：响应体的格式是怎么样的呢？

Z：响应体的格式如下：

```json
响应头:
HTTP/1.1 200 OK
Content-Type: application/json

响应体:
{
	"status": 200,
	"desc": "执行成功",
	"time": "20160513131050", 
	"data": {
		"id":1308,
    	"name":"alan",
    	"age":20
	}
}
```

四个必须：sdtd

M：那如果是分页插件的响应体呢？

Z：添加一个apge键    

```json
响应头:
HTTP/1.1 200 OK
Content-Type: application/json
响应体:
{
"status":200,
"desc":"执行成功",
"time": "20160513131050",
"pager":{
    "pageIndex":2,
    "pageSize":20,
    "pageCount":13,
    "itemCount":256
},
"data":[
    {
        "id":1308,
        "name":"alan",
        "age":20
    },
    ...
 ]
}
```

M：常用的状态码有哪些呢？

Z：主要是0,1,3接触的比较少

| 状态码（status） | 描述                                           |
| ---------------- | ---------------------------------------------- |
| 200 OK           | GET、POST、PUT、DELETE请求成功执行，并返回Json |
| 400 Bad Request  | 参数缺失（比如name没有传递）或参数校验错误     |
| 401 Unauthorized | 缺失鉴权信息（不满足OAuth2或Session）          |
| 403 Forbidden    | 操作不允许（比如用户没有权限删除指定信息）     |
| 404 Not Found    | 资源无法访问/不存在（比如没有用户的id为25）    |
| 500 Server Error | 服务器端发生错误（比如数组超界等）             |

M：业务状态码是什么？

Z：当接口状态码不够用的时候，在data中添加code字段，自定义状态码和状态信息   

```json
响应体:
{
	"status": 200,
	"desc": "操作成功",
    "data":{
        "message": "登录成功，但是密码强度不够",
        "code": 10700
    }
}
```

M：Http接口鉴权怎么做？

Z：使用OAuth 2 tokens、Session，响应体方式如下,少了status和data：

```json
响应头:
HTTP/1.1 200 OK
Content-Type: application/json
响应体: 
{
    "status":  401,
    "desc": "Unauthorized"
}
```

M：400的http响应体呢？

Z：如下

```json
响应头:
HTTP/1.1 200 OK
Content-Type: application/json
响应体: 
{
    "status":  400,
    "desc": "[name] not given"
}
```
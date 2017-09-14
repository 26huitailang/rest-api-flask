# rest-api-flask

## 简介
本项目源自我在Udemy上学习的内容，放在这里为大家作为入门学习的参考和学习，欢迎大家通过邮件的形式和我交流，邮箱 26huitailang@gmail.com。

## 内容概览

### section3
理解什么是REST，Stateless在这里是什么意思，使用postman测试你的API。

REST（Resource Representational State Transfer）是一种思考Web Server如何响应requests的方法，不是特定的某种编程工具，更像是一种风格。在交互中，服务器根据方法操作**resouces**，类似OOP，服务器有resouces，每个资源都能与对应的方法（HTTP Verbs）相互作用。

REST应该是Stateless的，首先明白资源是服务器上的一个实体，它呈现的形式（可以理解为格式）叫做表现层。每次对资源的操作往往会带来表现层的状态转化。那么无状态的意思就是每次操作请求不依赖于其他任何请求，结合服务器就是，服务器只知道当前的请求，而不知道之前任何的请求。e.g.

    POST /item/chair 这是创建一个item，服务器仅仅知道POST这个请求，但是这次请求中，服务器不知道这个数据是否已经在数据库中了。
    GET /item/chair 这个操作是去DB中看看item是不是在这里了。但是我们在查看之前，并不必须绑定POST创建这个操作，因为可能在之前的操作已经存在了。

    比如服务器不记录用户的登录状态，不知道用户是否已经登录，那么用户的每次请求服务器都会用一个唯一的字符串去标示（Token），方便服务器将之与特定的用户联系起来。（这个在section4中有使用Flask_JWT的例子）

### section4

通过class来实现RESTful应用。包括:
- 错误的处理，通过next返回None，判定并返回相应的状态码和信息
- 返回的状态码和信息，return的信息后面带上对应的状态码
- 用户的授权，使用Flask_JWT实现，返回认证用户相应的token，通过@jwt_required()装饰器限制一些API的请求，正确的token才能通过
- 数据的过滤，Flask_RESTful的reqparse构建parser，符合要求的数据才能通过

### section5

这部分加入了数据库，使用的是SQLite，使数据持久化，这样即使停止app数据也不会丢失，并修改对应的item的操作，将item独立为单独文件，一方面方便配置管理，一方面是python每次import文件时，都会运行文件，所以尽量不放到app.py中。

### section6

这部分尝试用ORM工具--SQLAlchemy，对于关系型数据库都能通过它将数据库映射为一个程序对象，在操作中像访问对象和方法一样非常方便。


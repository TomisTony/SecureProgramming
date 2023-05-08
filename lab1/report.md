# 安全编程技术-课程报告-Lab1

[TOC]

## Lab1.1

### 安装Java环境

![image-20230426110028556](assets/image-20230426110028556.png)

如图所示，本机在实验之前已安装JDK

### 安装Tomcat

- 下载Tomcat-10.1.8

![image-20230426110806885](assets/image-20230426110806885.png)

- 配置环境变量

根据RUNNING.txt中的步骤设置环境变量

![image-20230426113309509](assets/image-20230426113309509.png)

- 启动Tomcat成功

![image-20230426113413444](assets/image-20230426113413444.png)

- 解决Tomcat乱码

修改`TomcatFolder/conf/logging.properties`中的`java.util.logging.ConsoleHandler.encoding`为GBK即可

再次启动发现已无乱码

![image-20230426113734530](assets/image-20230426113734530.png)

### 安装eclipse

征得助教同意之后使用IDEA替代eclipse。

本机在实验之前已经安装IDEA。

新建项目并运行HelloWorld成功

![image-20230426135122101](assets/image-20230426135122101.png)

## Lab1.2

### 应用场景

一个用户登录与注册的界面。

用户可以在界面上输入账号密码登录，登录成功之后页面会有提示。

用户可以在界面上输入账号和两次密码注册，要求注册密码和二次输入的密码相同。

app采用前后端分离的架构，前端准备使用原生html+css+js，后端准备使用node.js配koa-router。

### 创建数据库

建`user`表

![image-20230505112153410](assets/image-20230505112153410.png)

表中有一个自增主键`iduser`，以及对应的用户`uname`和`password`。

![image-20230505112121541](assets/image-20230505112121541.png)

### 开发

#### 前端

前端采用原生html+css+js

html的主体是两个form，以登录的form为例：

```html
<div class="card">
    <div class="title">Login</div>
    <form>
        <input id="login-uname" required type="text" placeholder="user name" />
        <input id="login-pd" required type="password" placeholder="password" />
        <button class="button login-button">login</button>
    </form>
</div>
```

主要采用了flex布局

在javascript中取消了原生的表单提交，转而给按钮绑定自定义的提交事件。

以login按钮的为例：

```js
function login() {
    //使用ES6自带的fetch发送网络请求
}

//取消原生表单提交事件
const forms = document.querySelectorAll('form');
forms.forEach(form => form.addEventListener('submit', function(event) {
    event.preventDefault();
}))

//给按钮添加自定义提交事件
let loginButton = document.querySelector('.login-button');
loginButton.addEventListener('click', login);
```

#### 后端

后端采用node.js+koa-router。

后端连接本地数据库，配置`/login`和`/register`两个路由。

采用CORS中间件解决前后端跨域问题。

await被Promise包裹的query语句达到同步执行数据库查询的功能。

#### API list

详见源码文件夹中`README.md`

### 部署WebAPP

#### 一点小插曲（服务器部署）

刚开始准备直接部署在自己的服务器上：

- 在服务器上按照Lab1.1搭建使用tomcat

![image-20230426153253739](assets/image-20230426153253739.png)

- 设置服务器防火墙8080端口开放，在浏览器中尝试访问

![image-20230426153400768](assets/image-20230426153400768.png)

可见Tomcat配置成功

虽然搞好了服务器上的配置，过了几天发现服务器上的mysql由于密码太简单被攻击了（X

![image-20230505105111664](assets/image-20230505105111664.png)

考虑到后续重新配好数据库也有再次被攻击导致后端崩溃的可能，遂决定部署在本地。

#### 本地部署

！



TODO



！

### 测试

#### 注册

##### 正常注册



##### 用户名已存在



##### 两次密码输入不一致



#### 登录

##### 正常登录



##### 用户名不存在



##### 密码错误

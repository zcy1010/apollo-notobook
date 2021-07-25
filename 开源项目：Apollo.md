# 开源项目：Apollo

## 简介

### 产生原因

* 随着程序功能的日益复杂，程序的配置日益增多：各种功能的开关、参数的配置、服务器的地址等。
* 对程序配置的期望值也越来越高：配置修改后实时生效，分环境、分集群管理配置，完善的权限、审核机制等
* 在这样的大环境下，传统的通过配置文件、数据库等方式已经越来越无法满足开发人员对配置管理的需求。

### 简介

 Apollo（阿波罗）是携程框架部门研发的配置管理平台，能够集中化管理应用不同环境、不同集群的配置，配置修改后能够实时推送到应用端，并且具备规范的权限、流程治理等特性。
​ 服务端基于Spring Boot和Spring Cloud开发，打包后可以直接运行，不需要额外安装Tomcat等应用容器。
​ Java客户端不依赖任何框架，能够运行于所有Java运行时环境，同时对Spring环境也有较好的支持。.Net客户端不依赖任何框架，能够运行于所有.Net运行时环境。

# 开源项目：Apollo

## 简介

### 产生原因

* 随着程序功能的日益复杂，程序的配置日益增多：各种功能的开关、参数的配置、服务器的地址等。
* 对程序配置的期望值也越来越高：配置修改后实时生效，分环境、分集群管理配置，完善的权限、审核机制等
* 在这样的大环境下，传统的通过配置文件、数据库等方式已经越来越无法满足开发人员对配置管理的需求。

### 简介

 Apollo（阿波罗）是携程框架部门研发的配置管理平台，能够集中化管理应用不同环境、不同集群的配置，配置修改后能够实时推送到应用端，并且具备规范的权限、流程治理等特性。
​ 服务端基于Spring Boot和Spring Cloud开发，打包后可以直接运行，不需要额外安装Tomcat等应用容器。
​ Java客户端不依赖任何框架，能够运行于所有Java运行时环境，同时对Spring环境也有较好的支持。.Net客户端不依赖任何框架，能够运行于所有.Net运行时环境。

## 部署

### 环境准备

#### Java

Java1.8以上。

![image-20210723181540065](C:\Users\zcy\AppData\Roaming\Typora\typora-user-images\image-20210723181540065.png)

#### mySQL

5.6以上

![image-20210723181907378](C:\Users\zcy\AppData\Roaming\Typora\typora-user-images\image-20210723181907378.png)

### Apollo-quick-start 下载

仓库下载

![image-20210723182235637](C:\Users\zcy\AppData\Roaming\Typora\typora-user-images\image-20210723182235637.png)![image-20210723182259368](C:\Users\zcy\AppData\Roaming\Typora\typora-user-images\image-20210723182259368.png)

![image-20210723182306078](C:\Users\zcy\AppData\Roaming\Typora\typora-user-images\image-20210723182306078.png)

### 创建数据库

#### 创建ApolloPortalDB

![image-20210723212716986](C:\Users\zcy\AppData\Roaming\Typora\typora-user-images\image-20210723212716986.png)

![image-20210723212858681](C:\Users\zcy\AppData\Roaming\Typora\typora-user-images\image-20210723212858681.png)

#### 创建ApolloConfigDB

![image-20210723213007694](C:\Users\zcy\AppData\Roaming\Typora\typora-user-images\image-20210723213007694.png)

![image-20210723213100158](C:\Users\zcy\AppData\Roaming\Typora\typora-user-images\image-20210723213100158.png)

### 启动Apollo配置中心

#### 确定端口未占用

Quick Start脚本会在本地启动3个服务，分别使用8070, 8080, 8090端口，请确保这3个端口当前没有被使用。

![image-20210723213425940](C:\Users\zcy\AppData\Roaming\Typora\typora-user-images\image-20210723213425940.png)

3个端口均为占用

执行./sh文件，发现不能执行sh文件

处理方法：

* 在windows下想要执行shell脚本，需要使用到"Git Bash"，所以我们需要先安装Git。
* 配置Git环境变量

但是最终启动失败

![image-20210723214645328](C:\Users\zcy\AppData\Roaming\Typora\typora-user-images\image-20210723214645328.png)

查看Apollo-service.log 日志后，发现

![image-20210723215436668](C:\Users\zcy\AppData\Roaming\Typora\typora-user-images\image-20210723215436668.png)

MySQL相关配置不正确：

修改后如下：

![image-20210723215120334](C:\Users\zcy\AppData\Roaming\Typora\typora-user-images\image-20210723215120334.png)

启动成功：

![image-20210723215520020](C:\Users\zcy\AppData\Roaming\Typora\typora-user-images\image-20210723215520020.png)

成功启动：

1. 输入用户名apollo，密码admin后登录

![image-20210723215618921](C:\Users\zcy\AppData\Roaming\Typora\typora-user-images\image-20210723215618921.png)

![image-20210723215648000](C:\Users\zcy\AppData\Roaming\Typora\typora-user-images\image-20210723215648000.png)

### 启动客户端程序

准备了一个简单的Demo客户端来演示从Apollo配置中心获取配置。

程序很简单，就是用户输入一个key的名字，程序会输出这个key对应的值。

如果没找到这个key，则输出undefined。

同时，客户端还会监听配置变化事件，一旦有变化就会输出变化的配置信息。

运行`./demo.sh client`启动Demo客户端，忽略前面的调试信息，可以看到如下提示：

![image-20210723220018324](C:\Users\zcy\AppData\Roaming\Typora\typora-user-images\image-20210723220018324.png)

输入`timeout`，会看到如下信息：

![image-20210723220039612](C:\Users\zcy\AppData\Roaming\Typora\typora-user-images\image-20210723220039612.png)

在配置界面点击timeout这一项的编辑按钮

![image-20210723220124898](C:\Users\zcy\AppData\Roaming\Typora\typora-user-images\image-20210723220124898.png)

点击发布按钮，并填写发布信息

![image-20210723220147084](C:\Users\zcy\AppData\Roaming\Typora\typora-user-images\image-20210723220147084.png)

![image-20210723220207235](C:\Users\zcy\AppData\Roaming\Typora\typora-user-images\image-20210723220207235.png)



客户端一直在运行的话，在配置发布后就会监听到配置变化，并输出修改的配置信息：

![image-20210723220235624](C:\Users\zcy\AppData\Roaming\Typora\typora-user-images\image-20210723220235624.png)

再次输入`timeout`查看对应的值，会看到如下信息：

![image-20210723220319767](C:\Users\zcy\AppData\Roaming\Typora\typora-user-images\image-20210723220319767.png)

接入新的apollo

//TODO

# Apollo 框架介绍

下图是Apollo的作者宋顺给出的架构图：

![image-20210724220918673](C:\Users\zcy\AppData\Roaming\Typora\typora-user-images\image-20210724220918673.png)

![overall-architecture](https://raw.githubusercontent.com/ctripcorp/apollo/master/doc/images/overall-architecture.png)

## 四个核心模块及其主要功能

1. **ConfigService**

2. - 提供配置获取接口
   - 提供配置推送接口
   - 服务于Apollo客户端

3. **AdminService**

4. - 提供配置管理接口
   - 提供配置修改发布接口
   - 服务于管理界面Portal

5. **Client**

6. - 为应用获取配置，支持实时更新
   - 通过MetaServer获取ConfigService的服务列表
   - 使用客户端软负载SLB方式调用ConfigService

7. **Portal**

8. - 配置管理界面
   - 通过MetaServer获取AdminService的服务列表
   - 使用客户端软负载SLB方式调用AdminService

## 三个辅助服务发现模块

1. **Eureka**

2. - 用于服务发现和注册
   - Config/AdminService注册实例并定期报心跳
   - 和ConfigService住在一起部署

3. **MetaServer**

4. - Portal通过域名访问MetaServer获取AdminService的地址列表
   - Client通过域名访问MetaServer获取ConfigService的地址列表
   - 相当于一个Eureka Proxy
   - 逻辑角色，和ConfigService住在一起部署

5. **NginxLB**

6. - 和域名系统配合，协助Portal访问MetaServer获取AdminService地址列表
   - 和域名系统配合，协助Client访问MetaServer获取ConfigService地址列表
   - 和域名系统配合，协助用户访问Portal进行配置管理

更详细的介绍可见https://mp.weixin.qq.com/s/-hUaQPzfsl9Lm3IqQW3VDQ

# Apollo模块（第五天）

## Config Service

- 提供配置获取接口
- 提供配置更新推送接口（基于Http long polling）
  - 服务端使用[Spring DeferredResult](http://docs.spring.io/spring/docs/current/javadoc-api/org/springframework/web/context/request/async/DeferredResult.html)实现异步化，从而大大增加长连接数量
  - 目前使用的tomcat embed默认配置是最多10000个连接（可以调整），使用了4C8G的虚拟机实测可以支撑10000个连接，所以满足需求（一个应用实例只会发起一个长连接）。
- 接口服务对象为Apollo客户端

## Admin Service

- 提供配置管理接口
- 提供配置修改、发布等接口
- 接口服务对象为Portal

## Meta Server

- Portal通过域名访问Meta Server获取Admin Service服务列表（IP+Port）
- Client通过域名访问Meta Server获取Config Service服务列表（IP+Port）
- Meta Server从Eureka获取Config Service和Admin Service的服务信息，相当于是一个Eureka Client
- 增设一个Meta Server的角色主要是为了封装服务发现的细节，对Portal和Client而言，永远通过一个Http接口获取Admin Service和Config Service的服务信息，而不需要关心背后实际的服务注册和发现组件
- Meta Server只是一个逻辑角色，在部署时和Config Service是在一个JVM进程中的，所以IP、端口和Config Service一致

##  Eureka

- 基于[Eureka](https://github.com/Netflix/eureka)和[Spring Cloud Netflix](https://cloud.spring.io/spring-cloud-netflix/)提供服务注册和发现
- Config Service和Admin Service会向Eureka注册服务，并保持心跳
- 为了简单起见，目前Eureka在部署时和Config Service是在一个JVM进程中的（通过Spring Cloud Netflix）

## Portal

- 提供Web界面供用户管理配置
- 通过Meta Server获取Admin Service服务列表（IP+Port），通过IP+Port访问服务
- 在Portal侧做load balance、错误重试

##  Client

- Apollo提供的客户端程序，为应用提供配置获取、实时更新等功能
- 通过Meta Server获取Config Service服务列表（IP+Port），通过IP+Port访问服务
- 在Client侧做load balance、错误重试

# Apollo E-R Diagram(第六天)

## 主体E-R Diagram

- App
  - App信息
- AppNamespace
  - App下Namespace的元信息
- Cluster
  - 集群信息
- Namespace
  - 集群下的namespace
- Item
  - Namespace的配置，每个Item是一个key, value组合
- Release
  - Namespace发布的配置，每个发布包含发布时该Namespace的所有配置
- Commit
  - Namespace下的配置更改记录
- Audit
  - 审计信息，记录用户在何时使用何种方式操作了哪个实体。

## 权限相关E-R Diagram

## 主体ER图

![image-20210725212026406](C:\Users\zcy\AppData\Roaming\Typora\typora-user-images\image-20210725212026406.png)

- App
  - App信息
- AppNamespace
  - App下Namespace的元信息
- Cluster
  - 集群信息
- Namespace
  - 集群下的namespace
- Item
  - Namespace的配置，每个Item是一个key, value组合
- Release
  - Namespace发布的配置，每个发布包含发布时该Namespace的所有配置
- Commit
  - Namespace下的配置更改记录
- Audit
  - 审计信息，记录用户在何时使用何种方式操作了哪个实体。

## 权限ER图

![image-20210725212141913](C:\Users\zcy\AppData\Roaming\Typora\typora-user-images\image-20210725212141913.png)

- User
  - Apollo portal用户
- UserRole
  - 用户和角色的关系
- Role
  - 角色
- RolePermission
  - 角色和权限的关系
- Permission
  - 权限
  - 对应到具体的实体资源和操作，如修改NamespaceA的配置，发布NamespaceB的配置等。
- Consumer
  - 第三方应用
- ConsumerToken
  - 发给第三方应用的token
- ConsumerRole
  - 第三方应用和角色的关系
- ConsumerAudit
  - 第三方应用访问审计
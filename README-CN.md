# my-repo  

最后更新时间: 05/09/2021

下面是我正在开发的项目，当你尝试编译和运行我的项目的时候，请尽可能使用 `main` or `master` 分支，我会尽可能让主分支稳定可运行。部分项目会依赖于我写的模块，为了编译通过，你需要使用 Maven 手动 `install` 这些项目。大量的模块可能会看起来比较混乱，因为没能从中央仓库自动拉取，但是模块化是为了让我能写出重复使用的代码和功能，提高开发效率。这个 README 的第一个部分会讲我目前正在开发或维护的项目，第二个部分会讲我写的一些公用模块，在最后一部分，会讲一些我很久以前写的已经存档的项目。

# 1. 服务和网络应用 

## 1.1 Auth-Service

该项目包含两个应用:

- auth-service
- auth-service-web

在 `auth-service/` 中的是一个用于用户身份识别 (登陆)， 管理用户角色信息，记录登陆信息 (例如， IP 地址) 和操作信息 (例如，接口调用名称，参数等) 的服务。该服务提供 **Dubbo** RPC 调用的接口。一个带有 controller 层，需要登陆的 webapp 可以使用 **Auth-Module** 模块来集成该服务。

在 `auth-service-web` 中的是一个 webapp，用于提供 REST 接口 给客户端与 `auth-service` 中的服务进行交流，该服务类似一个 Gateway。一个 **Angular** 前端单页面应用已经写好，用于与该 webapp 交互。

连接: https://github.com/CurtisNewbie/auth-service

## 1.2 File-Server 

一个托管文件上传下载的 webapp，已经通过使用 **Auth-Module** 与 **Auth-Service** 集成。同样的，一个 **Angular** 前端单页面已经写好，用于与该 webapp 交互。

连接: https://github.com/CurtisNewbie/file-server

## 1.3 Chat-Service 

一个用于在线聊天的 webapp. 聊天，房间列表等功能都是基于 Redis 和 Websocket 的，所以房间内的信息并不是持久化的。同样的，一个 **Angular** 前端单页面已经写好，用于与该 webapp 交互。

连接: https://github.com/CurtisNewbie/chat-service

## 1.4 TodoApp 

一个用于管理 todo 的 **JavaFx** 应用，数据存储是基于 **SQLite** 的。可能 UI 不是特别好看，但实际上我每天都在使用。

link: https://github.com/CurtisNewbie/todoapp

# 2. BOM 

一个用于管理项目和模块直接依赖版本的 BOM (Bill of Material) 文件，几乎所有正在开发和维护的项目和模块都有使用它。如果你正在尝试编译运行其中的一个项目，你可能需要使用 Maven 手动 `install` 这个 BOM.

link: https://github.com/CurtisNewbie/curtisnewbie-bom

# 3. 模块 

为了提高代码重用，提高开发效率，我写了下面的这些模块。因为没有将这些模块发布到 Maven 仓库中，你只能手动的进行 `maven install`. 当我在开发服务或网络应用的时候，这些模块也会一同改变和提升，所以即使这些模块可能看起来比较基础，但它们会逐步包含更多的功能。

## 3.1 Auth-Module

用于与 **Auth-Service** 集成的和用户身份认证的模块. **Auth-Service** 在上面有提到，是用于管理用户信息和身份认证的服务，该模块通过实现 `AuthenticationProvider` 与 Spring Security 集成，并且在该实现中使用 **Dubbo** 远程调用 **Auth-Service** 的 API 来校验用户的登陆信息。同时，该模块也是负责收集并发送用户登陆信息和接口调用信息到 **Auth-Service** 的。

link: https://github.com/CurtisNewbie/auth-module

## 3.2 Transactional-Outbox-Module

一个对 **事务性发件箱 (Transactional-Outbox)** 模式的基于 polling publisher 的实现。当使用该模块时，只有当事物提交以后，该事件内的消息才会被发送到中间件中。

link: https://github.com/CurtisNewbie/transactional-outbox-module

## 3.3 Distributed-Task-Module

基于 Quartz 和 Redis 实现的简单的分布式定时任务的模块。

link: https://github.com/CurtisNewbie/distributed-task-module

## 3.4 Log-Tracing-Module 

基于 MDC 的日志追踪模块，支持 **Dubbo** 的远程调用。

link: https://github.com/CurtisNewbie/log-tracing-module

## 3.5 Messaging-Module 

用于使用 RabbitMQ 的异步消息模块. 该模块主要用于减少重复代码，提供了一些较方便的服务 API 和监听器的 adapter。

link: https://github.com/CurtisNewbie/messaging-module

## 3.6 Redis-Util-Module 

基于 **Redisson** 的模块，用于简化使用 **Redisson** 的代码，减少部分代码重复。但是该模块只用于简单的场景，对于较复杂的场景，我仍会直接使用 **Redisson**，例如, **Chat-Service**.

link: https://github.com/CurtisNewbie/redis-util-module

## 3.7 Common-Module

该服务包含常用的工具类。

link: https://github.com/CurtisNewbie/common-module

## 3.8 Service-Module 

该模块用于引入使用 **Dubbo** 和 **Nacos** 所需要的依赖关系，实际上该模块只包含一个 pom 文件。

link: https://github.com/CurtisNewbie/service-module

# 4. Archived Projects

## 4.1 MediaHoster 

一个支持流媒体文件扫描和流媒体播放的 webapp。使用 **Quarkus** 实现，并且支持 *byte-range* 请求 (指的是数据按请求的范围进行返回, 主要用于流媒体播放). 一个 **Angular** 前端和一个 **Android TV** 应用已经编写好用于与该应用交互。

link: https://github.com/CurtisNewbie/MediaHoster

## 4.2 Android ImageEncryptor

一个由密码保护的 Android 图片浏览器，使用 **Dagger 2** 和开源库 **PhotoView** 实现。

link: https://github.com/CurtisNewbie/Android_ImageEncryptor

## 4.3 PDFHoster

一个用于托管和在线浏览 PDF 文件的 webapp。 使用 **Quarkus** 实现，同时一个 **Angular** 前端已经实现，在线渲染 PDF 的功能是基于库 **ng2-pdfjs-viewer**，该库内部使用 PDF.js.

link: https://github.com/CurtisNewbie/PDFHoster

## 4.4 LocalGalleri 

一个用于在线浏览图片的 webapp。该应用扫描文件夹内的图片，并且以 **HATEOAS** 的方式返回给 **Angular** 前端，前端使用 **Virtual Scroll** 来让用户边滚动边拉取和显示图片。

link: https://github.com/CurtisNewbie/LocalGalleri
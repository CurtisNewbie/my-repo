# my-repo

Last Updated At: 05/09/2021

[English](./README.md) | [中文](./README-CN.md)

Following are active projects that I am working on, feel free to have a look. Always use the `main` or `master` branch, I will try my best to make them 'stable'. Some of my projects depend on the modules that I developed. To make them work, you may need to install them using Maven. The modules or dependencies may look messy, but I do try to write some reusable code/components like how we may do it in companies. 

In the first section, I will show you the projects that I am actively developing or maintaining, and then in the next section, I will talk about the modules that I developed, and finally in the last section, there are also some archived projects that I have written a long time ago.

# Content Page 

- [1. Services and Web Applications](#1-services-and-web-applications)
    - [1.1. Auth-Service](#11-auth-service)
    - [1.2. File-Server](#12-file-server)
    - [1.3. Chat-Service](#13-chat-service)
    - [1.4. Todo-App](#14-todoapp)
- [2. BOM](#2-bom)
- [3. Modules](#3-modules)
    - [3.1 Auth-Module](#31-auth-module)
    - [3.2 Transactional-Outbox-Module](#32-transactional-outbox-module)
    - [3.3 Distributed-Task-Module](#33-distributed-task-module)
    - [3.4 Log-Tracing-Module](#34-log-tracing-module)
    - [3.5 Messaging-Module](#35-messaging-module)
    - [3.6 Redis-Util-Module](#36-redis-util-module)
    - [3.7 Common-Module](#37-common-module)
    - [3.8 Service-Module](#38-service-module)
- [4. Archived Projects](#4-archived-projects)
    - [4.1 MediaHoster](#41-mediahoster)
    - [4.2 Android ImageEncryptor](#42-android-imageencryptor)
    - [4.3 PDFHoster](#43-pdfhoster)
    - [4.4 LocalGalleri](#44-localgalleri)
    - [4.5 IOC-Module](#45-ioc-module)

# 1. Services and Web Applications

## 1.1 Auth-Service

This project actually includes two applications: 

- auth-service
- auth-service-web

The one in `auth-service/` is a service for user authentication, managing users' role, recording access information (e.g., ip address and so on) and operation history (i.e., the rest endpoints that the user requested including the arguments). A web application (such as **File-Server**) may use **Auth-Module** is to integrate with this service. 

The one in `auth-service-web` is a web application that provides rest endpoints to communicate with the service application in `auth-service`, it's more like a gateway, and an **Angular** frontend is provided for this webapp.

link: https://github.com/CurtisNewbie/auth-service

## 1.2 File-Server 

A simple file server for hosting files, this is a web application that integrate with the **Auth-Service** mentioned above by using **Auth-Module**. An **Angular** frontend is provided for this webapp.

link: https://github.com/CurtisNewbie/file-server

## 1.3 Chat-Service 

A basic web application for online chatting. The functionalities are mainly backed by the Redis and WebSocket, and the messages are not persistent. An **Angular** frontend is provided for this webapp.

link: https://github.com/CurtisNewbie/chat-service

## 1.4 TodoApp 

A **JavaFx** application for managing todo(s), it's backed by **SQLite**. It doesn't look good, but it works, I actually use it all the time.

link: https://github.com/CurtisNewbie/todoapp

# 2. BOM 

I have a BOM (Bill of Material) file for managing dependencies, and almost all my active projects use it. If you are trying to run one of my application, you may need to install it.

link: https://github.com/CurtisNewbie/curtisnewbie-bom

# 3. Modules

I have written a few modules that are shared between services to reuse existing code, unfortunately, you will need to install them manually. While I am developing the applications, these modules evolve as well. So, the modules may look pretty basic at first, but they will get better.

## 3.1 Auth-Module

Module for web security, user authentication, and integration with **Auth-Service**. **Auth-Service** is a service for managing user information and authentication, this module integrates with the Spring Security by implementing a `AuthenticationProvider`, in which it uses **Dubbo** to do RPC call to **Auth-Service** and validate the user credentials. This module is also responsible for collecting and sending user access information and user operation information to **Auth-Service**.

link: https://github.com/CurtisNewbie/auth-module

## 3.2 Transactional-Outbox-Module

A polling publisher implementation of the **Transactional-Outbox** pattern for reliable message publishing. With this module, only when transactions are committed, messages are *'published'* to the message broker.

link: https://github.com/CurtisNewbie/transactional-outbox-module

## 3.3 Distributed-Task-Module

Module that supports basic distributed task scheduling using Quartz and Redis. 

link: https://github.com/CurtisNewbie/distributed-task-module

## 3.4 Log-Tracing-Module 

Module that provides log tracing ability. This is powered by MDC, and it works also for **Dubbo** RPC calls.

link: https://github.com/CurtisNewbie/log-tracing-module

## 3.5 Messaging-Module 

Module for async messaging using RabbitMQ, it provides convenient services and listener adapters for dispatching and consuming messages.

link: https://github.com/CurtisNewbie/messaging-module

## 3.6 Redis-Util-Module 

A simple module that wraps **Redisson** to simplify some of the boilerplate code, it doesn't do much. For the complex scenarios, I still use **Redisson** directly instead, e.g., for the **Chat-Service**.

link: https://github.com/CurtisNewbie/redis-util-module

## 3.7 Common-Module

Module that provides common utility classes.

link: https://github.com/CurtisNewbie/common-module

## 3.8 Service-Module 

This module is used to import dependencies to use **Dubbo** and **Nacos** for RPC. It's merely a pom file. 

link: https://github.com/CurtisNewbie/service-module

# 4. Archived Projects

## 4.1 MediaHoster 

A web application that supports media scanning (from directory) and streaming. It's powered by **Quarkus**, and it supports *byte-range requests*, meaning that a specified range of data is transmitted as requested. Both an **Angular** application and an **Android TV** application are written to work with this webapp.

link: https://github.com/CurtisNewbie/MediaHoster

## 4.2 Android ImageEncryptor

A password protected image viewer on Android platform, it's backed by **Dagger 2** and a open sourced library called **PhotoView**. 

link: https://github.com/CurtisNewbie/Android_ImageEncryptor

## 4.3 PDFHoster

A web application that hosts pdf files. It's powered by **Quarkus**. An **Angular** frontend is provided, and the ability to render pdf file content on the browser is supported by the library **ng2-pdfjs-viewer**, which internally uses PDF.js.

link: https://github.com/CurtisNewbie/PDFHoster

## 4.4 LocalGalleri 

A basic web application for image sharing. It essentially scans all the images in a directory, and exposes them as resources via REST and HATEOAS to the **Angular** frontend. As users scroll down in the **Virtual Scroll**, images are fetched by the browser.

link: https://github.com/CurtisNewbie/LocalGalleri

## 4.5 IOC-Module 

A simple IOC container for learning how IOC works.

link: https://github.com/CurtisNewbie/ioc-module
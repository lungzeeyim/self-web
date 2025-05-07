---
title: Other Question
tags:
- job
---

## Jaspersoft
- 什么是Jaspersoft？它的核心组件有哪些？
    - Jaspersoft 是一款开源的商业智能（BI）套件，主要用于数据报表、分析和可视化。核心组件包括：
        - JasperReports：报表引擎，负责生成和渲染报表。
        - JasperReports Server：集中化管理和发布报表的服务器平台。
        - JasperSoft Studio：可视化设计工具，用于创建报表模板。
        - TIBCO Jaspersoft OLAP（企业版）：支持多维数据分析。

- JasperReports 和 JasperReports Server 的区别是什么？
    - JasperReports 是底层库，用于编程生成报表（如通过Java代码调用）。
    - JasperReports Server 是Web应用，提供报表的存储、调度、权限管理和在线查看功能。

-  动态参数（Parameters）在报表中传递？
    - 在JasperSoft Studio中定义参数（如$P{start_date}）。
    - SQL查询中使用参数（如WHERE date >= $P{start_date}）。
    - 运行时通过Java代码或JasperReports Server传入参数值。

- 如何将报表导出为PDF或Excel？
    - 代码方式：通过JasperExportManager.exportReportToPdfFile()（Java API）。
    - JasperReports Server：在Web界面点击导出按钮选择格式。

- 如何将Jaspersoft集成到Java Web应用中？
    - 嵌入式：将JasperReports库加入项目依赖，调用API生成报表。
    - REST API：通过JasperReports Server的API获取报表（如/rest_v2/reports/{path}.pdf）。
    - iframe集成：直接嵌入Server的报表URL到Web页面。

## RESTFUL API
- 什么是 REST API？它与 SOAP 的主要区别？
    - REST API 是基于 HTTP 协议的架构风格，使用资源标识符（URI）和标准方法（GET/POST/PUT/DELETE）操作资源，无状态、可缓存。
    - JSON / XML

- REST 的六大约束条件
    - Cacheable：响应明确是否可缓存。
    - Uniform Interface：统一资源标识（URI）、自描述消息（如 JSON）、HATEOAS。
    - Layered System：客户端无需关心中间层（如代理、CDN）。
    - Code on Demand（可选）：服务器可返回可执行代码（如 JavaScript）。

- HTTP 方法与 CRUD 对应关系
    - GET：查询资源（Read）
    - POST：创建资源（Create）
    - PUT：全量更新资源（Update）
    - PATCH：部分更新资源（Update）
    - DELETE：删除资源（Delete）

- 常见 HTTP 状态码
    - 200 OK：成功。
    - 201 Created：资源创建成功。
    - 400 Bad Request：客户端错误（如参数缺失）。
    - 401 Unauthorized：未认证。
    - 403 Forbidden：无权限。
    - 404 Not Found：资源不存在。
    - 500 Internal Server Error：服务器内部错误。

- RESTful URL 设计示例
    - 获取用户列表：GET /users
    - 获取单个用户：GET /users/{id}
    - 创建用户：POST /users
    - 更新用户：PUT /users/{id}
    - 删除用户：DELETE /users/{id}
    - 获取用户的订单：GET /users/{id}/orders

- API 版本控制实现
    - URL 路径：/v1/users（简单，但破坏 URI 一致性）。
    - header：Accept: application/vnd.company.api.v1+json（更灵活）。

- 分页实现方式
    - Offset/Limit：GET /users?offset=0&limit=10（适合小型数据集）。
    - Cursor-based：GET /users?cursor=abc123&limit=10（性能更好，避免跳过大量数据）。

- 常见认证方式 ?
    - Basic Auth：Base64 编码的 用户名:密码（简单但不安全）。
    - API Key：请求头或参数中传递密钥（如 X-API-Key: abc123）。
    - OAuth 2.0：授权码模式（Authorization Code）最常用。
    - JWT：无状态令牌，包含签名 payload（如 Header.Payload.Signature）。

- OAuth 2.0 授权流程 ?
    - Authorization Code：前端跳转授权页，后端用 code 换 token（最安全）。
    - Client Credentials：机器对机器认证（无用户参与）。
    - Password：用户直接提供账号密码（仅信任客户端时使用）。

```
+---------+               +----------------+       +---------------+
|  User   |               | Your Frontend  |       | Auth Server   |
+---------+               +----------------+       +---------------+
     | 点击登录按钮               |                       |
     |-------------------------->|                       |
     |                           | 生成授权链接并跳转      |
     |                           |----------------------->|
     |                           |                       | 用户登录并授权
     |                           |                       |<---------+
     |                           | 重定向到 callback      |          |
     |                           |<-----------------------|          |
     | 从 URL 提取 code          |                       |          |
     |<--------------------------|                       |          |
     |                           | 发送 code 给后端       |          |
     |                           |----------------------->|          |
     |                           |                       | 用 code 换 token
     |                           |                       |<---------+
     |                           | 返回用户数据           |          |
     |                           |<-----------------------|          |
     | 显示登录成功               |                       |          |
     |<--------------------------|                       |          |

```







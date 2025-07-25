

=======
## 2. 功能特性

本项目提供以下核心功能：

### 2.1 HTTP 请求与响应日志记录
- 基于 Spring AOP，创建一个拦截器，拦截所有的 HTTP 请求和响应。
- 在拦截器中记录请求的路径、方法、参数和响应数据。
- 优点：解耦业务代码和日志逻辑，实现灵活的日志记录。

- 使用 Spring 的 HandlerInterceptor：
- 实现 HandlerInterceptor 接口，在 preHandle 和 postHandle 方法中记录请求和响应。
- 优点：提供了更直接的方式来拦截和处理 HTTP 请求。

- 使用第三方库（如 Logbook）：
- 直接集成 Logbook，它能够自动记录 HTTP 请求和响应数据。
- 配置简单，支持多种扩展。

### 2.2 支持多种日志格式
- 基于日志框架（如 Logback 或 Log4j）配置格式：
- 通过 Logback 的配置文件（logback.xml）或 Log4j 的 YAML/JSON 配置文件，定义不同格式的日志输出模板。
- 优点：简单易用，支持多种输出格式。

- 使用日志适配器/转换器：
- 实现一个日志适配器，将日志内容转换为不同格式（如 JSON、XML 或自定义格式）。
- 优点：灵活性高，可根据需求定制输出。

- 多格式日志输出器：
- 创建一个自定义的日志输出器，根据配置动态选择日志格式（如 JSON、纯文本等）。
- 优点：支持在同一系统中同时输出不同格式的日志。

## 2.3 灵活的日志过滤
- 基于正则表达式的过滤：
- 使用正则表达式匹配 URL、请求参数或响应内容，动态过滤日志。
- 优点：更精确的过滤规则，适合复杂场景。
- 动态规则引擎：

- 集成规则引擎（如 Drools 或 EasyRules），支持以规则文件或动态加载的方式定义过滤条件。
- 优点：支持更复杂的逻辑和条件组合。

- 分布式过滤规则：
- 在分布式系统中，集中管理日志过滤规则，并同步到各服务实例。
- 优点：统一规则，便于维护。

##  2.4 配置动态调整
- 配置中心支持：
- 集成配置中心（如 Spring Cloud Config、Apollo 或 Nacos），动态加载日志相关配置。
- 优点：集中化管理，支持实时更新。

- 基于数据库的配置更新：
- 将日志配置存储在数据库中，通过管理界面实时修改和生效。
- 优点：易于操作，适合运维团队使用。

- 热点更新机制：
- 利用 Spring Boot 的 @ConfigurationProperties 和热加载机制，监听配置文件的变化并实时生效。
- 优点：实现简单，适合小型项目。

##  2.5 性能优化
- 日志批量写入：
- 将日志数据暂存到内存队列中，定期批量写入磁盘或外部存储。
- 优点：减少 I/O 操作，提高写入效率。

- 日志压缩存储：
- 在写入日志文件时，使用 GZIP 等压缩算法对数据进行压缩。
- 优点：节省存储空间，适合大规模日志数据。

##  2.6 扩展性强
- 支持多种存储目标：
- 提供接口支持，将日志写入文件、数据库、消息队列（如 Kafka、RabbitMQ）或云存储。
- 优点：适应不同的存储需求。

- 基于消息中间件的日志流转：
- 将日志数据作为消息发送到中间件（如 Kafka），再由独立服务处理日志存储或分析。

- 优点：支持高并发日志处理。


<!-- by 莫永启 -->
## 3. 环境要求

运行本项目需要满足以下环境要求：

### 3.1 操作系统
- 支持 Windows、macOS 和主流 Linux 发行版。

### 3.2 Java 运行环境
- 推荐使用 JDK 11 或更高版本。
- 可通过以下命令检查 JDK 是否已正确安装：
  ```bash
  java -version
  ```

### 3.3 构建工具
- 本项目使用 Gradle 进行构建，需安装 安装Gradle3.3版本以上。
- 检查 Gradle 版本：
  ```bash
  gradle -v
  ```

### 3.4 网络环境
- 稳定的互联网连接，用于下载依赖和运行服务。
- 介于国内github位于国外的服务，国内用户可自行使用梯子等网络工具等
- 在运行项目:
  ```bash
  gradlew run
  Downloading https://services.gradle.org/distributions/gradle-3.3-bin.zip下载需要网络环境
  ```
---


<!-- by 唐文广 -->
## 4. 快速开始
温馨提示：你需要完成环境的配置才能部署本项目，本项目要求JDK最低1.8及以上，安装了Gradle 3.3及以上版本。
按照以下步骤，您可以快速启动本项目：

### 4.1 克隆代码
首先，克隆项目代码到本地：
```bash
git clone https://github.com/anyEkko/logbook-spring-boot-demo.git
```
![alt text](img/image.png)

### 4.2 构建项目
使用 gradle 进行构建：
```bash
gradlew build
```
构建成功结果如下
![alt text](img/gradlewbuild.png)
 
### 4.3 启动服务
运行以下命令启动 Spring Boot 服务：
```bash
gradlew bootRun
```
启动成功后如下：
![alt text](img/gradlewbootRun.png)

### 4.4 访问服务
项目启动后，默认监听 `http://localhost:8080`，您可以通过浏览器或工具（如 Postman）访问测试。  
我们可以访问 `http://localhost:8080/echo/` + 任意你想测试的用例。  
例如：我们访问 `http://localhost:8080/echo/helloworld`。  
我们可以先在网页上看到helloworld字样。  
![alt text](img/helloworld2.png)  
我们在后台也可以清楚看到样例的信息： 
![alt text](img/helloworld.png)
---
- 优点：支持高并发日志处理。


<!--by 伍师杰-->
### 5. 项目架构
本项目采用模块化架构设计，遵循高内聚、低耦合的原则，确保系统的可维护性和可扩展性。架构主要分为以下核心模块：

### 5.1 日志记录模块
实现方式：基于Logbook框架实现HTTP请求/响应的全链路拦截与记录
核心功能：
支持JSON、文本等多种日志格式配置
提供请求/响应内容的精细化过滤规则
支持异步日志写入，避免阻塞主业务流程
可扩展的日志输出渠道（文件、ELK、数据库等）

### 5.2 配置模块
实现方式：基于Spring Boot配置体系，结合Nacos实现动态配置
核心功能：
通过application.yml集中管理应用配置
支持多环境配置隔离（dev/test/prod）
实现配置热更新机制，关键参数修改实时生效
提供配置版本管理和回滚能力

### 5.3 安全模块
实现方式：基于自定义过滤器+注解实现敏感数据处理
核心功能：
自动识别并脱敏身份证号、手机号等敏感信息
支持正则表达式自定义脱敏规则
提供日志审计追踪功能
符合GDPR等数据安全合规要求

### 5.4 控制器模块
实现方式：Spring MVC RESTful风格API设计
核心功能：
清晰的API版本管理（/v1/api/...）
统一的异常处理机制
完整的Swagger接口文档
请求参数自动校验（JSR-303）
模块交互设计
各模块通过定义明确的接口契约进行交互：
采用依赖注入(DI)实现模块解耦
关键交互点设置熔断降级机制
模块间通信统一使用DTO对象
通过Spring Event实现异步事件通知
该架构设计支持横向扩展，后续可通过以下方式增强：
引入模块化加载机制（OSGi）
增加gRPC内部通信协议
支持插件化功能扩展


<!-- by 谢鹏飞 -->
## 7. 测试方法

本项目附带多种测试方式，以确保功能的正确性和稳定性：

<!-- by 谢鹏飞 -->
### 7.1 JUnit单元测试
- 本项目是一个基于Gradle工程的项目
- 使用JUnit编写的单元测试覆盖核心功能。
- 在build.gradle文件中添加依赖
- JUnit4依赖
- dependencies {
-    testImplementation 'junit:junit:4.13.2'
- }
- 有两种测试测试方式
- 执行以下命令运行测试：
  ```bash
- 1.执行所有测试方法
- gradle test
- 2.执行特定的方法
- 找到该类位于的包和方法
- 示例
- gradle test --tests "com.example.LogbookSpringBootDemoApplicationTest.testAdd"
  ```
<!-- by 谢鹏飞 -->
### 7.2 接口测试
<!-- by 谢鹏飞 -->
### 7.2.1 使用Postman方法测试
- 通过Postman工具进行接口测试,Postman是一个功能强大的API测试工具,支持发送各种类型的HTTP请求并查看响应。
- 打开Postman应用
- 创建一个GET请求,或者其他请求如(GET、POST、PUT、DELETE等) 
- 示例请求：
- 执行项目中一个GET请求
- 在请求URL中输入http://localhost:8080/echo/{message}
- 将{message}替换成想要的消息
- 点击 Send 按钮发送请求
- Send成功后即可查看响应回来的数据
- 验证响应数据是否符合预期


<!-- by 谢鹏飞 -->
### 7.2.2 Swagger文档测试

- 在 build.gradle 文件中添加依赖
- dependencies {
-    implementation 'org.springdoc:springdoc-openapi-ui:1.6.11'
- }
- 启动项目,Swagger文档会自动生成。
- 通过浏览器访问url:localhost:8080/swagger-ui.html SwaggerUI页面进行查看
- 选择需要测试的接口,填写参数并点击Try it out按钮发送请求。
- 示例请求:
- 在请求URL中输入http://localhost:8080/echo/{message}
- 将{message}替换成想要的消息
- 发送请求后,即可查看响应回来的信息
- 验证响应数据是否符合预期
- Swagger文档测试的优点:
- 相比于Postman测试工具,它可直接在浏览器进行接口测试


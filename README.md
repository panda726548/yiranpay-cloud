<div align="center">
    <h1 style="margin: 30px 0 30px; font-weight: bold;">YiRanPay Base Frame</h1>
    <h4>基于 Vue/Element UI 和 Spring Boot/Spring Cloud & Alibaba 前后端分离的分布式微服务架构</h4>
</div>


## 平台简介

聚合支付是一种第四方支付服务。简而言之，第三方支付提供的是资金清算通道，而聚合支付提供的是支付基础之上的多种衍生服务。聚合支付服务”不具备支付牌照，而是通过聚合多种第三方支付平台、合作银行及其他服务商接口等支付工具的综合支付服务。  
- 采用前后端分离的模式，前端基于 Vue/Element UI。
- 后端采用Spring Boot、Spring Cloud & Alibaba。
- 注册中心、配置中心选型Nacos，权限认证使用Redis。
- 流量控制框架选型Sentinel，分布式事务选型Seata。
- 演示地址联系作者

## 该如何使用它？

所有的服务模块在 yiranpay-modules 下。  
如果您了解一个项目是如何编译及部署的，可以选择适合自己的方式。  
以下根据常见条件列出部分使用方法：  

- **1：作为单独的外部服务使用**

  下载版本中的 yiranpay-x.x.x.zip 解压出 Jar 包进行部署。  
  （暂时没有，等有项目需要的时候会上传 Jar 包）  
  需自行配置 Nacos 等组件，Jar 的启动命令中添加 Nacos 相关指令：

  ```bash
  java -jar -Dserver.port=80  
              -Dspring.cloud.nacos.discovery.namespace=YOUR_NAMESPACE  
              -Dspring.cloud.nacos.config.namespace=YOUR_NAMESPACE  
              -Dspring.cloud.nacos.config.group=YOUR_GROUP  
              -Dspring.cloud.nacos.config.server-addr=YOUR_SERVER   
              -Dspring.cloud.nacos.discovery.server-addr=YOUR_SERVER  
              *.jar  
  ```

  具体配置可参考 docs 文档中提供的参考配置。  
  如果发现 BUG，可以在 `Issues` 中提交您的问题.

- **2：可以访问该项目的 Maven 私服 & 不需要修改框架代码**

  在 yiranpay-modules 中选择需要的模块进行对应 tag 的部署即可。（也可以自己进行编译）  
  如果发现 BUG，可以在`Issues` 中提交您的问题。或直接与负责人沟通。

  
## 模块简介

```
yiranpay   
├── yiranpay-auth                                        // 认证中心
├── yiranpay-common                                      // 通用模块
│       └── yiranpay-common-core                         // 核心模块
│       └── yiranpay-common-datascope                    // 权限范围
│       └── yiranpay-common-datasource                   // 多数据源
│       └── yiranpay-common-log                          // 日志记录
│       └── yiranpay-common-redis                        // Redis
│       └── yiranpay-common-seata                        // seata
│       └── yiranpay-common-security                     // 安全模块
│       └── yiranpay-common-swagger                      // 系统接口
├── yiranpay-gateway                                     // 网关模块
├── yiranpay-modules                                     // 业务模块
│       └── yiranpay-file                                // 文件服务
│       └── yiranpay-gen                                 // 代码生成
│       └── yiranpay-channel                             // 支付渠道路由模块
│       └── yiranpay-job                                 // 定时任务
│       └── yiranpay-facade                              // 对外接口模块
│       └── yiranpay-system                              // 系统模块
│       └── yiranpay-member                              // 会员模块
│       └── yiranpay-payorder                            // 订单模块
│       └── yiranpay-product                             // 产品模块
│       └── yiranpay-reconciliation                      // 对账模块
│       └── pom.xml                                  // 服务模块继承此pom
├── yiranpay-api                                     // 接口模块
│       └── yiranpay-aoi-outside                       // 支付接口
│       └── yiranpay-api-system                        // 系统接口
├── yiranpay-visual                                  // 运维中心
│       └── yiranpay-monitor                           // 监控管理
├──pom.xml                                           // 依赖管理

风控系统（集成风控引擎（Radar））
https://gitee.com/freshday/radar
```

## 架构图（参考）
![image](https://github.com/panda726548/yiranpay-cloud/assets/52069417/54728608-0ffe-4d45-8e74-afb38c920fbb)

## 对账流程
![image](https://github.com/panda726548/yiranpay-cloud/assets/52069417/35e6f771-02bb-4fd6-8a7b-acb0dcccd500)

## 模块功能说明
1.  **用户管理** ：用户是系统操作者，该功能主要完成系统用户配置。对各个基本的用户增删改查，导出excel表格，批量删除。
1.  **角色管理** ：角色菜单权限分配、设置角色按机构进行分配菜单权限和增删改查权限。
1.  **菜单管理** ：N级别自定义菜单，自定义菜单图标，业务菜单和系统菜单分离，菜单状态显示隐藏，配置系统菜单，操作权限，按钮权限标识等。
1.  **部门管理** ：配置系统组织机构（公司、部门、小组），树结构展现。
1.  **岗位管理** ：配置系统用户所属担任职务。
1.  **字典管理** ：对系统中经常使用的一些较为固定的数据进行维护。
1.  **参数管理** ：对系统动态配置常用参数。
1.  **通知公告** ：系统通知公告信息发布维护。
1.  **操作日志** ：系统正常操作日志记录和查询；系统异常信息日志记录1. 查询。
1.  **登录日志** ：系统登录日志记录查询包含登录异常。
1.  **在线用户** ：当前系统中活跃用户状态监控。可强制用户下线。
1.  **定时任务** ：在线（添加、修改、删除)任务调度包含执行结果日志。启动、暂停、执行定时任务操作。
1.  **数据监控** ：监视当期系统数据库连接池状态，可进行分析SQL找出系统性能瓶颈。
1.  **服务监控** ：监控服务器相关信息。
1.  **表单构建** ：拖拽式快速构建表单，组建元素丰富，有富文本、上传控件、下拉框等等
1.  **代码生成** ：前后端代码的生成（java、html、xml、sql)支持CRUD下载 。
1.  **系统接口** ：根据业务代码自动生成相关的api接口文档。开发人员只需要加好注解自动生成API接口文档。
1.  **UES加密** ：系统加密模块，对敏感信息加密，提供加密解密方法。
1.  **渠道管理** ：支付渠道管理，包括资金渠道配置（支付渠道），目标机构配置，API结果码设置，统一结果码配置...
1.  **平台订单渠道** ：平台支付订单，所有的交易都走支付核心，所有的交易都记录在渠道订单中。
1.  **综合管理** ：联合查询，根据不同的条件查询订单支付结果，机构订单结构查询，根据机构订单号（提供给第三方的订单号）从第三方支付或者银行查询支付结果。
1.  **支付网关**：支付网关是直接对接业务系统的接口，它本身并不执行任何支付相关的业务逻辑。它将支付产品接口中和业务无关的功能提取出来，在这里统一实现。这样在具体产品接口中，就无需考虑这些和业务无关的逻辑。支付网关设计还和对外的接口参数有关。商户接口配置、接口权限、IP白名单、商户秘钥管理
1.  **交易对账管理** ：每天定时对前一天平台的交易订单和银行方（例如：微信、支付宝...）订单进行匹配校验，校验订单状态、手续费、交易金额等。
1.  **平台订单渠道** ：平台支付订单，所有的交易都走支付核心，所有的交易都记录在渠道订单中。
1.  **MQ管理** ：配置MQ消息，记录发送的MQ消息信息，按照一定的规则处理发送失败的消息数据。
1.  **支付产品** ：支付产品模块是按照支付场景来为业务方提供支付服务。这个模块一般位于支付网关之后，支付渠道之前。 它根据支付能力将不同的支付渠道封装成统一的接口，通过支付网关来对外提供服务。所以，从微服务的角度，支付产品本身也是一个代理模式的微服务，它透过支付网关响应业务方请求， 进行一些统一处理后，分发到不同的支付渠道去执行，最后将执行结果做处理后，通过支付网关再回传给业务方。
1.  **会员管理**: 会员管理分为内部客户与外部客户两种，内部客户是指集团内部的公司或个人，外部客户则是使用平台服务且与集团无关的外部公司或者个人。
    内部客户：集团内部的公司或个人。以阿里巴巴集团为例，不同业务线包含众多子公司，根据集团战略需要统一接入支付宝，这种情况下内部公司的接入在支付宝系统时一般会定义为内部客户，此类客户和外部客户之间会有一定的差异化服务，在一些风险、服务以及产品层面均会作出一定的调整；
    外部客户：使用平台服务且与集团无关的外部公司或者个人。以支付宝举例，喜马拉雅接入了支付宝，对于支付宝来说即外部客户，因为接入了支付宝所以可以使用支付宝的部分功能。

## 集成风控引擎（Radar）实现支付风控管理
-实时风控，特殊场景可以做到100ms内响应
-可视化规则编辑器，丰富的运算符、计算规则灵活
-支持中文，易用性更强
-自定义规则引擎，更加灵活，支持复杂多变的场景
-插件化的设计，快速接入其它数据能力平台
-NoSQL，易扩展，高性能
-配置简单，开箱即用

    ![image](https://github.com/panda726548/yiranpay-cloud/assets/52069417/46aff59b-2274-474d-9e78-afd1ed5bf600)
    ![image](https://github.com/panda726548/yiranpay-cloud/assets/52069417/07f69637-a01a-499b-96c7-c2241bd46468)
    ![image](https://github.com/panda726548/yiranpay-cloud/assets/52069417/bbc03fae-a00f-4aeb-a3ee-e1af0fae56ea)
    ![image](https://github.com/panda726548/yiranpay-cloud/assets/52069417/7e4ec4e0-f26b-470a-863a-a25a3bae7670)
    ![image](https://github.com/panda726548/yiranpay-cloud/assets/52069417/fe0eefe5-0809-434b-ae7a-908ac84d41ab)

    


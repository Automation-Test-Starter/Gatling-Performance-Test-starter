
# Gatling-performance-test-starter

**中文** | [English](/README_EN.md)

一个使用 gatling 工具做性能测试的介绍文档，包含了环境搭建、工程初始化、示例，进阶用法等内容

- [Gatling-performance-test-starter](#gatling-performance-test-starter)
  - [Gatling 介绍](#gatling-介绍)
  - [环境搭建](#环境搭建)
    - [VSCode + Gradle + Scala 版本](#vscode--gradle--scala-版本)
      - [准备工作](#准备工作)
      - [安装插件](#安装插件)
      - [官方 demo 初始化\&调试](#官方-demo-初始化调试)
    - [VSCode + Maven + Scala 版本](#vscode--maven--scala-版本)
      - [准备工作](#准备工作-1)
      - [安装插件](#安装插件-1)
      - [官方 demo 初始化\&调试](#官方-demo-初始化调试-1)
    - [IDEA + Gradle + Scala 版本](#idea--gradle--scala-版本)
    - [IDEA + Maven + Scala 版本](#idea--maven--scala-版本)
  - [从 0 到 1 搭建自己的 Gatling 工程](#从-0-到-1-搭建自己的-gatling-工程)
    - [Gradle + Scala 版本](#gradle--scala-版本)
      - [创建一个空的 Gradle 工程](#创建一个空的-gradle-工程)
      - [配置项目 build.gradle](#配置项目-buildgradle)
      - [gradle build 项目并初始化](#gradle-build-项目并初始化)
      - [初始化目录](#初始化目录)
      - [编写脚本](#编写脚本)
      - [调试脚本](#调试脚本)
    - [Maven + Scala 版本](#maven--scala-版本)
      - [创建一个空的 Maven 工程](#创建一个空的-maven-工程)
      - [配置项目 pom.xml](#配置项目-pomxml)
      - [初始化目录](#初始化目录-1)
      - [编写脚本](#编写脚本-1)
      - [调试脚本](#调试脚本-1)
  - [进阶用法](#进阶用法)
    - [测试报告解析](#测试报告解析)
      - [总览](#总览)
        - [总览图](#总览图)
        - [请求数\&响应时间分布图](#请求数响应时间分布图)
        - [请求标准统计分析图](#请求标准统计分析图)
        - [活跃用户数统计图](#活跃用户数统计图)
        - [响应时间分布图](#响应时间分布图)
        - [响应时间百分位对比图](#响应时间百分位对比图)
        - [每秒请求数图](#每秒请求数图)
        - [每秒响应数图](#每秒响应数图)
      - [单个请求分析报告](#单个请求分析报告)
    - [性能场景设置](#性能场景设置)
      - [Injection 注入](#injection-注入)
        - [什么是 Injection](#什么是-injection)
        - [常用 Injection 场景](#常用-injection-场景)
          - [Open Model 开放模型场景](#open-model-开放模型场景)
          - [Closed Model 闭合模型场景](#closed-model-闭合模型场景)
        - [Meta DSL 场景](#meta-dsl-场景)
        - [Concurrent Scenarios 并发场景](#concurrent-scenarios-并发场景)
        - [其他场景](#其他场景)
    - [持续集成](#持续集成)
      - [接入 github action](#接入-github-action)
        - [Gradle + Scala 版本](#gradle--scala-版本-1)
        - [Maven + Scala 版本](#maven--scala-版本-1)
    - [录制脚本 Recorder](#录制脚本-recorder)
  - [参考](#参考)

## Gatling 介绍

Gatling 是一个用于性能测试和负载测试的开源工具，特别适用于测试 Web 应用程序。它是一个基于 Scala 编程语言的高性能工具，用于模拟并测量应用程序在不同负载下的性能。

以下是 Gatling 的一些重要特点和优势：

- 基于 Scala 编程语言：Gatling 的测试脚本使用 Scala 编写，这使得它具有强大的编程能力，允许用户编写复杂的测试场景和逻辑。
- 高性能：Gatling 被设计为高性能的负载测试工具。它使用了非阻塞的 I/O 和异步编程模型，能够模拟大量并发用户，从而更好地模拟真实世界中的负载情况。
- 易于学习和使用：尽管 Gatling 的测试脚本是使用 Scala 编写的，但它的 DSL（领域特定语言）非常简单，容易上手。即使你不熟悉 Scala，也可以快速学会如何创建测试脚本。
- 丰富的功能：Gatling 提供了丰富的功能，包括请求和响应处理、数据提取、条件断言、性能报告生成等。这些功能使你能够创建复杂的测试场景，并对应用程序的性能进行全面的评估。
- 多协议支持：除了 HTTP 和 HTTPS，Gatling 还支持其他协议，如 WebSocket，JMS，和 SMTP。这使得它适用于测试各种不同类型的应用程序。
- 实时结果分析：Gatling 可以在测试运行期间提供实时的性能数据和图形化报告，帮助你快速发现性能问题。
- 开源和活跃的社区：Gatling 是一个开源项目，拥有一个活跃的社区，不断更新和改进工具。
- 支持 CI/CD 集成：Gatling 可以与 CI/CD 工具（如 Jenkins）集成，以便在持续集成和持续交付流程中执行性能测试。

总的来说，Gatling 是一个功能强大的性能测试工具，适用于测试各种类型的应用程序，帮助开发团队识别和解决性能问题，以确保应用程序在生产环境中具有稳定的性能和可伸缩性。

## 环境搭建

> 由于我是 macbook，后面的介绍几本会以 macbook demo 为例，windows 的同学可以自行参考

### VSCode + Gradle + Scala 版本

#### 准备工作

- [x] 开发工具：VSCode
- [x] 安装 Gradle 版本>=6.0，我使用的 Gradle 8.44
- [x] 安装 JDK 版本>=8，我使用的 JDK 19

#### 安装插件

- [x] VSCode 搜索 Scala (Metals) 插件进行安装
- [x] VSCode 搜索 Gradle for Java 插件进行安装

#### 官方 demo 初始化&调试

> 前面先会用官方 demo 工程来做初始化和调试，后面再介绍如何自己创建工程

- 克隆官方 demo 工程

```bash
git clone git@github.com:gatling/gatling-gradle-plugin-demo-scala.git
```

- 使用 VSCode 打开克隆下来的官方 demo 工程

- 用 VSCode 打开本项目 Terminal 窗口，执行以下命令

```bash
gradle build
```

![readme-build](./readme-pic/readme-build.png)

- 运行工程中的 demo

```bash
gradle gatlingRun
```

- 查看命令行运行结果

![readme-report](./readme-pic/readme-report.png)

- 点击命令行报告中的 html 报告链接，并使用浏览器打开，即可查看详细的报告信息

![readme-report1](./readme-pic/readme-report1.png)

### VSCode + Maven + Scala 版本

#### 准备工作

- [x] 开发工具：VSCode
- [x] 安装 Maven，我使用的 Gradle 8.44
- [x] JDK 版本>=8，我使用的 JDK 19

#### 安装插件

- [x] VSCode 搜索 Scala (Metals) 插件进行安装
- [x] VSCode 搜索 Maven for Java 插件进行安装

#### 官方 demo 初始化&调试

> 前面先会用官方 demo 工程来做初始化和调试，后面再介绍如何自己创建工程

- 克隆官方 demo 工程

```bash
git clone git@github.com:gatling/gatling-maven-plugin-demo-scala.git
```

- 使用 VSCode 打开克隆下来的官方 demo 工程

- 用 VSCode 打开本项目 Terminal 窗口，执行以下命令运行工程中的 demo

```bash
mvn gatling:test
```

- 查看命令行运行结果

![readme-report2](./readme-pic/readme-report2.png)

- 点击命令行报告中的 html 报告链接，并使用浏览器打开，即可查看详细的报告信息

![readme-report1](./readme-pic/readme-report1.png)

### IDEA + Gradle + Scala 版本

与 VSCode 下基本类似，这里就不再赘述了

差异点如下：

- IDEA 搜索 Scala 插件进行安装
- 新的运行方式：右键选择项目目录下的 Engine.scala 文件，选择 Run 'Engine'也可以运行 demo（运行过程中需要按回车键确认哦）

### IDEA + Maven + Scala 版本

与 VSCode 下基本类似，这里就不再赘述了

差异点如下：

- IDEA 搜索 Scala 插件进行安装
- 新的运行方式：右键选择项目目录下的 Engine.scala 文件，选择 Run 'Engine'也可以运行 demo（运行过程中需要按回车键确认哦）

## 从 0 到 1 搭建自己的 Gatling 工程

### Gradle + Scala 版本

#### 创建一个空的 Gradle 工程

```bash
mkdir gatling-gradle-demo
cd gatling-gradle-demo
gradle init
```

#### 配置项目 build.gradle

在 项目中 build.gradle 文件中添加以下内容

> 可 copy 本项目中的 build.gradle 文件内容，更多配置可参考[官方文档](https://gatling.io/docs/gatling/reference/current/extensions/gradle_plugin/)

```groovy
// 插件配置
plugins {
    id 'scala' // scala插件声明（基于开发工具插件）
    id 'io.gatling.gradle' version '3.9.5.6'  // 基于gradle的gatling框架插件版本声明
}
//仓库源配置
repositories {
  // 使用 maven 中心仓库源
  mavenCentral()
}
// gatling 配置
gatling {
  // logback root level，如果配置文件夹中不存在 logback.xml，则默认 Gatling 控制台日志级别
  logLevel = 'WARN' 

  // 执行记录 HTTP 请求的详细程度
  // set to 'ALL' for all HTTP traffic in TRACE, 'FAILURES' for failed HTTP traffic in DEBUG
  logHttp = 'FAILURES' 

  // Simulations 过滤器
  simulations = {
      include "**/simulation/*.scala"
  }
}
// 依赖配置
dependencies {     
 // 图表库，用于生成报告图表
 gatling 'io.gatling.highcharts:gatling-charts-highcharts:3.8.3'
 }
```

#### gradle build 项目并初始化

- 用编辑器打开本项目 Terminal 窗口，执行以下命令确认项目 build 成功

```bash
gradle build
```

- 初始化完成：完成向导后，Gradle 将在项目目录中生成一个基本的 Gradle 项目结构
  
![readme-project-tree1](./readme-pic/readme-project-tree1.png)

#### 初始化目录
  
在 src/gatling/scala 目录下创建一个 simulation 目录，用于存放测试脚本

> Gatling 测试通常位于 src/gatling 目录中。你需要在项目根目录下手动创建 src 目录，然后在 src 目录下创建 gatling 目录。在 gatling 目录下，你可以创建你的测试模拟文件夹 simulation，以及其他文件夹，如 data、bodies、resources 等。

#### 编写脚本

- 在 simulation 目录下创建一个 demo.scala 文件，用于编写测试脚本

- 示例脚本如下，可供参考

> 脚本包含了两个场景，一个是 get 请求，一个是 post 请求
> get 接口验证接口返回状态码为 200，post 接口验证接口返回状态码为 201
> get 接口使用了 rampUsers，post 接口使用了 constantConcurrentUsers
> rampUsers：在指定时间内逐渐增加并发用户数，constantConcurrentUsers：在指定时间内保持并发用户数不变
> 两个接口的并发用户数都是 10 个，持续时间都是 10 秒
> 两个接口的请求间隔都是 2 秒

```scala
package simulation 

import scala.concurrent.duration._

import io.gatling.core.Predef._
import io.gatling.http.Predef._

class demo extends Simulation { 

  val httpProtocol = http
    .baseUrl("https://jsonplaceholder.typicode.com") // 5
  val scn = scenario("GetSimulation")
    .exec(http("get_demo") 
      .get("/posts/1")
      .check(status.is(200)))
    .pause(2)
  val scn1 = scenario("PostSimulation")
    .exec(http("post_demo")
      .post("/posts")
      .body(StringBody("""{"title": "foo","body": "bar","userId": 1}""")).asJson
      .check(status.is(201)))
    .pause(2)

  setUp( 
    scn.inject(rampUsers(10) during(10 seconds)),
    scn1.inject(constantConcurrentUsers(10) during(10 seconds))
  ).protocols(httpProtocol)
}
```

#### 调试脚本

执行以下命令，运行测试脚本并查看报告

```bash
gradle gatlingRun
```

![readme-report3](./readme-pic/readme-report3.png)

### Maven + Scala 版本

#### 创建一个空的 Maven 工程

```bash
mvn archetype:generate -DgroupId=demo.gatlin.maven -DartifactId=gatling-maven-demo
```

初始化完成：完成向导后，Maven 将在新建项目目录并生成一个基本的 Maven 项目结构
  
![readme-project-tree2](./readme-pic/readme-project-tree2.png)

#### 配置项目 pom.xml

在 项目中 pom.xml 文件中添加以下内容

> 可 copy 本项目中的 pom.xml 文件内容，更多配置可参考[官方文档](https://gatling.io/docs/gatling/reference/current/extensions/maven_plugin/)

```xml
<!-- 依赖配置 -->
<dependencies>
  <dependency>
    <groupId>io.gatling.highcharts</groupId>
    <artifactId>gatling-charts-highcharts</artifactId>
    <version>3.9.5</version>
    <scope>test</scope>
  </dependency>
</dependencies>
<!-- 插件配置 -->
  <build>
    <plugins>
      <plugin>
        <groupId>io.gatling</groupId>
        <artifactId>gatling-maven-plugin</artifactId>
        <version>4.6.0</version>
      </plugin>
      <plugin>
        <groupId>net.alchim31.maven</groupId>
        <artifactId>scala-maven-plugin</artifactId>
        <version>4.8.1</version>
        <configuration>
          <scalaVersion>2.13.12</scalaVersion>
        </configuration>
        <executions>
          <execution>
            <goals>
              <goal>testCompile</goal>
            </goals>
            <configuration>
              <jvmArgs>
                <jvmArg>-Xss100M</jvmArg>
              </jvmArgs>
              <args>
                <arg>-deprecation</arg>
                <arg>-feature</arg>
                <arg>-unchecked</arg>
                <arg>-language:implicitConversions</arg>
                <arg>-language:postfixOps</arg>
              </args>
            </configuration>
          </execution>
        </executions>
      </plugin>
    </plugins>
  </build>
```

#### 初始化目录
  
在 src/test/scala 目录下创建一个 simulation 目录，用于存放测试脚本

> scala 测试通常位于 src/test 目录中。你需要在项目 test 目录下创建 scala 目录。在 scala 目录下，你可以创建你的测试模拟文件夹 simulation，以及其他文件夹，如 data、bodies、resources 等。

#### 编写脚本

- 在 simulation 目录下创建一个 demo.scala 文件，用于编写测试脚本

- 示例脚本如下，可供参考

> 脚本包含了两个场景，一个是 get 请求，一个是 post 请求
> get 接口验证接口返回状态码为 200，post 接口验证接口返回状态码为 201
> get 接口使用了 rampUsers，post 接口使用了 constantConcurrentUsers
> rampUsers：在指定时间内逐渐增加并发用户数，constantConcurrentUsers：在指定时间内保持并发用户数不变
> 两个接口的并发用户数都是 10 个，持续时间都是 10 秒
> 两个接口的请求间隔都是 2 秒

```scala
package simulation 

import scala.concurrent.duration._

import io.gatling.core.Predef._
import io.gatling.http.Predef._

class demo extends Simulation { 

  val httpProtocol = http
    .baseUrl("https://jsonplaceholder.typicode.com") // 5
  val scn = scenario("GetSimulation")
    .exec(http("get_demo") 
      .get("/posts/1")
      .check(status.is(200)))
    .pause(2)
  val scn1 = scenario("PostSimulation")
    .exec(http("post_demo")
      .post("/posts")
      .body(StringBody("""{"title": "foo","body": "bar","userId": 1}""")).asJson
      .check(status.is(201)))
    .pause(2)

  setUp( 
    scn.inject(rampUsers(10) during(10 seconds)),
    scn1.inject(constantConcurrentUsers(10) during(10 seconds))
  ).protocols(httpProtocol)
}
```

#### 调试脚本

执行以下命令，运行测试脚本并查看报告

```bash
mvn gatling:test
```

![readme-report3](./readme-pic/readme-report3.png)

## 进阶用法

### 测试报告解析

#### 总览

##### 总览图

> 性能测试执行结束后打开详细的 html 报告，可以看到详细的性能测试报告；
> 可通过指标、活跃用户和随时间变化的请求/响应以及分布来分析您的报告

![readme-test-report1](./readme-pic/readme-test-report1.png)

- 页面中间标题处显示 Simulation 的名字
- 左侧的列表展示不同类型的报告菜单，可点击切换
- 页面中部展示性能测试报告的总览信息，包括：请求总数、成功请求总数、失败请求总数、最短响应时间、最长响应时间、平均响应时间、吞吐量、标准差、百分比分布等。也会展示 gatling 的版本及本次报告运行的时间和时长
- 全局菜单指向综合统计数据。
- 详细信息菜单指向每个请求类型的统计信息。

##### 请求数&响应时间分布图

![readme-test-report2](./readme-pic/readme-test-report2.png)

此图表展示了响应时间在标准范围内的分布情况
左侧的列表显示所有的请求以及请求响应的时间分布，红色代表失败的请求
右边 Number of request 代表用户并发数量，以及各个请求的请求数量及其成功失败状态

> 这些范围可以在 gatling.conf 文件中配置

##### 请求标准统计分析图

![readme-test-report3](./readme-pic/readme-test-report3.png)

此图表显示了一些标准统计数据，例如全局和每个请求的最小值、最大值、平均值、标准差和百分位数。
stats 显示了所有请求具体的成功失败情况 OK 代表成功，KO 代表失败，百分比 99th pct 代表对于这一个 API 总的请求中有百分之 99 的请求 response time 是这个数值

> 这些百分位数可以在 gatling.conf 文件中配置。

##### 活跃用户数统计图

![readme-test-report4](./readme-pic/readme-test-report4.png)

此图表展示了活跃用户数指的是在测试时间段内，正在进行请求的用户数。在测试开始时，活跃用户数为 0。当用户开始发送请求时，活跃用户数开始增加。当用户完成请求时，活跃用户数开始减少。活跃用户数的最大值是在测试期间同时发送请求的用户数。

##### 响应时间分布图

![readme-test-report5](./readme-pic/readme-test-report5.png)

此图表显示了响应时间的分布，包括请求成功的响应时间和请求失败的响应时间。

##### 响应时间百分位对比图

![readme-test-report6](./readme-pic/readme-test-report6.png)

此图表显示一段时间内的各种响应时间百分位数，但仅适用于成功的请求。由于失败的请求可能会提前结束或由超时引起，因此它们会对百分位数的计算产生巨大影响。

##### 每秒请求数图

![readme-test-report7](./readme-pic/readme-test-report7.png)

此图表展示了每秒的请求数，包括成功的请求数和失败的请求数。

##### 每秒响应数图

![readme-test-report8](./readme-pic/readme-test-report8.png)

此图表展示了每秒的响应数，包括成功的响应数和失败的响应数。

#### 单个请求分析报告

> 可点击报告页面上的 details 菜单切换到 details tab 页面，查看单个请求的详细报告

![readme-test-report9](./readme-pic/readme-test-report9.png)

Details 页面主要展示了每个请求的统计数据，与全局报告相似地包括了响应时间分布图，响应时间百分位图，每秒请求数图，每秒响应数图。不同的是最底下有一张图是描述单个请求相对于全局所有请求的响应时间。该图横坐标是每秒全局所有请求数，纵坐标是单个请求的响应时间。

### 性能场景设置

#### Injection 注入

##### 什么是 Injection

在 Gatling 性能测试中，"Injection"是指将虚拟用户（或负载）引入系统的一种方式。它定义了模拟用户如何被引入测试场景，包括用户的数量、速率和方式。Injection 是 Gatling 中用于控制负载和并发度的关键概念，允许你模拟不同的用户行为和负载模型。

用户注入配置文件的定义是通过 injectOpen 和 injectClosed 方法（Scala 中的 inject）完成的。此方法将按顺序处理的注入步骤序列作为参数。每个步骤都定义了一组用户，以及如何将这些用户注入到场景中。

官网更多介绍：<https://gatling.io/docs/gatling/reference/current/core/injection/>

##### 常用 Injection 场景

###### Open Model 开放模型场景

```scala
setUp(
  scn.inject(
    nothingFor(4), // 1
    atOnceUsers(10), // 2
    rampUsers(10).during(5), // 3
    constantUsersPerSec(20).during(15), // 4
    constantUsersPerSec(20).during(15).randomized, // 5
    rampUsersPerSec(10).to(20).during(10.minutes), // 6
    rampUsersPerSec(10).to(20).during(10.minutes).randomized, // 7
    stressPeakUsers(1000).during(20) // 8
  ).protocols(httpProtocol)
)
```

1. nothingFor(duration)：设置一段停止的时间，这段时间什么都不做
2. atOnceUsers(nbUsers)：立即注入一定数量的虚拟用户
3. rampUsers(nbUsers) during(duration)：在指定时间内，设置一定数量逐步注入的虚拟用户
4. constantUsersPerSec(rate) during(duration)：定义一个在每秒钟恒定的并发用户数，持续指定的时间
5. constantUsersPerSec(rate) during(duration) randomized：定义一个在每秒钟围绕指定并发数随机增减的并发，持续指定时间
6. rampUsersPerSec(rate1) to (rate2) during(duration)：定义一个并发数区间，运行指定时间，并发增长的周期是一个规律的值
7. rampUsersPerSec(rate1) to(rate2) during(duration) randomized：定义一个并发数区间，运行指定时间，并发增长的周期是一个随机的值
8. stressPeakUsers(nbUsers).during(duration) ：按照拉伸到给定持续时间的[阶跃函数](https://en.wikipedia.org/wiki/Heaviside_step_function)的平滑近似注入给定数量的用户。

###### Closed Model 闭合模型场景

```scala
setUp(
  scn.inject(
    constantConcurrentUsers(10).during(10), // 1
    rampConcurrentUsers(10).to(20).during(10) // 2
  )
)
```

1. constantConcurrentUsers(nbUsers).during(duration) ：注入以使系统中的并发用户数恒定
2. rampConcurrentUsers(fromNbUsers).to(toNbUsers).during(duration) ：注入，使系统中的并发用户数从一个数字线性增加到另一个数字

##### Meta DSL 场景

"Meta DSL"是一种特殊的领域特定语言（DSL），用于描述性能测试场景的元数据（metadata）和全局配置。Meta DSL 允许你定义性能测试中的一些全局设置和参数，以影响整个测试过程，而不是特定于某个场景。

可以使用 Meta DSL 的元素以更简单的方式编写测试。如果您想要链接级别和斜坡以达到应用程序的极限（有时称为容量负载测试的测试），您可以使用常规 DSL 手动完成，并使用 map 和 flatMap 进行循环。

- incrementUsersPerSec

```scala
setUp(
   // 生成一个开放的工作量注入配置文件
  // 每秒分别有 10、15、20、25 和 30 个用户到达
  // 每个级别持续 10 秒
  // 每级持续 10 秒
  scn.inject(
    incrementUsersPerSec(5.0)
      .times(5)
      .eachLevelLasting(10)
      .separatedByRampsLasting(10)
      .startingFrom(10) // Double
  )
```

- incrementConcurrentUsers
  
```scala
setUp(
  // 生成一个封闭的工作负载注入配置文件
  // 并发用户分别为 10、15、20、25 和 30 级
  // 每个级别持续 10 秒
  // 每级持续 10 秒
  scn.inject(
    incrementConcurrentUsers(5)
      .times(5)
      .eachLevelLasting(10)
      .separatedByRampsLasting(10)
      .startingFrom(10) // Int
  )
)
```

incrementUsersPerSec 用于开放式工作负载，incrementConcurrentUsers 用于封闭式工作负载（用户数/秒与并发用户数）。

separatedByRampsLasting 和 startingFrom 都是可选的。如果您不指定斜坡，测试完成后就会立即从一个级别跳到另一个级别。如果您不指定启动用户数，测试将从 0 个并发用户或每秒 0 个用户开始，并立即进入下一步。

##### Concurrent Scenarios 并发场景

```scala
setUp(
  scenario1.inject(injectionProfile1),
  scenario2.inject(injectionProfile2)
)
```

您可以在同一个 setUp 块中配置多个场景同时启动并并发执行。

##### 其他场景

查看官网介绍：<https://gatling.io/docs/gatling/reference/current/core/injection/>

### 持续集成

#### 接入 github action

以 github action 为例，其他 CI 工具类似

##### Gradle + Scala 版本

> 可参考 demo：<https://github.com/Automation-Test-Starter/gatling-gradle-scala-demo>

- 创建.github/workflows 目录：在你的 GitHub 仓库中，创建一个名为 .github/workflows 的目录。这将是存放 GitHub Actions 工作流程文件的地方。

- 创建工作流程文件：在.github/workflows 目录中创建一个 YAML 格式的工作流程文件，例如 gatling.yml。
- 编辑 gatling.yml 文件：将以下内容复制到文件中。

```yaml
name: Gatling Performance Test

on:
  push:
    branches:
      - main

jobs:
  performance-test:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout code
        uses: actions/checkout@v2

      - name: Set up Java
        uses: actions/setup-java@v2
        with:
          java-version: 11
          distribution: 'adopt'

      - name: Run Gatling tests
        run: |
          ./gradlew gatlingRun
        env:
          GATLING_SIMULATIONS_FOLDER: src/gatling/scala

      - name: Archive Gatling results
        uses: actions/upload-artifact@v2
        with:
          name: gatling-results
          path: build/reports/gatling

      - name: Upload Gatling results to GitHub
        uses: actions/upload-artifact@v2
        with:
          name: gatling-results
          path: build/reports/gatling
```

- 提交代码：将 gatling.yml 文件添加到仓库中并提交。
- 查看测试报告：在 GitHub 中，导航到你的仓库。单击上方的 Actions 选项卡，然后单击左侧的 Performance Test 工作流。你应该会看到工作流正在运行，等待执行完成，就可以查看结果。

![readme-github-action-gradle](./readme-pic/readme-github-action-gradle.png)

##### Maven + Scala 版本

> 可参考 demo：<https://github.com/Automation-Test-Starter/gatling-maven-scala-demo>

- 创建.github/workflows 目录：在你的 GitHub 仓库中，创建一个名为 .github/workflows 的目录。这将是存放 GitHub Actions 工作流程文件的地方。

- 创建工作流程文件：在.github/workflows 目录中创建一个 YAML 格式的工作流程文件，例如 gatling.yml。
- 编辑 gatling.yml 文件：将以下内容复制到文件中。

```yaml
name: Gatling Performance Test

on:
  push:
    branches:
      - main

jobs:
  performance-test:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout code
        uses: actions/checkout@v2

      - name: Set up Java
        uses: actions/setup-java@v2
        with:
          java-version: 11
          distribution: 'adopt'

      - name: Run Gatling tests
        run: |
          mvn gatling:test
        env:
          GATLING_SIMULATIONS_FOLDER: src/test/scala

      - name: Archive Gatling results
        uses: actions/upload-artifact@v2
        with:
          name: gatling-results
          path: target/gatling

      - name: Upload Gatling results to GitHub
        uses: actions/upload-artifact@v2
        with:
          name: gatling-results
          path: target/gatling
```

- 提交代码：将 gatling.yml 文件添加到仓库中并提交。
- 查看测试报告：在 GitHub 中，导航到你的仓库。单击上方的 Actions 选项卡，然后单击左侧的 Performance Test 工作流。你应该会看到工作流正在运行，等待执行完成，就可以查看结果。

![readme-github-action-maven](./readme-pic/readme-github-action-maven.png)

### 录制脚本 Recorder

> 待补充

## 参考

- galting 官网：<https://gatling.io/>
- galting 官方文档：<https://gatling.io/docs/gatling/>
- galting 官方 github: <https://github.com/gatling/>
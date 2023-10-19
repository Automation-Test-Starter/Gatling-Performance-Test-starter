# Gatling-performance-test-starter

**English** | [中文](/README.md)

An introduction to using the gatling tool for performance testing, including environment setup, project initialization, examples, advanced usage, and more!

- [Gatling-performance-test-starter](#gatling-performance-test-starter)
  - [Gatling Introduction](#gatling-introduction)
  - [Environment setup](#environment-setup)
    - [VSCode + Gradle + Scala Version](#vscode--gradle--scala-version)
      - [Preparation](#preparation)
      - [install plugins](#install-plugins)
      - [official demo initialization \& debugging](#official-demo-initialization--debugging)
    - [VSCode + Maven + Scala version](#vscode--maven--scala-version)
      - [Preparation](#preparation-1)
      - [install plugins](#install-plugins-1)
      - [Official demo initialization \& debugging](#official-demo-initialization--debugging-1)
    - [IDEA + Gradle + Scala version](#idea--gradle--scala-version)
    - [IDEA + Maven + Scala version](#idea--maven--scala-version)
  - [Build your own Gatling project from 0 to 1](#build-your-own-gatling-project-from-0-to-1)
    - [Gradle + Scala versions](#gradle--scala-versions)
      - [Create an empty Gradle project](#create-an-empty-gradle-project)
      - [Configure the project build.gradle](#configure-the-project-buildgradle)
      - [gradle build project and initialize](#gradle-build-project-and-initialize)
      - [Initialization Directory](#initialization-directory)
      - [Writing Scripts](#writing-scripts)
      - [Debugging Scripts](#debugging-scripts)
    - [Maven + Scala version](#maven--scala-version)
      - [Create an empty Maven project](#create-an-empty-maven-project)
      - [Configure the project pom.xml](#configure-the-project-pomxml)
      - [Initialization Directory](#initialization-directory-1)
      - [Writing Scripts](#writing-scripts-1)
      - [Debugging Scripts](#debugging-scripts-1)
  - [Advanced Usage](#advanced-usage)

## Gatling Introduction

Gatling is an open source tool for performance and load testing, especially for testing web applications. It is a high-performance tool based on the Scala programming language for simulating and measuring the performance of applications under different loads.

Here are some of the key features and benefits of Gatling:

- Based on Scala programming language: Gatling's test scripts are written in Scala, which makes it a powerful programming tool that allows users to write complex test scenarios and logic.
- High Performance: Gatling is designed as a high performance load testing tool. It uses non-blocking I/O and an asynchronous programming model that is capable of simulating large numbers of concurrent users to better mimic real-world load situations.
- Easy to learn and use: Although Gatling's test scripts are written in Scala, its DSL (Domain Specific Language) is very simple and easy to learn. Even if you are not familiar with Scala, you can quickly learn how to create test scripts.
- Rich Features: Gatling provides a rich set of features, including request and response processing, data extraction, conditional assertions, performance report generation, and more. These features enable you to create complex test scenarios and perform comprehensive evaluation of application performance.
- Multi-Protocol Support: In addition to HTTP and HTTPS, Gatling supports other protocols such as WebSocket, JMS, and SMTP, making it suitable for testing a wide range of different types of applications.
- Real-time results analysis: Gatling provides real-time performance data and graphical reports during test runs to help you quickly identify performance issues.
- Open source and active community: Gatling is an open source project with an active community that constantly updates and improves the tool.
- CI/CD Integration Support: Gatling can be integrated with CI/CD tools such as Jenkins to perform performance testing in continuous integration and continuous delivery processes.

Overall, Gatling is a powerful performance testing tool for testing a wide range of application types, helping development teams identify and resolve performance issues to ensure consistent performance and scalability of applications in production environments.

## Environment setup

> Since I'm a macbook user, I'll use the macbook demo as an example in the introduction, but windows users can refer to it on their own.

### VSCode + Gradle + Scala Version

#### Preparation

- [x] Development tool: VSCode
- [x] Install Gradle version >= 6.0, I am using Gradle 8.44.
- [x] Install JDK version >= 8, I use JDK 19

#### install plugins

- [x] VSCode search for Scala (Metals) plugin for installation
- [x] VSCode search for Gradle for Java plugin for installation

#### official demo initialization & debugging

> We will use the official demo project for initialization and debugging first, and then we will introduce how to create your own project later.

- Clone the official demo project

```bash
git clone git@github.com:gatling/gatling-gradle-plugin-demo-scala.git
```

- Open the cloned official demo project with VSCode.

- Open the project's Terminal window with VSCode and execute the following command

```bash
gradle build
```

![readme-build](./readme-pic/readme-build.png)

- Run the demo in the project

```bash
gradle gatlingRun
```

- Viewing the results of a command line run

![readme-report](./readme-pic/readme-report.png)

- Click on the html report link in the command line report and open it with your browser to view the detailed report information

![readme-report1](./readme-pic/readme-report1.png)

### VSCode + Maven + Scala version

#### Preparation

- [x] Development tool: VSCode
- [x] Install Maven, I use Gradle 8.44.
- [x] JDK version >= 8, I use JDK 19

#### install plugins

- [x] VSCode search for Scala (Metals) plugins to install
- [x] VSCode search for Maven for Java plugins to install

#### Official demo initialization & debugging

> We will use the official demo project for initialization and debugging first, and then we will introduce how to create your own project.

- Clone the official demo project

```bash
git clone git@github.com:gatling/gatling-maven-plugin-demo-scala.git
```

- Use VSCode to open the cloned official demo project.

- Open the Terminal window of this project with VSCode and execute the following command to run the demo in the project

```bash
mvn gatling:test
```

- Viewing the results of a command line run

![readme-report2](./readme-pic/readme-report2.png)

- Click on the html report link in the command line report and open it with your browser to view the detailed report information

![readme-report1](./readme-pic/readme-report1.png)

### IDEA + Gradle + Scala version

This is similar to the VSCode version, so I won't repeat it here.

The differences are as follows:

- IDEA searches for Scala plugins to install
- New way to run: right click and select Engine.scala file in the project directory, select Run 'Engine' to run the demo (you need to press enter to confirm the run).

### IDEA + Maven + Scala version

This is similar to the VSCode version, so I won't repeat it here.

The differences are as follows:

- IDEA searches for Scala plugins to install
- New way to run: right-click the Engine.scala file in the project directory and select Run 'Engine' to run the demo (you need to press enter to confirm during the run).

## Build your own Gatling project from 0 to 1

### Gradle + Scala versions

#### Create an empty Gradle project

```bash
mkdir gatling-gradle-demo
cd gatling-gradle-demo
gradle init
```

#### Configure the project build.gradle

Add the following to the build.gradle file in the project

> You can copy the content of the build.gradle file in this project, for more configurations, please refer to the [official documentation](https://gatling.io/docs/gatling/reference/current/extensions/gradle_plugin/).

```groovy
// Plugin Configuration
plugins {
    id 'scala' // scala plugin declaration (based on the development tools plugin)
    id 'io.gatling.gradle' version '3.9.5.6' // declaration of the version of the gradle-based gatling framework plugin
}
// Repository source configuration
repositories {
  // Use the maven central repository source
  mavenCentral()
}
// gatling configuration
gatling {
  // logback root level, defaults to the Gatling console log level if logback.xml does not exist in the configuration folder
  logLevel = 'WARN' 

  // Enforce logging of HTTP requests at a level of detail
  // set to 'ALL' for all HTTP traffic in TRACE, 'FAILURES' for failed HTTP traffic in DEBUG
  logHttp = 'FAILURES' 

  // Simulations filter
  simulations = {
      include "**/simulation/*.scala"
  }
}
// Dependencies
dependencies {     
 // Charts library for generating report charts
 gatling 'io.gatling.highcharts:gatling-charts-highcharts:3.8.3'
 }
```

#### gradle build project and initialize

- Open the Terminal window of the project with an editor and execute the following command to confirm that the project build was successful

```bash
gradle build
```

- Initialization complete: After completing the wizard, Gradle will generate a basic Gradle project structure in the project directory
  
![readme-project-tree1](./readme-pic/readme-project-tree1.png)

#### Initialization Directory
  
Create a simulation directory in the src/gatling/scala directory to hold test scripts

> Gatling tests are usually located in the src/gatling directory. You need to manually create the src directory in the project root, and then create the gatling directory under the src directory. In the gatling directory, you can create your test simulation folder simulation, as well as other folders such as data, bodies, resources, and so on.

#### Writing Scripts

- Create a demo.scala file in the simulation directory to write your test scripts.

- For reference, the following is a sample script

> The script contains two scenarios, one for get requests and one for post requests.
> The get interface validates that the interface returns a status code of 200 and the post interface validates that the interface returns a status code of 201.
> The get interface uses rampUsers, the post interface uses constantConcurrentUsers.
> rampUsers: incrementally increase the number of concurrent users over a specified period of time, constantConcurrentUsers: keep the number of concurrent users constant over a specified period of time.
> The number of concurrent users is 10 for both interfaces, and the duration is 10 seconds for both interfaces.
> The request interval is 2 seconds for both interfaces.

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

#### Debugging Scripts

Execute the following command to run the test script and view the report

```bash
gradle gatlingRun
```

![readme-report3](./readme-pic/readme-report3.png)

### Maven + Scala version

#### Create an empty Maven project

```bash
mvn archetype:generate -DgroupId=demo.gatlin.maven -DartifactId=gatling-maven-demo
```

Initialization complete: After completing the wizard, Maven will create a new project directory and generate a basic Maven project structure in the
  
![readme-project-tree2](./readme-pic/readme-project-tree2.png)

#### Configure the project pom.xml

Add the following contents to the pom.xml file in the project

> You can copy the contents of the pom.xml file in this project, for more configuration, please refer to the [official documentation](https://gatling.io/docs/gatling/reference/current/extensions/maven_plugin/).

```xml
<!-- dependencies Configuration -->
<dependencies>
  <dependency>
    <groupId>io.gatling.highcharts</groupId>
    <artifactId>gatling-charts-highcharts</artifactId>
    <version>3.9.5</version>
    <scope>test</scope>
  </dependency>
</dependencies>
<!-- Plugin Configuration -->
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

#### Initialization Directory
  
Create a simulation directory in the src/test/scala directory to hold the test scripts

> scala tests are usually located in the src/test directory. You need to create a scala directory under the project test directory. In the scala directory, you can create your test simulation folder simulation, as well as other folders such as data, bodies, resources, and so on.

#### Writing Scripts

- Create a demo.scala file in the simulation directory to write your test scripts.

- For reference, the following is a sample script

> The script contains two scenarios, one for get requests and one for post requests.
> The get interface validates that the interface returns a status code of 200 and the post interface validates that the interface returns a status code of 201.
> The get interface uses rampUsers, the post interface uses constantConcurrentUsers.
> rampUsers: incrementally increase the number of concurrent users over a specified period of time, constantConcurrentUsers: keep the number of concurrent users constant over a specified period of time.
> The number of concurrent users is 10 for both interfaces, and the duration is 10 seconds for both interfaces.
> The request interval is 2 seconds for both interfaces.

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

#### Debugging Scripts

Execute the following command to run the test script and view the report

```bash
mvn gatling:test
```

![readme-report3](./readme-pic/readme-report3.png)

## Advanced Usage

> To be completed

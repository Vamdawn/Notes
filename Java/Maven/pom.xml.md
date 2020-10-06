# pom.xml 解读

## Overview

> A Project Object Model or POM is the fundamental unit of work in Maven. It is an XML file that contains information about the project and configuration details used by Maven to build the project. It contains default values for most projects. Examples for this is the build directory, which is target; the source directory, which is src/main/java; the test source directory, which is src/test/java; and so on. When executing a task or goal, Maven looks for the POM in the current directory. It reads the POM, gets the needed configuration information, then executes the goal.
>
> Some of the configuration that can be specified in the POM are the project dependencies, the plugins or goals that can be executed, the build profiles, and so on. Other information such as the project version, description, developers, mailing lists and such can also be specified.
>
> http://maven.apache.org/guides/introduction/introduction-to-the-pom.html

## Minimal POM

- project 根元素
- modelVersion 在maven2&maven3必须设置为4.0.0
- groupId 组织标识
- artifactId 项目名称
- version 当前项目版本号

## Dependencies

项目依赖, 通过`<dependencies>`元素中的`<dependency>`来定义依赖

Example:

```xml
<dependencies>
    <dependency>
        <!-- 依赖项组织标识 -->
        <groupId>group.a</groupId>
        <!-- 依赖项项目名称 -->
        <artifactId>artifact</artifactId>
        <!-- 依赖项项目版本 -->
        <version>0.0.1</version>
        <!-- 限制依赖的应用范围: compile(default), provided, runtime, test, system, import -->
        <scope>test</scope>
        <!-- 移除该依赖中指定的依赖项 -->
        <exclusions>
            <exclusion>
            <groupId>group.b</groupId>
            <artifactId>excluded-artifact</artifactId>
            </exclusion>
        </exclusions>
    </dependency>
</dependencies>>
```

## Properities

属性(可以认为是变量), 使用`${propertyName}`的形式引用属性, 自定义属性在`<properties>`标签中定义

Example:

```xml
<properties>
    <hello.world>helloworld</hello.world>
</properties>
```



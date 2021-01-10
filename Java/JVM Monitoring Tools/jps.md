# Commmand: jps

## Introduction

列出指定机器上运行中的java进程

## Usage

```shell
jps [-help]
jps [-q] [-mlvV] [<hostid>]
```

## Arguments

`-q`: 隐藏className, jar文件完整路径名, 传递给main方法的参数, 仅展示jvm进程id

`-m`: 展示传递给main方法的参数

`-l`: 展示应用main.class的完整包名， 或者应用的jar文件完整路径名

`-v`: 展示传递给JVM的参数

`-V`: 不展示传递给JVM的参数【默认】

`<hostid>`: 指定目标机器

## Output Format

```shell
lvmid [ [ classname | JARfilename | "Unknown"] [ arg* ] [ jvmarg* ] ]
```

## Example

```shell
# from https://docs.oracle.com/javase/9/tools/jps.htm#JSWOR733

jps
18027 Java2Demo.JAR
18032 jps
18005 jstat

jps -l remote.domain
3002 /opt/jdk1.7.0/demo/jfc/Java2D/Java2Demo.JAR
2857 sun.tools.jstatd.jstatd

jps -m remote.domain:2002
3002 /opt/jdk1.7.0/demo/jfc/Java2D/Java2Demo.JAR
3102 sun.tools.jstatd.jstatd -p 2002
```
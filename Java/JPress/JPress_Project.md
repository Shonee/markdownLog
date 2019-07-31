JPress项目运行时错误：

```java
[ERROR] Failed to execute goal org.apache.maven.plugins:maven-compiler-plugin:3.5.1:compile (default-compile) on project xxx: Fatal error compiling: 无效的目标发行版: 1.8 -> [Help 1]
//maven使用了jad1.8，而本地版本不对
//添加新版本jdk时，路径选择到jdk中的jre即可  ..\jdk*\jre8
//本地安装jdk1.8后，在eclipse中也要重新引用1.8版本才行
//如果是maven项目，要在jdk上编辑 --> Default VM arguments:    		//  -Dmaven.multiModuleProjectDirectory=$M2_HOME

```



```java
[ERROR] No goals have been specified for this build. You must specify a valid lifecycle phase or a goal in the format <plugin-prefix>:<goal> or <plugin-group-id>:<plugin-artifact-id>[:<plugin-version>]:<goal>. Available lifecycle phases are: validate, initialize, generate-sources, process-sources, generate-resources, process-resources, compile, process-classes, generate-test-sources, process-test-sources, generate-test-resources, process-test-resources, test-compile, process-test-classes, test, prepare-package, package, pre-integration-test, integration-test, post-integration-test, verify, install, deploy, pre-clean, clean, post-clean, pre-site, site, post-site, site-deploy. -> [Help 1]
//goals中没有内容，为其添加compile
//run as --> run configuration内容
```

![1559196359269](D:\markdownLog\JPress\assets\1559196359269.png)



项目右键 --> update maven --> maven clean --> maven install



```java
[ERROR] No plugin found for prefix 'tomcat7' in the current project and in the plugin groups [org.apache.maven.plugins, org.codehaus.mojo] available from the repositories [local (C:\Users\yc\.m2\repository), central (https://repo.maven.apache.org/maven2)] -> [Help 1]
//要设置tomcat7来进行部署
//eclipse中添加tomcat7版本，设置为项目服务器
//项目pom.xml中添加：
    <plugin>
        <groupId>org.apache.tomcat.maven</groupId>
        <artifactId>tomcat7-maven-plugin</artifactId>
        <version>2.2</version>
    </plugin>
```

版本

​	mysql

​	eclipse4.5/jdk1.8

​	maven3.5

​	tomcat7.0(tomcat7:run-war)

在eclipse中运行成功后生成一个war包在start-tomcat文件夹下，要拿到tomcat中去运行



运行成功了，接下来有机会进行二次开发。
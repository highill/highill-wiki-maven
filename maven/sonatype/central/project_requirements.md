

#project_requirements  




<span id = "要求" ></span>  

# 要求 

- [为什么有要求](#为什么有要求)    
- [提供Java文档和源代码](#提供Java文档和源代码)    
- [使用GPG/PGP签名文件](#使用GPG/PGP签名文件)  
- [充分的元数据](#充分的元数据)  
  - [正确的坐标](#正确的坐标)  
  - [项目名, 描述和URL](#项目名, 描述和URL)  
  - [许可信息](#许可信息)  
  - [开发者信息](#开发者信息)    
  - [SCM信息](#SCM信息)    
- [POM完整例子](#POM完整例子)   

<span id = "为什么有要求" ></span>  

## 为什有有要求  

为了保证在中央库里组件可用性的最小水平, 需要确立一些要求. 开发的组件必须满足. 这样允许用户在中央库里根据提供的元数据查找关于组件的关联细节. 下面章节将详述这些要求.  
   
帮助视频: 

- [要求和签名秘诀](https://youtu.be/DE3FVty3NgE)  
- [第一次部署](https://youtu.be/dXR4pJ_zS-0)  
- [工程对象模型POM](https://youtu.be/N7KXuvi_2SE)  
- [Java文档, 源文件和签名](https://youtu.be/HeQ70mRSSGE)  


<span id = "提供Java文档和源代码" ></span>  

## 提供Java文档和源代码  

工程使用 ` pom ` 以外打包需要提供包含文档和源文件的JAR文件. 允许你组件的客户像在他们的IDE里一样显示和导航自动地访问浏览Java文档和源文件. 
Maven仓库下文件命名惯例格式使用分类名 ` javadoc ` 和 ` sources ` 并且组合使用 ` artifactId ` 和 ` version ` 名字并打包为 ` jar `. 举例来说这是用这个值: 

```  
<groupId>com.example.applications</groupId>
<artifactId>example-application</artifactId>
<version>1.4.7</version>
```  

Java文档和源文件归档的文件名使用格式 artidactId-version-classifier.packaging 是  

```  
example-application-1.4.7-sources.jar
example-application-1.4.7-javadoc.jar
```  

如果, 由于一些原因(例如, 许可问题或一个Scala工程), 不能提供 ` -sources.jar ` 或 ` -javadoc.jar `, 请制作伪造的 ` -sources.jar ` 或 ` -javadoc.jar `用简单的README放在里边通过检查. 官方不希望失效规则因为一些人如果它们有选择权趋向跳过它, 并且官方希望尽可能高的保持用户体验的质量.  


   
  
<span id = "使用GPG/PGP签名文件" ></span>  

## 使用GPG/PGP签名文件  

所有部署的文件需要使用GPG/PGP签名, 并且每个文件必须包含签名在` .asc `文件. 举了例子, 如果部署这些文件: 

```  
example-application-1.4.7.pom
example-application-1.4.7.jar
example-application-1.4.7-sources.jar
example-application-1.4.7-javadoc.jar
```  

需要包含这些文件: 

```  
example-application-1.4.7.pom.asc
example-application-1.4.7.jar.asc
example-application-1.4.7-sources.jar.asc
example-application-1.4.7-javadoc.jar.asc
```  

如果需要更新设置和配置GPG的帮助, 请阅读[细节指令](http://central.sonatype.org/pages/working-with-pgp-signatures.html).    



<span id = "充分的元数据" ></span>  

## 充分的元数据  

作为部署的一部分, 需要提交一个 ` pom `文件. 这是` Project Object Model `工程对象模型文件, 使用Apache Maven定义你的工程和构造. 当构建使用其它工具时, 你必须装配他并且确保它包含下面信息.  

在要求信息之外, 强烈建议工程包含正确的依赖, 以便构建工具能使用它的信息去解决正确地传递依赖并且用户不需要手动管理依赖.  
 


<span id = "正确的坐标" ></span>  

### 正确的坐标   

工程坐标, 也被认为是GAV, 坐标决定工程在仓库的位置. 值是:  

- ` groupId ` 工程的顶级命名空间, 使用颠倒的域名开始  
- ` artifactId ` 组件的唯一名称  
- ` version ` 组件的版本字符串   

版本可以是任意的字符串并且不能以 ` -SNAPSHOT ` 结束. 自从这是保留的字符串版本被识别为当前在开发. 不论如何, 强烈建议使用[语义版本](http://semver.org) 帮助用户选择他们的版本.  

一个有效的例子是:  

```  
<groupId>com.example.applications</groupId>
<artifactId>example-application</artifactId>
<version>1.4.7</version>
```  

除非默认的 ` jar `应用, 工程需要添加 ` packaging `. packaging例子值是 ` jar `, ` war `, ` ear `, ` pom `, ` maven-plugin `, ` ejb `, ` rar `, ` par `, ` aar ` 和 ` apklib `使用其它值也是有效的.  


<span id = "项目名, 描述和URL"></span>  

### 项目名, 描述和URL  

为了一些人类可读的关于工程和指出工程网站或更多的信息, 要求填写 ` name `, ` description ` 和 ` url `.  

```  
<name>Example Application</name>
<description>A application used as an example on how to set up pushing 
  its components to the Central Repository.</description>
<url>http://www.example.com/example-application</url>
```  

通用和可接受的命名实践是组合使用Maven属性的坐标:  

```  
<name>${project.groupId}:${project.artifactId}</name>  
```  




<span id = "许可信息" ></span>  

### 许可信息  

你需要声明许可用于散布你的组件. 举个例子, 如果你使用Apache许可你可以使用:  

```  
<licenses>
  <license>
    <name>The Apache License, Version 2.0</name>
    <url>http://www.apache.org/licenses/LICENSE-2.0.txt</url>
  </license>
</licenses>
```  

另一个例子是MIT许可:  

```  
<licenses>
  <license>
    <name>MIT License</name>
    <url>http://www.opensource.org/licenses/mit-license.php</url>
  </license>
</licenses>
```  




<span id = "开发者信息" ></span>  

### 开发者信息  

为了能够联系工程需要添加开发者部分.  

```  
 <developers>
    <developer>
      <name>Manfred Moser</name>
      <email>manfred@sonatype.com</email>
      <organization>Sonatype</organization>
      <organizationUrl>http://www.sonatype.com</organizationUrl>
    </developer>
  </developers>
```  

如果没有网站, 可以接受连接到你GitHub或其他组织的概要描述.



<span id = "SCM信息" ></span>  

### SCM信息  

连接到源代码控制系统是另一个元素. 语法依赖于版本控制系统的使用.  
` connection `详述只读连接, 当 ` developerConnection `详述读和写访问连接细节. ` url ` 包含SCM系统前端地址.  

详细信息在[各种各样支持的格式](http://maven.apache.org/scm/scms-overview.html) 的 [Maven SCM文档](http://maven.apache.org/scm/), 以及若干例子如下.  

自己Subversion的服务: 

```  
<scm>
  <connection>scm:svn:http://subversion.example.com/svn/project/trunk/</connection>
  <developerConnection>scm:svn:https://subversion.example.com/svn/project/trunk/</developerConnection>
  <url>http://subversion.example.com/svn/project/trunk/</url>
</scm>
```  

GitHub上的Git服务:  

```  
<scm>
  <connection>scm:git:git://github.com/simpligility/ossrh-demo.git</connection>
  <developerConnection>scm:git:ssh://github.com:simpligility/ossrh-demo.git</developerConnection>
  <url>http://github.com/simpligility/ossrh-demo/tree/master</url>
</scm>

```  

BitBukcet上的Git服务:  

```  
<scm>
  <connection>scm:git:git://bitbucket.org/simpligility/ossrh-pipeline-demo.git</connection>
  <developerConnection>scm:git:ssh://bitbucket.org:simpligility/ossrh-pipeline-demo.git</developerConnection>
  <url>https://bitbucket.org/simpligility/ossrh-pipeline-demo/src</url>
</scm>
```  

BitBucket上的Mercurial:  

```  
<scm>
  <connection>scm:hg:http://bitbucket.org/juven/hg-demo</connection>
  <developerConnection>scm:hg:https://bitbucket.org/juven/hg-demo</developerConnection>
  <url>http://bitbucket.org/juven/hg-demo</url>
</scm>
```  


来自Apache Maven的Apache Git服务上的Git:  

```  
<scm>
  <connection>scm:git:https://git-wip-us.apache.org/repos/asf/maven.git</connection>
  <developerConnection>scm:git:https://git-wip-us.apache.org/repos/asf/maven.git</developerConnection>
  <url>https://github.com/apache/maven/tree/${project.scm.tag}</url>
  <tag>master</tag>
</scm>
```  






<span id = "POM完整例子" ></span>  

## POM完整例子  

下面完整例子展示了XML头和 ` project ` 和 ` modelVersion ` 的要求元素, 以及例子元素和内容.  

```  
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0" 
xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" 
xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/maven-v4_0_0.xsd">
  <modelVersion>4.0.0</modelVersion>

  <groupId>com.simpligility.training</groupId>
  <artifactId>ossrh-demo</artifactId>
  <version>1.0</version>
  <packaging>jar</packaging>

  <name>ossrh-demo</name>
  <description>A demo for deployment to the Central Repository via OSSRH</description>
  <url>http://github.com/simpligility/ossrh-demo</url>

  <licenses>
    <license>
      <name>The Apache Software License, Version 2.0</name>
      <url>http://www.apache.org/licenses/LICENSE-2.0.txt</url>
    </license>
  </licenses>

  <developers>
    <developer>
      <name>Manfred Moser</name>
      <email>manfred@sonatype.com</email>
      <organization>Sonatype</organization>
      <organizationUrl>http://www.sonatype.com</organizationUrl>
    </developer>
  </developers>

  <scm>
    <connection>scm:git:git://github.com/simpligility/ossrh-demo.git</connection>
    <developerConnection>scm:git:ssh://github.com:simpligility/ossrh-demo.git</developerConnection>
    <url>http://github.com/simpligility/ossrh-demo/tree/master</url>
   </scm>

...

</project>

```  

这些事 ` pom ` 文件的必要条件. 此外阻止 ` <repositories> ` 和 ` <pluginRepositories> ` 的使用, 代替发布任何必需组件到中央库. 这个应用对你的组件来说也是第三方构件.  

完整地配置例子工程包含元数据以及依赖和Maven构建配置, 例如,   

https://github.com/simpligility/ossrh-demo/blob/master/pom.xml  
https://bitbucket.org/simpligility/ossrh-pipeline-demo/src  






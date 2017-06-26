
# central_sonatype.md  

sonatype提供文档, 如何上传新的构建, 使用构建等等.  


# Producers官网文档  
- [Getting Started](http://central.sonatype.org/pages/producers.html)  
- [OSSRH Guide](http://central.sonatype.org/pages/ossrh-guide.html)  
- [Project Requirements](http://central.sonatype.org/pages/requirements.html)  
- [PGP Signing](http://central.sonatype.org/pages/working-with-pgp-signatures.html)  
- [Deploy - Apache Ant](http://central.sonatype.org/pages/apache-ant.html)  
- [Deploy - Apache Maven](http://central.sonatype.org/pages/apache-maven.html)  
- [Deploy - Gradle](http://central.sonatype.org/pages/gradle.html)  
- [Deploy - sbt](http://central.sonatype.org/pages/sbt.html)  
- [Deploy - Manual Deployment](http://central.sonatype.org/pages/manual-staging-bundle-creation-and-deployment.html)   
- [Release](http://central.sonatype.org/pages/releasing-the-deployment.html)   
- [Choosing Your Coordinates](http://central.sonatype.org/pages/choosing-your-coordinates.html)  


- [制作人](#制作人)  
- [OSSRH指导](#OSSRH指导)  
- [要求](#要求)  
- [PGP签名](#PGP签名)  
- [Ant部署](#Ant部署)  




<span id = "制作人" ></span>  

# 制作人  

制作人本质是愿意向中央库公布内容.  

不论是个人的微小的开源工程, 一些工程的一组开发者或者大组织运营你们自己的仓库管理发行开源组件 - 我们能够帮助你将它们发布到中央库, 并且为你的用户提供中央库的权益.  

[benefits of the Central Repository](http://central.sonatype.org/pages/about.html)   

- [个人工程 - 开源软件仓库主机(OSSRH)](#个人工程-开源软件仓库主机)  
- [大组织/大熔炉 - 仓库同步](#大组织大熔炉-仓库同步)  
    - [为什么同步你的熔炉到中央库](#为什么同步你的熔炉到中央库)  
    - [是否已经有人已经这么做](#是否已经有人这么做)    
	- [下一步](#下一步)  

	
<span id = "个人工程-开源软件仓库主机"> </span> 	
## 个人工程-开源软件仓库主机  	

Sonatype的开源软件仓库主机(OSSRH)服务是项目所有者和贡献者向中央库发布他们的组件的主要渠道. 
他是部署了Nexus Repository Manager的主机, 使用[Nexus Staging Suite](http://books.sonatype.com/nexus-book/reference/staging.html) 用于部署过程和验证, 结合同步处理到中央库内容递送网络.  

使用OSSRH需要下面几个简单步骤初始化: 
1. 提供项目详情  
2. 设置你的系统部署到OSSRH  

在那之后, 你能随时公布许多组件和发布提供的Group ID和嵌套Group ID的组件到中央库.  
这些连续的 简单公布到中央库 视频为初学者提供了一些短教程. (详见原文)  

更多详细说明, 请查看我们[每步指导](http://central.sonatype.org/pages/ossrh-guide.html)  




<span id = "大组织大熔炉-仓库同步"> </span>
## 大组织大熔炉-仓库同步   
   
机构运行他们自己的仓库管理也能不使用OSSRH把他们的组件公布到中央库.   


<span id = "为什么同步你的熔炉到中央库">  </span> 
### 为什么同步你的熔炉到中央库  
   
作为软件开发工具链的一部分, 运行你们自己的仓库管理, 允许你保持控制. 配合同步到中央库, 给你们的使用者提供简单访问你们组件和为他们提供中央库的权益.  
 

<span id = "是否已经有人这么做">  </span>  
### 是否已经有人这么做  

很多大熔炉已经同步到中央库, 例如  

- Apache  
- Atlassian  
- eXo Platform  
- JBoss/Redhat  
- Liferay  
- Oracle/ java.net  

 
<span id = "下一步"> </span>  
### 下一步  

<span id = "producersNextSteps">  </span>  
直接联系我们 获取运行你的开源熔炉[Nexus Repository Manager](https://www.sonatype.com/nexus-repository-sonatype) 的许可, 并且获得同步到中央库的帮助. 
[在中央同步上使用Nexus智能代理](http://central.sonatype.org/pages/central-sync-with-nexus-smart-proxy.html)可以找到进一步详细配置.  



<span id = "OSSRH指导" ></span>  

# OSSRH指导  

- [介绍](#介绍)   
- [初始化安装](#初始化安装)  
    - [创建Sonatype门票](#创建Sonatype门票)     
	- [检查要求](#检查要求)     
	- [部署](#部署)  
- [发布到中央库](#发布到中央库)   
- [OSSRH使用说明](#OSSRH使用说明)    
    - [访问仓库](#访问仓库)    


<span id = "介绍"> </span> 	
## 介绍  
Sonatype OSSRH使用 [Sonatype Nexus仓库管理](links.sonatype.com/products/nexus/pro/home)为务必复查[服务条款](http://central.sonatype.org/pages/central-repository-producer-terms.html)开源项目二进制提供仓库主机服务. OSSRH使用的Maven仓库格式允许: 

- 部署开发版本二进制(snapshots 快照)  
- 阶段发布二进制  
- 升级发布二进制和同步它们到中央库  

你的OSSRH仓库初始化设置需要一些手工步骤和人工检查([为什么?](http://central.sonatype.org/articles/2014/Feb/27/why-the-wait/)).
在你的部署过程有代表性的修改组件进入OSSRH. 它们就同步了.    
 
 
<span id = "初始化安装" > </span>
## 初始化安装 

<span id = "创建Sonatype门票"> </span> 
### 创建Sonatype门票  
Sonatype使用JIRA管理请求.  

1. [创建你的JIRA账号](https://issues.sonatype.org/secure/Signup!default.jspa)  
2. [创建新工程门票](https://issues.sonatype.org/secure/CreateIssue.jspa?issuetype=21&pid=10134)  

你的工程由触发器创建. 正常地, 过程少于两个工作日. [为什么等待](http://central.sonatype.org/articles/2014/Feb/27/why-the-wait/) 

帮助视频:  
- [在中央库声明你的名空间](https://youtu.be/P_3yo-oU1To)  
- [申请访问OSSRH](https://youtu.be/0gyF17kWMLg)  

请你已经收到又见通知表名门票被Resolved再部署. 一个重要的常见问题关联到新工程过早部署, 它错误指向你的构建到所有仓库. 最后, 如果你的组件已经在里边, 确保在你的门票里记录, 并且检查如何[移动到OSSRH](http://central.sonatype.org/articles/2014/Feb/27/migrating-a-project-to-ossrh/).  


<span id = "检查要求" > </span> 
### 检查要求 
在中央库有效的组件有基础的元数据和内容. 我们建议当你创建仓库时熟悉它们. 更多细节, [中央库组件要求](http://central.sonatype.org/pages/requirements.html).   

帮助视频:  
- [要求和签名秘诀](https://youtu.be/DE3FVty3NgE)  
- [工程对象模型POM](https://youtu.be/N7KXuvi_2SE)  
- [Java文档, 源文件和签名](https://youtu.be/HeQ70mRSSGE)  

 
<span id = "部署"> </span>
### 部署  
打多数开发可以轻松实现开发程序为了自动满足组建要求. 取决于你选择的工具和方法, 他们有一些不同.  

- [Apache Maven]  
- [Apache Ant]  
- [Gradle]  
- [sbt] 
- [手动实现绑定创建和部署]  

注意: 对任何单一文件上传到OSSRH大概有1024MB的限制. 当达到这个限制上传会失败, 带有管道损坏异常. 如果需要上传大组件需要直接连接官方.    

帮助视频: 
- [第一次部署](https://youtu.be/dXR4pJ_zS-0)  


<span id = "发布到中央库"> </span>  
## 发布到中央库 

此时此刻, 你的工程被部署到私有仓库仅你的工程成员访问. 

发布你的组件, 你能二选一从命令行直接地发布它们, 如果你使用Nexus Staging Maven Plugin或Ant任务或打开你喜欢的浏览器转到 https://oss.sonatype.org/ , 或者按照 [细节指令](http://central.sonatype.org/pages/releasing-the-deployment.html) . 

帮助视频: 
- [访问OSSRH](https://youtu.be/b5D2EBjLp40)  



<span id = "OSSRH使用说明"> </span>  
## OSSRH使用说明   


<span id = "访问仓库"> </span>  
### 访问仓库  

如下仓库允许你直接地在OSSRH访问你的组件. 用户直接地通过中央库获取你的组件, 但是这个列表或许对你工程的提交者和合作者有用. 

- 快照部署和下载访问的仓库地址  
  - https://oss.sonatype.org/content/repositories/snapshots/  
- 发布部署不能下载访问的仓库地址    
  - https://oss.sonatype.org/service/local/staging/deploy/maven2/  
- 发布下载访问的仓库地址, 这个仓库被同步到中央库, 直接部署到这个仓库是不可能的  
  - https://oss.sonatype.org/content/repositories/releases/  
- 包含快照和发布的仓库组  
  - https://oss.sonatype.org/content/groups/public/  


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



<span id = "PGP签名" ></span>  

# 使用PGP签名操作  

- [安装GnuPG](#安装GnuPG)  
- [生成密钥对](#生成密钥对)  
- [密钥列表](#密钥列表)  
- [文件签名](#文件签名)  
- [分发公钥](#分发公钥)  
- [使用构建工具签名](#使用构建工具签名)  
- [处理过期的密钥](#处理过期的密钥)  
- [删除子密钥](#删除子密钥)    

发布组件到中央库的一个条件是, 它们已经被PGP签名. GnuPG或GPG是OpenPGP标准的免费地可用的实现. GPG提供生成签名的能力, 管理密钥, 验证签名. 这也文档使用GPG关联到中央仓库. 在容器里需要:  

- 创建你的密钥对  
- 发布它到密钥服务, 方便用户能够验证它  



<span id = "安装GnuPG"></span>  

## 安装GnuPG  

从 https://www.gnupg.org/download/ 下载GPG或使用喜欢包管理安装, 并且运行带有版本标记的gpg命令验证.  

```  
$ gpg --version
gpg (GnuPG) 1.4.18
Copyright (C) 2014 Free Software Foundation, Inc.
License GPLv3+: GNU GPL version 3 or later <http://gnu.org/licenses/gpl.html>
This is free software: you are free to change and redistribute it.
There is NO WARRANTY, to the extent permitted by law.

Home: ~/.gnupg
Supported algorithms:
Pubkey: RSA, RSA-E, RSA-S, ELG-E, DSA
Cipher: IDEA, 3DES, CAST5, BLOWFISH, AES, AES192, AES256, TWOFISH,
        CAMELLIA128, CAMELLIA192, CAMELLIA256
Hash: MD5, SHA1, RIPEMD160, SHA256, SHA384, SHA512, SHA224
Compression: Uncompressed, ZIP, ZLIB, BZIP2

```  

注意一些系统使用更新的gpg2:  

```  
$ gpg2 --version
gpg (GnuPG) 2.0.28
libgcrypt 1.6.3
Copyright (C) 2015 Free Software Foundation, Inc.
License GPLv3+: GNU GPL version 3 or later <http://gnu.org/licenses/gpl.html>
...

```  


<span id = "生成密钥对"></span>  

## 生成密钥对  

密钥对允许你使用GPG签名构件, 用户随后能验证插件被你签名. 可以生成密钥:  

```  
$ gpg --gen-key
```  

询问类型(RSA)和数量(2048bit)选择密钥默认值. key的有效期默认是永远不过期. 尽管如此一般地建议使用一个值小于两年. 一旦密钥过期能够扩展它, 提供你自己的密钥和已知的密码.  

下一步需要提供姓名, 邮箱和密钥的注释. 这些标识符是必需的, 它们将被下载软件构件的任何人查看以及验证签名. 最后, 你可以提供密码保护你的私钥. 要点是选择安全的密码并且不能泄露给任何人. 这个密码和私钥都是签名构件必须的.  




<span id = "密钥列表"></span>  

## 密钥列表  

一旦密钥对被创建, 可以连同其它安装的密钥一起列出它们:  

```  
$ gpg2 --list-keys

/home/juven/.gnupg/pubring.gpg
------------------------------
pub   1024D/C6EED57A 2010-01-13
uid                  Juven Xu (Juven Xu works at Sonatype) <juven@sonatype.com>
sub   2048g/D704745C 2010-01-13
```  

输出显示了公钥文件的路径. 开始行使用 ` pub `显示了长度(1024D), 密钥标识(C6EED57A), 以及公钥的创建日期(2010-01-13).  

下一行显示了密钥的UID, 它由姓名, 注释和邮箱组成. 最后一行显示了子密钥, 现在不需要关心这些.  

列出私钥可以使用:  

```  
$ gpg2 --list-secret-keys

/home/juven/.gnupg/secring.gpg
------------------------------
sec   1024D/C6EED57A 2010-01-13
uid                  Juven Xu (Juven Xu works at Sonatype)
ssb   2048g/D704745C 2010-01-13
```  

输出和刚才提供的公钥类似.  


<span id = "文件签名"></span>  

## 文件签名  

为任何文件创建一个ACSII格式的签名, 运行下面的gpg命令:  

```  
$ gpg2 -ab temp.java
```  

` -a `选项告诉gpg创建ASCII装甲的输出, ` -b `选项告诉gpg制作一个分离的签名. 如果私钥有密码, 将要被要求密码. 没有密码, 有人伪造构件签名仅需要你的私钥. 密码是保护的额外等级.    

GPG将创建像 ` temp.java.asc `这样的文件. 它是 ` temp.java `的签名. 它需要和主文件一起分发, 因此其他人能使用你的公钥验证主文件.  

```  
$ gpg2 --verify temp.java.asc
```  



<span id = "分发公钥"></span>  

## 分发公钥  

由于其他人需要你的公钥验证你的文件, 你必须分发你的公钥到密钥服务:  

```  
$ gpg2 --keyserver hkp://pool.sks-keyservers.net --send-keys C6EED57A
```  

` -keyserver ` 参数标识目标密钥服务地址, 使用` -send-keys `是希望分发密钥的密钥标识. 可能同步列出公约列表获取密钥标识. 一旦提交到密钥服务, 公钥将被同步到其它密钥服务.  

现在其他人能从密钥服务导入你的公钥到他们本地机器:  

```  
$ gpg2 --keyserver hkp://pool.sks-keyservers.net --recv-keys C6EED57A
```  




<span id = "使用构建工具签名"></span>  

## 使用构建工具签名  

现在已经创建并分发你的密钥, 能继续获取组件最为构件的一部分自动签名. 依赖于构建工具,这个设置都不一样. 查明更多关于这些下一步在指定的章节:  

- [Apache Maven](#http://central.sonatype.org/pages/apache-maven.html)  
- [Apache Ant](#http://central.sonatype.org/pages/apache-ant.html)  
- [Grade](#http://central.sonatype.org/pages/gradle.html)  
- [sbt](#http://central.sonatype.org/pages/sbt.html)  
- [Manual Staging Bundle Creation and Deployment](#http://central.sonatype.org/pages/manual-staging-bundle-creation-and-deployment.html)  


<span id = "处理过期的密钥"></span>  

## 处理过期的密钥  

当生成PGP密钥时, 需要指定密钥多长时间有效. 在那周期之后你可以编辑已存在密钥扩展它的有效时间.  

举个例子, 有一个密钥对有效期在2012-02-27:  

```  
$ gpg2 --list-keys
/Users/juven/.gnupg/pubring.gpg
-------------------------------
pub   2048R/A6BAB25C 2011-08-31 [expires: 2012-02-27]
uid                  Juven Xu (for testing) <test@juvenxu.com>
sub   2048R/DD289F64 2011-08-31 [expires: 2011-02-27]

```  

下面命令使用密钥标识作为参数能编辑密钥:  

```  
$ gpg2 --edit-key A6BAB25C
gpg (GnuPG/MacGPG2) 2.0.17; Copyright (C) 2011 Free Software Foundation, Inc.
This is free software: you are free to change and redistribute it.
There is NO WARRANTY, to the extent permitted by law.

Secret key is available.

pub  2048R/A6BAB25C  created: 2011-08-31  expires: 2012-02-27  usage: SC
                     trust: ultimate      validity: ultimate
sub  2048R/DD289F64  created: 2011-08-31  expires: 2011-02-27  usage: E
(1). Juven Xu (for testing) <test@juvenxu.com>
```  

这里仅有一个密钥, 因此选择1:  

```  
gpg> 1 
pub  2048R/A6BAB25C  created: 2011-08-31  expires: 2012-02-27  usage: SC
                     trust: ultimate      validity: ultimate
sub  2048R/DD289F64  created: 2011-08-31  expires: 2011-02-27  usage: E
(1)* Juven Xu (for testing) <test@juvenxu.com>

```  

将看到 ` * `在 (1)后面, 这意味着选中了这个密钥来编辑. 编辑密钥有效期, 键入下面的命令:  

```  
gpg> expire
Changing expiration time for the primary key.
Please specify how long the key should be valid.
         0 = key does not expire
      <n>  = key expires in n days
      <n>w = key expires in n weeks
      <n>m = key expires in n months
      <n>y = key expires in n years

```  

键入需要的, 例如10m(10个月), 然后确认. 编辑的最后一步是保存你完成的:  

```  
gpg> save
```  

现在可以看到密钥的有效时间更新了:  

```  
$ gpg2 --list-keys
pub   2048R/A6BAB25C 2011-08-31 [expires: 2012-06-26]
uid                  Juven Xu (for testing) &lt;test@juvenxu.com&gt;
sub   2048R/DD289F64 2011-08-31 [expires: 2011-02-27]
```  

最后, 再次分发公钥:  

```  
$ gpg2 --keyserver hkp://pool.sks-keyservers.net --send-keys A6BAB25C
```  



<span id = "删除子密钥"></span>  

## 删除子密钥  

一些PGP工具生成子密钥并且默认使用它们签名. 但是制作Maven工具识别签名, 必须使用主密钥签名构件.  

一些PGP工具默认生成子签名密钥并且使用它签名替代使用主密钥签名. 如果使用它签名构件和部署构件到中央库这是一个问题, 因为Maven和Nexus Repository Manager一样仅能依靠主密钥验证.  

修复这个问题需要删除子签名密钥,这样PGP将使用主密钥签名. 一个想法不论是否有子签名密钥, 使用独有的密钥标识运行下面的命令:  

```  
$ gpg2 --edit-key A6BAB25C
gpg (GnuPG/MacGPG2) 2.0.17; Copyright (C) 2011 Free Software Foundation, Inc.
This is free software: you are free to change and redistribute it.
There is NO WARRANTY, to the extent permitted by law.

Secret key is available.

pub  2048R/A6BAB25C  created: 2011-08-31  expires: 2012-06-26  usage: SC
                     trust: ultimate      validity: ultimate
sub  2048R/DD289F64  created: 2011-08-31  expired: 2011-09-30  usage: E
sub  2048R/8738EC86  created: 2011-12-19  expires: 2012-06-16  usage: S
(1). Juven Xu (for testing) &lt;test@juvenxu.com&gt;
```  

从上面的例子可以看到, 这个密钥有2个子密钥使用标识 ` DD289F64  ` 和 ` 8738EC86  `. 输出也显示了创建时间和过期时间. 这些密钥的用法是重要的. E为了加密, 因此子密钥 ` DD289F64  `仅被用于加密. S为了签名, 因此子密钥 ` 8738EC86  ` 仅被用于签名.  

如果主密钥有S子密钥, 它将用做签名. 否则, 它自己将处理签名工作. 因此, 在我们的例子, 希望删除子密钥 ` 8738EC86  `.  

首先选择希望删除的子密钥, 因为它的索引是2(索引从0开始), 运行命令:  

```  
gpg> key 2
pub  2048R/A6BAB25C  created: 2011-08-31  expires: 2012-06-26  usage: SC
                     trust: ultimate      validity: ultimate
sub  2048R/DD289F64  created: 2011-08-31  expired: 2011-09-30  usage: E
sub* 2048R/8738EC86  created: 2011-12-19  expires: 2012-06-16  usage: S
[ultimate] (1). Juven Xu (for testing) &lt;test@juvenxu.com&gt;
```  

从输出能够看到, 子密钥 ` 8738EC86  `被标记为 ` * `. 现在删除它:  

```  
gpg> delkey
Do you really want to delete this key? (y/N) y

pub  2048R/A6BAB25C  created: 2011-08-31  expires: 2012-06-26  usage: SC
                     trust: ultimate      validity: ultimate
sub  2048R/DD289F64  created: 2011-08-31  expired: 2011-09-30  usage: E
[ultimate] (1). Juven Xu (for testing) &lt;test@juvenxu.com&gt;
```  

小建议    

如果你已经分发公钥, 最好废除签名子密钥替代删除它. 尽管你能控制主密钥作为签名密钥. 废除子密钥, 使用 ` revkey ` 命令代替 ` delkey `.  

现在 ` 8738EC86  ` 不会被列出, 最后一步是保存和改变:  

```  
gpg> save
```  

就是这样, 现在你能铜鼓偶签名文件测试修改, 然后验证它. 输出应该包含一些类似的:  

```  
gpg: Signature made ************************* using *** key ID [YOUR-PRIMARY-KEY-ID]  
```  



<span id = "Ant部署" ></span>  

# Ant部署  

- [介绍使用Apache Ant部署到OSSRH](#介绍使用Apache Ant部署到OSSRH)  
- [编译和创建Jar](#编译和创建Jar)  
- [Java文档和源文件创建Jar](#Java文档和源文件创建Jar)  
- [使用Maven Ant任务签名和部署](#使用Maven Ant任务签名和部署)  
- [签名组件](#签名组件)  
- [使用Apache Ivy部署](#使用Apache Ivy部署)  
- [使用Aether Ant任务部署](#使用Aether Ant任务部署)  
- [Ant例子](#Ant例子)  


<span id = "介绍使用Apache Ant部署到OSSRH" ></span>  

## 介绍使用Apache Ant部署到OSSRH     

Apache Ant能使用多种方式配置组件部署到中央库的完整要求. 事实上, Apache Ant是自己被发布到中央库.  

Apache Ant提供创建组件要求的任务. 使用Apache Ivy或Aether Ant任务能执行部署它自己. Eclipse Aether仓库访问组件使用Maven 3+. 老版本Maven Ant任务尽管使用废弃的Maven 2也能使用.   

下面的例子假设工程目录设置为:  

```  
build.xml
pom.xml
src/
lib/
...

```  

` src ` 目录包含Java源文件代码和 完整要求的` pom.xml `. 位置被存储在 build.xml文件的属性里:  

```  
<property name="src" location="src" />
<property name="build" location="build" />
<property name="dist" location="dist" />

```  

` build ` 和 ` dist `嵌套 ` lib `目录被创建在 ` init `任务.  

```  
<target name="init">
  <mkdir dir="${build}" />
  <mkdir dir="${dist}/lib" />
</target>
```  

组件坐标和名称使用Maven仓库命名规范声明:  

```  
<!-- define Maven coordinates -->
<property name="groupId" value="com.juvenxu" />
<property name="artifactId" value="ant-demo" />
<property name="version" value="1.0-SNAPSHOT" />
<!-- define artifacts' name, which follows the convention of Maven -->
<property name="jar" value="${dist}/lib/${artifactId}-${version}.jar" />
<property name="javadoc-jar" value="${dist}/lib/${artifactId}-${version}-javadoc.jar" />
<property name="sources-jar" value="${dist}/lib/${artifactId}-${version}-sources.jar" />

```  

为简单被Aether或Maven Ant任务使用, 访问OSSRH的证书存储在Maven ` setting.xml `里. Ivy用法使用一个property文件.  



<span id = "编译和创建Jar" ></span>  

## 编译和创建Jar  

在例子里, 编译和创建jar文件使用下面的命令:  

```  
<target name="compile" depends="init">
  <javac srcdir="${src}" destdir="${build}" />
</target>

<target name="jar" depends="compile">
  <!-- build the main artifact -->
  <jar jarfile="${jar}" basedir="${build}" />
</target>
```  


这个任务的主要输出是jar文件, 想要部署的, 命名定义在 ` dist/lib ` 目录 ` jar ` 属性位置的文件, 部署任务将从这里选择它们.   


<span id = "Java文档和源文件创建Jar" ></span>  

## Java文档和源文件创建Jar  

Java文档和源文件jar创建使用下面定义完成的.  

```  
<target name="dist" depends="jar">
  <!-- build the javadoc jar -->
  <javadoc sourcepath="${src}" destdir="${dist}/javadoc" />
  <jar jarfile="${javadoc-jar}">
    <fileset dir="${dist}/javadoc" />
  </jar>

  <!-- build the sources jar -->
  <jar jarfile="${sources-jar}">
    <fileset dir="${src}" />
  </jar>
</target>

```  

此外, 主要结果是适当命名的jar文件在 ` dist/lib `目录里.  


<span id = "使用Maven Ant任务签名和部署"></span>  

## 使用Maven Ant任务签名和部署  

Maven Ant任务能被Maven 部署插件执行.  

在设置上, Maven Ant任务在Ant执行的环境变量上有效, 可以定义 ` stage ` 目标发布到OSSRH.  

```  
<project name="ant-demo" default="deploy" basedir="." xmlns:artifact="antlib:org.apache.maven.artifact.ant">

  <!-- defined maven snapshots and staging repository id and url -->
  <property name="ossrh-snapshots-repository-url" 
    value="https://oss.sonatype.org/content/repositories/snapshots/" />
  <property name="ossrh-staging-repository-url" 
    value="https://oss.sonatype.org/service/local/staging/deploy/maven2/" />
  <!-- there server id in the Maven settings.xml -->
  <property name="ossrh-server-id" value="ossrh" />

  <target name="deploy" depends="dist" description="deploy snapshot version to Maven snapshot repository">
    <artifact:mvn>
      <arg value="org.apache.maven.plugins:maven-deploy-plugin:2.6:deploy-file" />
      <arg value="-Durl=${ossrh-snapshots-repository-url}" />
      <arg value="-DrepositoryId=${ossrh-server-id}" />
      <arg value="-DpomFile=pom.xml" />
      <arg value="-Dfile=${jar}" />
    </artifact:mvn>
  </target>

  <!-- before this, update project version (both build.xml and pom.xml) from SNAPSHOT to RELEASE -->
  <target name="stage" depends="dist" description="deploy release version to Maven staging repository">
    <!-- sign and deploy the main artifact -->
    <artifact:mvn>
      <arg value="org.apache.maven.plugins:maven-gpg-plugin:1.3:sign-and-deploy-file" />
      <arg value="-Durl=${ossrh-staging-repository-url}" />
      <arg value="-DrepositoryId=${ossrh-server-id}" />
      <arg value="-DpomFile=pom.xml" />
      <arg value="-Dfile=${jar}" />
      <arg value="-Pgpg" />
    </artifact:mvn>

    <!-- sign and deploy the sources artifact -->
    <artifact:mvn>
      <arg value="org.apache.maven.plugins:maven-gpg-plugin:1.3:sign-and-deploy-file" />
      <arg value="-Durl=${ossrh-staging-repository-url}" />
      <arg value="-DrepositoryId=${ossrh-server-id}" />
      <arg value="-DpomFile=pom.xml" />
      <arg value="-Dfile=${sources-jar}" />
      <arg value="-Dclassifier=sources" />
      <arg value="-Pgpg" />
    </artifact:mvn>

    <!-- sign and deploy the javadoc artifact -->
    <artifact:mvn>
      <arg value="org.apache.maven.plugins:maven-gpg-plugin:1.3:sign-and-deploy-file" />
      <arg value="-Durl=${ossrh-staging-repository-url}" />
      <arg value="-DrepositoryId=${ossrh-server-id}" />
      <arg value="-DpomFile=pom.xml" />
      <arg value="-Dfile=${javadoc-jar}" />
      <arg value="-Dclassifier=javadoc" />
      <arg value="-Pgpg" />
    </artifact:mvn>
  </target>

  <target name="clean" description="clean up">
    <delete dir="${build}" />
    <delete dir="${dist}" />
  </target>
</project>

```  

将注意到 ` stage `目标调用 ` artifact:mvn `三次, 每次使用一个 ` -Pgpg ` 的参数. 这里假定已经在 ` .m2/settings.xml ` 文件里创建概要文件叫做 ` gpg `. 你可以指定密码解锁私钥. 看下面 ` settings.xml `的例子:  

```  
<settings>
  <servers>
    <server>
      <id>ossrh</id>
      <username>your-username</username>
      <password>your-password</password>
    </server>
  </servers>
  <profiles>
    <profile>
      <id>gpg</id>
      <properties>
        <! -- Optionally specify a different path and name for the gpg executable
              if it differs from the default of "gpg"              
        <gpg.executable>gpg2</gpg.executable>
        -->
        <gpg.passphrase>xxxxxx</gpg.passphrase>
      </properties>
    </profile>
  </profiles>
</settings>
```  

注意这里的在 ` server `块之上的 ` id ` 元素匹配 ` build.xml `使用的变量 ` ossrh-server-id `的值. 这是ant任务当部署到OSSRH时将如何查找你的证书.  



<span id = "签名组件" ></span>  

## 签名组件  

如果你决定直接地使用Ant签名组件, 可以使用[Ant任务签名](#http://commons.apache.org/sandbox/commons-openpgp/signer.html).  


<span id = "使用Apache Ivy部署" ></span>  

## 使用Apache Ivy部署  

[Apache Ivy](#https://ant.apache.org/ivy/) 同样地允许解决发布组件到仓库. 签名的组件使用[发布任务](#http://ant.apache.org/ivy/history/2.2.0/use/publish.html)能被部署到OSSRH.  



<span id = "使用Aether Ant任务部署" ></span>  

## 使用Aether Ant任务部署  

[Aether Ant任务](#https://github.com/eclipse/aether-ant) 使用相同的组件与Maven仓库Apache Maven交互 - Eclipse Aether. 能使用 ` deploy ` 任务 发布签名的组件.  


<span id = "Ant例子"></span>  

## Ant例子  

- [使用Ant和Nexus仓库管理里的Nexus Staging Suite](#https://books.sonatype.com/error.html)  
- [Ant和Aether在Nexus 仓库管理例子文档和例子工程](#https://github.com/sonatype/nexus-book-examples/)  
- [Ant和Ivy在Nexus仓库管理例子文档和例子工程](#https://github.com/sonatype/nexus-book-examples)  
- [Apache Cassandra使用Maven Ant任务](#https://git-wip-us.apache.org/repos/asf?p=cassandra.git;a=blob_plain;f=build.xml;hb=HEAD)  


      

 
 
































      



















































  	




    


	

	
	
	

 





 












































  









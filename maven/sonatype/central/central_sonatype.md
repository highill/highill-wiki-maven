
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





# 制作人(Producers)  

制作人本质是愿意向中央库公布内容.  

不论是个人的微小的开源工程, 一些工程的一组开发者或者大组织运营你们自己的仓库管理发行开源组件 - 我们能够帮助你将它们发布到中央库, 并且为你的用户提供中央库的权益.  

[benefits of the Central Repository](http://central.sonatype.org/pages/about.html)   

- [个人工程 - 开源软件仓库主机(OSSRH)](#producersIndividualProjects)  
- [大组织/大熔炉 - 仓库同步](#producersLargeOrganizations)  
    - [为什么同步你的熔炉到中央库](#producersWhySynchronize)  
    - [是否已经有人已经这么做](#是否已经有人这么做)    
	- [下一步](#producersNextStep)  

	
<span id = "producersIndividualProjects"> </span> 	
## 个人工程 - 开源软件仓库主机	

Sonatype的开源软件仓库主机(OSSRH)服务是项目所有者和贡献者向中央库发布他们的组件的主要渠道. 
他是部署了Nexus Repository Manager的主机, 使用[Nexus Staging Suite](http://books.sonatype.com/nexus-book/reference/staging.html) 用于部署过程和验证, 结合同步处理到中央库内容递送网络.  

使用OSSRH需要下面几个简单步骤初始化: 
1. 提供项目详情  
2. 设置你的系统部署到OSSRH  

在那之后, 你能随时公布许多组件和发布提供的Group ID和嵌套Group ID的组件到中央库.  
这些连续的 简单公布到中央库 视频为初学者提供了一些短教程. (详见原文)  

更多详细说明, 请查看我们[每步指导](http://central.sonatype.org/pages/ossrh-guide.html)  




<span id = "producersLargeOrganizations"> </span>
## 大组织/大熔炉 - 仓库同步  
   
机构运行他们自己的仓库管理也能不使用OSSRH把他们的组件公布到中央库.   


<span id = "producersWhySynchronize">  </span> 
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

 
<span id = "producersNextStep"> </span>  
### 下一步  

<span id = "producersNextSteps">  </span>  
直接联系我们 获取运行你的开源熔炉[Nexus Repository Manager](https://www.sonatype.com/nexus-repository-sonatype) 的许可, 并且获得同步到中央库的帮助. 
[在中央同步上使用Nexus智能代理](http://central.sonatype.org/pages/central-sync-with-nexus-smart-proxy.html)可以找到进一步详细配置.  



# OSSRH指导  

- [介绍](#ossrhGuideIntroduction)   
- [初始化安装](#ossrhGuideInitialSetup)  
    - [创建Sonatype门票](#ossrhGuideCreateTicket)     
	- [检查要求](#ossrhGuideReviewRequirements)     
	- [部署](#ossrhGuideDeployment)  
- [发布到中央库](#ossrhGuideRelease)   
- [OSSRH使用说明](#ossrhGuideOSSRH)    
    - [访问仓库](#ossrhGuideAccessing)    


<span id = "ossrhGuideIntroduction"> </span> 	
## 介绍  
Sonatype OSSRH使用 [Sonatype Nexus仓库管理](links.sonatype.com/products/nexus/pro/home)为务必复查[服务条款](http://central.sonatype.org/pages/central-repository-producer-terms.html)开源项目二进制提供仓库主机服务. OSSRH使用的Maven仓库格式允许: 

- 部署开发版本二进制(snapshots 快照)  
- 阶段发布二进制  
- 升级发布二进制和同步它们到中央库  

你的OSSRH仓库初始化设置需要一些手工步骤和人工检查([为什么?](http://central.sonatype.org/articles/2014/Feb/27/why-the-wait/)).
在你的部署过程有代表性的修改组件进入OSSRH. 它们就同步了.    
 
 
<span id = "ossrhGuideInitialSetup" > </span>
## 初始化安装 

<span id = "ossrhGuideCreateTicket"> </span> 
### 创建Sonatype门票  
Sonatype使用JIRA管理请求.  

1. [创建你的JIRA账号](https://issues.sonatype.org/secure/Signup!default.jspa)  
2. [创建新工程门票](https://issues.sonatype.org/secure/CreateIssue.jspa?issuetype=21&pid=10134)  

你的工程由触发器创建. 正常地, 过程少于两个工作日. [为什么等待](http://central.sonatype.org/articles/2014/Feb/27/why-the-wait/) 

帮助视频:  
- [在中央库声明你的名空间](https://youtu.be/P_3yo-oU1To)  
- [申请访问OSSRH](https://youtu.be/0gyF17kWMLg)  

请你已经收到又见通知表名门票被Resolved再部署. 一个重要的常见问题关联到新工程过早部署, 它错误指向你的构建到所有仓库. 最后, 如果你的组件已经在里边, 确保在你的门票里记录, 并且检查如何[移动到OSSRH](http://central.sonatype.org/articles/2014/Feb/27/migrating-a-project-to-ossrh/).  


<span id = "ossrhGuideReviewRequirements" > </span> 
### 检查要求 
在中央库有效的组件有基础的元数据和内容. 我们建议当你创建仓库时熟悉它们. 更多细节, [中央库组件要求](http://central.sonatype.org/pages/requirements.html).   

帮助视频:  
- [要求和签名秘诀](https://youtu.be/DE3FVty3NgE)  
- [工程对象模型POM](https://youtu.be/N7KXuvi_2SE)  
- [Java文档, 源文件和签名](https://youtu.be/HeQ70mRSSGE)  

 
<span id = "ossrhGuideDeployment"> </span>
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


<span id = "ossrhGuideRelease"> </span>  
## 发布到中央库 

此时此刻, 你的工程被部署到私有仓库仅你的工程成员访问. 

发布你的组件, 你能二选一从命令行直接地发布它们, 如果你使用Nexus Staging Maven Plugin或Ant任务或打开你喜欢的浏览器转到 https://oss.sonatype.org/ , 或者按照 [细节指令](http://central.sonatype.org/pages/releasing-the-deployment.html) . 

帮助视频: 
- [访问OSSRH](https://youtu.be/b5D2EBjLp40)  



<span id = "ossrhGuideOSSRH"> </span>  
## OSSRH使用说明   


<span id = "ossrhGuideAccessing"> </span>  
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


# 要求 

- [为什么有要求](#为什么有要求)    
- [提供Java文档和源代码](#提供Java文档和源代码)    
- [使用GPG/PGP签名文件](#使用GPG/PGP签名文件)  
- [充分的元数据](#充分的元数据)  
  - [正确的坐标]  
  - [项目名, 描述和URL]  
  - [许可信息]
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























































  	




    


	

	
	
	

 





 












































  









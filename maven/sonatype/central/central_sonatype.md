
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
    - [是否已经有人已经这么做](#producersIsAnybodyDoing)    
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
 

<span id = "producersIsAnybodyDoing">  </span>  
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


  








































  	




    


	

	
	
	

 





 












































  









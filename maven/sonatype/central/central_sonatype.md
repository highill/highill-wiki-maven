
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
	- [下一步](#producersNextSteps)  

	
## 个人工程 - 开源软件仓库主机	

<span id = "producersIndividualProjects"> </span>  

Sonatype的开源软件仓库主机(OSSRH)服务是项目所有者和贡献者向中央库发布他们的组件的主要渠道. 
他是部署了Nexus Repository Manager的主机, 使用[Nexus Staging Suite](http://books.sonatype.com/nexus-book/reference/staging.html) 用于部署过程和验证, 结合同步处理到中央库内容递送网络.  

使用OSSRH需要下面几个简单步骤初始化: 
1. 提供项目详情  
2. 设置你的系统部署到OSSRH  

在那之后, 你能随时公布许多组件和发布提供的Group ID和嵌套Group ID的组件到中央库.  
这些连续的 简单公布到中央库 视频为初学者提供了一些短教程. (详见原文)  

更多详细说明, 请查看我们[每步指导](http://central.sonatype.org/pages/ossrh-guide.html)  





## 大组织/大熔炉 - 仓库同步  
<span id = "producersLargeOrganizations"> </span>   
机构运行他们自己的仓库管理也能不使用OSSRH把他们的组件公布到中央库.   



### 为什么同步你的熔炉到中央库  

<span id = "producersWhySynchronize">  </span>    
作为软件开发工具链的一部分, 运行你们自己的仓库管理, 允许你保持控制. 配合同步到中央库, 给你们的使用者提供简单访问你们组件和为他们提供中央库的权益.  
 


### 是否已经有人这么做  

<span id = "producersIsAnybodyDoing">  </span>  
很多大熔炉已经同步到中央库, 例如  

- Apache  
- Atlassian  
- eXo Platform  
- JBoss/Redhat  
- Liferay  
- Oracle/ java.net  

 

### 下一步  

<span id = "producersNextSteps">  </span>  
直接联系我们 获取运行你的开源熔炉[Nexus Repository Manager](https://www.sonatype.com/nexus-repository-sonatype) 的许可, 并且获得同步到中央库的帮助. 
[在中央同步上使用Nexus智能代理](http://central.sonatype.org/pages/central-sync-with-nexus-smart-proxy.html)可以找到进一步详细配置.  








    


	

	
	
	

 





 












































  









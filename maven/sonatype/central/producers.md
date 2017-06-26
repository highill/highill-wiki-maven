

# producers  


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





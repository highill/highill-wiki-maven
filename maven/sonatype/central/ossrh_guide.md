

# ossrh_guide  



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

  
  
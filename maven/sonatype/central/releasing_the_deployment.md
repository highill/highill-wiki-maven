
# releasing_the_deployment.md  

- [介绍从OSSRH到中央库发布部署](#介绍从OSSRH到中央库发布部署)  
- [登录到OSSRH](#登录到OSSRH)  
- [定位和检查暂存仓库](#定位和检查暂存仓库)  
- [关闭删除或者发布暂存仓库](#关闭删除或者发布暂存仓库)  




<span id = "介绍从OSSRH到中央库发布部署" ></span>  

# 介绍从OSSRH到中央库发布部署  

在成功地部署到OSSRH之后, 组件被存放在隔离的, 临时的仓库, 对项目成员来说是私有的. 为了获取这些发布的组件, 需要`release`它们. 如果在仓库里检验时发现任何问题, 也可以 _Drop_ 暂存仓库. 允许在解决任何问题后再次运行部署, 避免这些组件发布到release仓库, 并且有序地进入中央库.  

通常这个过程是手动地完成, 但是也可能被命令行触发.  

<span id = "登录到OSSRH" ></span>  

# 登录到OSSRH  

为了访问和使用暂存仓库工作需要登录到OSSRH有效地址 https://oss.sonatype.org/.  使用 OSSRH的JIRA问题追踪系统的用户名和密码, 并且 _Login_ 链接在 OSSRH用户界面的右手边最上角.   

帮助视频:  
- [访问OSSRH](https://youtu.be/b5D2EBjLp40)  


<span id = "定位和检查暂存仓库" ></span>  

# 定位和检查暂存仓库   

一旦登录将能够访问在左手边导航的 _Build Promotion_ 菜单, 并且选择 _Staging Repositories_ 元素. _Staging Repository_页签随着一长串的仓库被显示.  

在部署时创建的暂存仓库命名使用工程的groupId开始, 使用移除圆点拼接破折号和4位数字. 举个例子, 如果工程的groupId是 com.example.applications, staging profile名称应该使用 comexampleapplications开始. 序列号从1000开始, 每次部署时递增, 因此可以举个例子, 暂存仓库命名为 ` comexampleapplication-1010 `.  

选择暂存仓库, 下面的面板列表将展示关于仓库的更多细节. 此外, _Close_ 和 _Release_ 按钮将被激活.  

<span id = "关闭删除或者发布暂存仓库" ></span>  

# 关闭删除或者发布暂存仓库  

部署到仓库之后将是 ` Open ` 状态. 可以使用 ` Contents ` 页签评估部署到仓库里的组件. 如果相信任何事情都是正确的, 可以按下列表上的 ` Close ` 按钮. 这将会触发组件违反[先决条件](http://central.sonatype.org/pages/requirements.html)的评估.  

如果你的组件不满足要求将会关闭失败. 如果发生了, 可以按下 _Drop_, 暂存仓库将被删除. 这允许改正组件和部署处理的任何问题, 并且重新运行部署. _Activity_ 页签下面的选择列表有可用的细节. 选择独立的步骤获取更多细节.  

一旦已经成功关闭暂存仓库, 可以通过按住 _Release_按钮 发布它. 这将移动组件到OSSRH的release仓库, 并被同步到中央库.  

如果你是第一次发布, 不要忘记在问题追踪ticket上评论, 让官网知道已经完成发布, 因此官网可以激活同步处理.  

注意使用Nexus Staging Maven插件和Ant任务部署, 默认情况下, 在部署时自动地试图关闭暂存仓库并且可以同样使用来自命令行发布暂存仓库. 这允许避免完全登录到OSSRH用户界面. 更多细节可以在这个指导的[Maven](http://central.sonatype.org/pages/apache-maven.html)和[Ant](http://central.sonatype.org/pages/apache-ant.html)章节发现.  



 

 




















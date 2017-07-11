
# choosing_your_coordinates.md   

# 选择坐标  

` groupId ` 标识工程唯一的贯穿所有工程和全部名空间的控制部分. 与[Java包命名规范]((http://docs.oracle.com/javase/tutorial/java/package/namingpkgs.html)相似, 它重新利用域名系统反转的方式. 这意味着控制域名, 可以使用任何 groupId 使用反转域名开始并且细分以希望的方式创建.  

举个例子, 如果控制 _example.com_ , 可以使用任何以 _com.example_ 开始的groupId. 举个例子 _com.example.domain_ , _com.example.testsupport_ 等等. 

其它例子是:  

- www.springframework.org -> org.springframework  
- oness.sf.net -> net.sf.oness  
- github.com/youusername -> com.github.yourusername  

工程使用artifacts已经上传到中央库, 可以等同于之前使用过的, 即使这违反了约定.  

一个好的方式决定groupId的粒度是使用工程结构. 那就是, 如果当前工程是多模块工程, 应该添加一个新的标识符到父工程的groupId - 举个例子, _org.apache.maven_ , _org.apache.maven.plugins_ , _org.apache.maven.reporting_ .  

_artifactId_ 是工程自己的名字. 可以选择任何希望的小写字母并且没有奇怪符号. 更长的名字使用破折号分割比较常见 - _maven-core_ , _commons-math_ .  

对于_version_官方建议遵循语义化数字管理, 为了传达有意义的数字到用户和给予版本一个可以理解的顺序. 不论如何, 没有指定要求版本必须是数字.  



# 为分配第三方构件groupId的政策  

这信息是为处理不希望直接地上传它们的构件到中央库的第三方工程. 如果希望部署 _own project_ 到中央库, 请使用[OSSRH指导](http://central.sonatype.org/pages/ossrh-guide.html).  

当大多数工程理解发布构件到中央库的重要性, 仍有少量工程不在这里, 不具有相同的价值. 当一个工程拒绝上传构件到中央库, 由于任何原因, 比如许可限制, 鼓励用户自己提交构件包到中央库.  

如果希望在中央库里获取一个特定的库, 所有你需要做的就是在  https://issues.sonatype.org/ 签约一个账户, 创建一个构件包, 并且上传它到暂存仓库. Sonatype将执行一些到期的注意程度, 以确保构件有一个使用无限制分发的兼容的许可, 并且将促进上传的构件到中央Maven仓库.  

一旦已经上传包, Nexus Repository Manager发送消息到Sonatype的管理员. 官方将在构件上执行一些检查. 将检查是否构件已经发布到中央库. 也可能发送一些问题确认已经尝试联系原始工程让他们发布构件, 官网将在包上传一个工作日内回复. 如果包上传被提升, 将受到一个邮件确认提升. 如果包上传被删除, 也将收到来自Nexus Repository Manager的邮件, 然后告诉为什么包被删除.  

Sonatype仍然相信构件最好被工程管理, 然后创建它们, 但是, 在不少情况下, 已经运行的工程里拒绝答复社区的要求. 如果依赖一个没有发布构件到中央库的工程, 或者如果它们看起来是不活跃的. 请利用能力上传自己的构件包.  






 











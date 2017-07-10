
# deploy_with_manual_deployment.md  

- [介绍手动地部署到OSSRH](#介绍手动地部署到OSSRH)  
- [签名组件](#签名组件)  
- [包创建](#包创建)  


<span id = "介绍手动地部署到OSSRH" ></span>  

# 介绍手动地部署到OSSRH  

在某些情况下, 有不在控制下的工具创建的组件, 或者希望上传已经存在的组件. 有两种方式可以直接地部署它们到OSSRH:  

- 可以使用Maven GPG插件签名和上传它们  
- 可以手动地签名它们并且创建包上传  

手动部署处理也可以用于如果不想设置在 一步一步指导的 ` Deployment(部署)`章节 提及的[构建工具](http://central.sonatype.org/pages/ossrh-guide.html).  


<span id= "签名组件" ></span>  

# 签名组件  

比如说希望签名和部署这些组件:  

```  
ossrh-test-1.2.pom
ossrh-test-1.2.jar
ossrh-test-1.2-javadoc.jar
ossrh-test-1.2-sources.jar

```  

可以使用maven-gpg-plugin通过运行如下命令签名和上传它们:  

```  
$ mvn gpg:sign-and-deploy-file -Durl=https://oss.sonatype.org/service/local/staging/deploy/maven2/ -DrepositoryId=ossrh -DpomFile=ossrh-test-1.2.pom -Dfile=ossrh-test-1.2.jar
```  

对于jar本身. 当签名和部署分类时, 比如源代码和java文档, 需要指定 -Dclassifier 参数.  

```  
$ mvn gpg:sign-and-deploy-file -Durl=https://oss.sonatype.org/service/local/staging/deploy/maven2/ -DrepositoryId=ossrh -DpomFile=ossrh-test-1.2.pom -Dfile=ossrh-test-1.2-sources.jar -Dclassifier=sources
$ mvn gpg:sign-and-deploy-file -Durl=https://oss.sonatype.org/service/local/staging/deploy/maven2/ -DrepositoryId=ossrh -DpomFile=ossrh-test-1.2.pom -Dfile=ossrh-test-1.2-javadoc.jar -Dclassifier=javadoc

```  

gpg插件将使用在POM文件里指定的打包形式作为文件扩展名. 作为一种选择, 可以指定 ` -Dpackaging=jar ` 和使用同样语义其它打包值比如 ` war `. 注意, 在 ` -DrepositoryId `里指定的值, 必须匹配在 ` settings.xml ` 里的 ` server ` 元素如下配置:  

```  
<settings>
  ...
  <servers>
    ...
    <server>
      <id>ossrh</id>
      <username>your-jira-id</username>
      <password>your-jira-pwd</password>
    </server>
  </servers>
  ...
</settings>

```  

 




<span id = "包创建" ></span>  

# 包创建  

作为一种选择, 可以手动地签名构件, 创建包, 上传包. 再次, 比如有下面的构件:  

```  
ossrh-test-1.2.pom
ossrh-test-1.2.jar
ossrh-test-1.2-javadoc.jar
ossrh-test-1.2-sources.jar
```  

首先需要签名每个文件. 可以使用[GnuPG](https://www.gnupg.org/), OpenPGP标准的一个免费地可用实现, 在工作目录通过运行如下命令签名文件:  

```  
$ gpg -ab ossrh-test-1.2.pom
$ gpg -ab ossrh-test-1.2.jar
$ gpg -ab ossrh-test-1.2-javadoc.jar
$ gpg -ab ossrh-test-1.2-sources.jar
```  

更多关于使用GnuPGP生成签名, 管理密钥, 验证签名的细节在[这里](http://central.sonatype.org/pages/working-with-pgp-signatures.html).  

然后应该有:  

```  
ossrh-test-1.2.pom
ossrh-test-1.2.pom.asc
ossrh-test-1.2.jar
ossrh-test-1.2.jar.asc
ossrh-test-1.2-javadoc.jar
ossrh-test-1.2-javadoc.jar.asc
ossrh-test-1.2-sources.jar
ossrh-test-1.2-sources.jar.asc
```  

可以使用类似的命令创建一个包命名 ` bundle.jar ` :  

```  
$ jar -cvf bundle.jar ossrh-test-1.2.pom ossrh-test-1.2.pom.asc ossrh-test-1.2.jar ossrh-test-1.2.jar.asc ossrh-test-1.2-javadoc.jar ossrh-test-1.2-javadoc.jar.asc ossrh-test-1.2-sources.jar ossrh-test-1.2-sources.jar.asc
```  

一旦 ` bundle.jar `被产生, 登录到[OSSRH](https://oss.sonatype.org/), 选择左侧 _Build Promotion_ 菜单的 _Staging Upload_ .  

从 _Staging Upload_ 页签, 选择来自 _Upload Mode_ 下拉列表的 _Artifact Bundle_ .  

点击 _Select Bundle To Upload_ 按钮, 选择刚刚创建的包.  

点击 _Upload Bundle_ 按钮. 如果上传成功, staging仓库将被创建, 可以使用[发布](http://central.sonatype.org/pages/releasing-the-deployment.html)处理.   











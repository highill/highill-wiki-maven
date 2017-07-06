
# deploy_with_gradle.md  

- [介绍使用Grade部署到中央库](#介绍使用Grade部署到中央库)  
- [元数据和签名](#元数据和签名)    
- [Jar文件](#Jar文件)  
- [签名构件](#签名构件)  
- [元数据定义和上传](#元数据定义和上传)  
- [证书](#证书)  
- [部署](#部署)  
- [发布部署到中央库](#发布部署到中央库)  
- [链接](#链接)  





<span id = "介绍使用Grade部署到中央库" ></span>  

# 介绍使用Grade部署到中央库  

正如[Gradle](https://gradle.org/) 能简单地配置[消费](http://central.sonatype.org/pages/consumers.html)来自中央库的组件, 它能配置发布到OSSRH.  


<span id = "元数据和签名" ></span>  

# 元数据和签名  

为了使用Gradle部署组件到OSSRH. 必须查看 ` pom.xml `元数据的[要求](http://central.sonatype.org/pages/requirements.html), 替代要求和签名组件.  

` maven ` [Gradle插件](https://docs.gradle.org/current/userguide/maven_plugin.html) 可以照料元数据, 生成要求的 ` pom.xml ` 文件, 和照料构建输出到仓库的部署, ` signing ` [插件](https://docs.gradle.org/current/userguide/signing_plugin.html) 允许获取组件, 创建标准的Gradle任务和签名.  

```  
apply plugin: 'maven'
apply plugin: 'signing'
```  



<span id = "Jar文件" ></span>  

# Jar文件  

典型的Java工程可以添加 ` javadocJar ` 和 ` sourcesJar `任务  

```  
task javadocJar(type: Jar) {
    classifier = 'javadoc'
    from javadoc
}

task sourcesJar(type: Jar) {
    classifier = 'sources'
    from sourceSets.main.allSource
}
```  

并且连接它们到构件集合和工程jar一起  

```  
artifacts {
    archives javadocJar, sourcesJar
}
```  


<span id = "签名构件" ></span>  

# 签名构件  

定义构件使用签名  

```  
signing {
    sign configurations.archives
}
```  


<span id = "元数据定义和上传" ></span>  

# 元数据定义和上传  

为了准备实际的上传, 必须使用maven插件的帮助定义所有元数据. Group 和 version 在工程的最顶层, 为 archiveTask配置artifactId.   

```  
group = "com.example.applications"
archivesBaseName = "example-application"
version = "1.4.7"

```  

生成的pom文件必须被签名并且所有签名的构件必须被上传. 所有这些作为 ` uploadArchives `配置的一部分配置.  

```  
uploadArchives {
  repositories {
    mavenDeployer {
      beforeDeployment { MavenDeployment deployment -> signing.signPom(deployment) }

      repository(url: "https://oss.sonatype.org/service/local/staging/deploy/maven2/") {
        authentication(userName: ossrhUsername, password: ossrhPassword)
      }

      snapshotRepository(url: "https://oss.sonatype.org/content/repositories/snapshots/") {
        authentication(userName: ossrhUsername, password: ossrhPassword)
      }

      pom.project {
        name 'Example Application'
        packaging 'jar'
        // optionally artifactId can be defined here 
        description 'A application used as an example on how to set up 
          pushing  its components to the Central Repository.'
        url 'http://www.example.com/example-application'

        scm {
          connection 'scm:svn:http://foo.googlecode.com/svn/trunk/'
          developerConnection 'scm:svn:https://foo.googlecode.com/svn/trunk/'
          url 'http://foo.googlecode.com/svn/trunk/'
        }

        licenses {
          license {
            name 'The Apache License, Version 2.0'
            url 'http://www.apache.org/licenses/LICENSE-2.0.txt'
          }
        }

        developers {
          developer {
            id 'manfred'
            name 'Manfred Moser'
            email 'manfred@sonatype.com'
          }
        }
      }
    }
  }
}

```  

来自Grade工程的依赖将被放入生成的pom文件.  



<span id = "证书" ></span>  

# 证书  

签名和上传的证书存储在用户目录下 ` gradle.properties ` 文件里. 内容应该如下  

```  
signing.keyId=YourKeyId
signing.password=YourPublicKeyPassword
signing.secretKeyRingFile=PathToYourKeyRingFile

ossrhUsername=your-jira-id
ossrhPassword=your-jira-password
```  




<span id = "部署" ></span>  

# 部署  

使用这个配置适当的开始部署  

```   
gradle uploadArchives
```  




<span id = "发布部署到中央库" ></span>  

# 发布部署到中央库  

一旦部署完成, 可以继续手动地[发布](http://central.sonatype.org/pages/releasing-the-deployment.html)组件.  

作为一种选择, 可以使用设置使用Nexus Staging Ant任务包装Gradle自动与staging仓库交互. 一个可见的例子[Nexus Repository Manager文档例子工程](https://github.com/sonatype/nexus-book-examples/). 使用[Gradle Nexus Staging插件](https://github.com/Codearte/gradle-nexus-staging-plugin/)能够达到同样自动操作.  

两种途径允许完全地组件发布通过OSSRH到中央库.    


<span id = "链接" ></span>  

# 链接  

- [Gradle](https://gradle.org/)网站  
- [Gradle发布](https://docs.gradle.org/current/userguide/artifact_management.html)文档  
- 在仓库管理和Nexus里使用Gradle和Nexus Staging Suite  
- [在Nexus 仓库管理文档里Gradle例子工程](https://github.com/sonatype/nexus-book-examples/)  
- [关于部署到OSSRH博客地址](http://yennicktrevels.com/blog/2013/10/11/automated-gradle-project-deployment-to-sonatype-oss-repository/)  
- [Gradle Nexus Staging插件](https://github.com/Codearte/gradle-nexus-staging-plugin/)  
- [关于在Nexus 上使用Gradle Nexus Staging插件的博客地址](http://www.sonatype.org/nexus/2015/03/31/nexus-staging-plugin-automatic-releasepromotion-of-artifacts-to-maven-central-from-gradle/)  
- [使用gradle-mvn-push 发布Android压缩包(AAR)](https://github.com/chrisbanes/gradle-mvn-push)  













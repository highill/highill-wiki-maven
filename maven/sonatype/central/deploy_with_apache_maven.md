


# deploy_with_apache_maven  


# Maven部署  

- [介绍使用Apache Maven部署到OSSRH](#介绍使用Apache_Maven部署到OSSRH)  
- [其他先决条件](#其他先决条件)  
- [帮助视频](#帮助视频)  
- [分布式管理和认证](#分布式管理和认证)   
- [Java文档和源文件附件](#Java文档和源文件附件)  
- [GPG签名组件](#GPG签名组件)  
- [Nexus Staging Maven插件适合部署和发布](#Nexus_Staging_Maven插件适合部署和发布)  
- [弃用的oss-parent](#弃用的oss-parent)  
- [使用配置文件](#使用配置文件)  
- [执行快照部署](#执行快照部署)  
- [执行发布部署](#执行发布部署)  
- [使用Maven发布插件执行发布部署](#使用Maven发布插件执行发布部署)  
- [手动发布部署到中央库](#手动发布部署到中央库)  
- [附加信息](#附加信息)  



<span id = "介绍使用Apache_Maven部署到OSSRH" > </span>  

## 介绍使用Apache_Maven部署到OSSRH  

Apache Maven开始于分发它所有的组件和要求的依赖到中央库 - 那时以Maven Central著称. Maven是预配置连接到中央库并且从中央库下载一切它需要的包含的工程依赖.  

推荐使用Maven 3的稳定版, 自从Apache Maven的其他版本包含Maven 2和Maven 1的所有版本生命周期结束, 并且不再被工程维护者支持. 有一些关于签名组件和其它方面的已知问题使用一些旧的Maven发布版本.  

Maven构建配置可以在各种方法里设置完整的必要条件, 并且将在下面讨论所有可应用的细节.  

注意当这些指令是Sonatype深思熟虑的最佳实践, 不同意见可以查找[附加信息](#附加信息) 章节下面的其它文档链接.  


<span id = "其他先决条件" ></span>  

## 其他先决条件  

和Apache Maven安装无关, Maven GPG插件要求必须在命令行路径安装有GPG客户端. 更多信息, 请参照https://www.gnupg.org/ 和 下面的[插件文档](http://maven.apache.org/plugins/maven-gpg-plugin/).     


<span id = "帮助视频" ></span>  

## 帮助视频  

- [必要条件和签名技巧](https://youtu.be/DE3FVty3NgE)  
- [第一次部署](https://youtu.be/dXR4pJ_zS-0)  
- [工程对象模型POM](https://youtu.be/N7KXuvi_2SE)  
- [Java文档, 源代码和签名](https://youtu.be/HeQ70mRSSGE)  



<span id = "分布式管理和认证" ></span>  

## 分布式管理和认证  

为了使用Nexus Staging Maven插件配置Maven部署到OSSRH Nexus Repository Manager, 需要这样配置:  

```  
<distributionManagement>
  <snapshotRepository>
    <id>ossrh</id>
    <url>https://oss.sonatype.org/content/repositories/snapshots</url>
  </snapshotRepository>
</distributionManagement>
<build>
  <plugins>
    <plugin>
      <groupId>org.sonatype.plugins</groupId>
      <artifactId>nexus-staging-maven-plugin</artifactId>
      <version>1.6.7</version>
      <extensions>true</extensions>
      <configuration>
        <serverId>ossrh</serverId>
        <nexusUrl>https://oss.sonatype.org/</nexusUrl>
        <autoReleaseAfterClose>true</autoReleaseAfterClose>
      </configuration>
    </plugin>
    ...
  </plugins>
</build>

```  

由于OSSRH一直使用Sonatype Nexus Repository Manager的最新版本, 最好使用Nexus Staging Maven插件的最新版本.  

作为一种选择, 可以使用Maven部署插件, 它是默认的行为, 需要添加完整的 ` distributionManagement `部分:  

```  
<distributionManagement>
  <snapshotRepository>
    <id>ossrh</id>
    <url>https://oss.sonatype.org/content/repositories/snapshots</url>
  </snapshotRepository>
  <repository>
    <id>ossrh</id>
    <url>https://oss.sonatype.org/service/local/staging/deploy/maven2/</url>
  </repository>
</distributionManagement>

```  

上面配置从Maven ` settings.xml ` 获取用户账号细节并部署到OSSRH. 使用认证的最小设置是:  

```  
<settings>
  <servers>
    <server>
      <id>ossrh</id>
      <username>your-jira-id</username>
      <password>your-jira-pwd</password>
    </server>
  </servers>
</settings>
```  

在` settings.xml `里server元素的 ` id ` 元素和 在 ` snapshotRepository `和 ` repository ` 里的 ` id ` 元素是一样的, 也和Nexus Staging Maven插件的 ` serverId ` 配置一样.  

  

<span id = "Java文档和源文件附件" ></span>  

## Java文档和源文件附件  

得到生成的Java文档和源代码jar文件, 需要配置Java文档和源代码Maven插件.  

```  
<build>
  <plugins>
    <plugin>
      <groupId>org.apache.maven.plugins</groupId>
      <artifactId>maven-source-plugin</artifactId>
      <version>2.2.1</version>
      <executions>
        <execution>
          <id>attach-sources</id>
          <goals>
            <goal>jar-no-fork</goal>
          </goals>
        </execution>
      </executions>
    </plugin>
    <plugin>
      <groupId>org.apache.maven.plugins</groupId>
      <artifactId>maven-javadoc-plugin</artifactId>
      <version>2.9.1</version>
      <executions>
        <execution>
          <id>attach-javadocs</id>
          <goals>
            <goal>jar</goal>
          </goals>
        </execution>
      </executions>
    </plugin>
  </plugins>
</build>

```  





<span id = "GPG签名组件" ></span>  

## GPG签名组件  

Maven GPG插件使用下面的配置完成签名组件.  

```  
<build>
  <plugins>
    <plugin>
      <groupId>org.apache.maven.plugins</groupId>
      <artifactId>maven-gpg-plugin</artifactId>
      <version>1.5</version>
      <executions>
        <execution>
          <id>sign-artifacts</id>
          <phase>verify</phase>
          <goals>
            <goal>sign</goal>
          </goals>
        </execution>
      </executions>
    </plugin>
  </plugins>
</build>

```  

信任来自settings.xml有效的GPG证书和安装的gpg命令. 另外万一来自不同的gpg可以配置gpg命令. 这是一些操作系统的命令场景:  

```  
<settings>
  <profiles>
    <profile>
      <id>ossrh</id>
      <activation>
        <activeByDefault>true</activeByDefault>
      </activation>
      <properties>
        <gpg.executable>gpg2</gpg.executable>
        <gpg.passphrase>the_pass_phrase</gpg.passphrase>
      </properties>
    </profile>
  </profiles>
</settings>

```  

需要更多关于设置和配置GPG的帮助, 请阅读[细节命令](http://central.sonatype.org/pages/working-with-pgp-signatures.html).  


<span id = "Nexus_Staging_Maven插件适合部署和发布" ></span>  

## Nexus_Staging_Maven插件适合部署和发布  

Nexus Staging Maven插件是部署组件到OSSRH和发布它们带中央库的推荐方式. 在pom.xml可以简单地配置插件.  

```  
<build>
<plugins>
...
<plugin>
  <groupId>org.sonatype.plugins</groupId>
  <artifactId>nexus-staging-maven-plugin</artifactId>
  <version>1.6.7</version>
  <extensions>true</extensions>
  <configuration>
     <serverId>ossrh</serverId>
     <nexusUrl>https://oss.sonatype.org/</nexusUrl>
     <autoReleaseAfterClose>true</autoReleaseAfterClose>
  </configuration>
</plugin>

```  

如果版本是发布版本(没有以 -SNAPSHOT结尾)并且使用合适的设置, 可以运行部署到OSSRH并且通常自动发布到中央库:  

```  
mvn clean deploy  

```  

使用autoReleaseAfterClose属性设置为false, 可以手动地检查Nexus Repository Manager的 staging仓库, 并且稍后触发staging仓库的发布.  

```  
mvn nexus-staging:release  
```  

如果发现一些错误, 可以删除staging仓库:  

```  
mvn nexus-staging:drop  
```  

请阅读在Nexus的Repository Management里的图书[使用Nexus Staging Suite促进构建](http://books.sonatype.com/nexus-book/reference/staging.html) 获取更多关于Nexus Maven插件的信息.  



<span id = "弃用的oss-parent" ></span>  

## 弃用的oss-parent  

过去所有的插件配置和设置被使用 ` org.sonatype.oss:oss-parent:9 `最后坐标的 Maven parent POM管理. 这个工程缺少SCM, URL和其它细节, 并且它已经阻止使用. 项目已经停止维护并且不在配合像Maven版本或Java版本工具工作. 如果希望, 请管理自己的类似方式的组织层次POM.  


<span id = "使用配置文件" ></span>  

## 使用配置文件  

自从Java文档和源文件jar生成和使用GPG签名组件一样, 是个相当消耗时间的处理, 这些执行有代表地从正常构建配置分离, 并且移动到一个profile. 这个profile当部署被profile激活执行时打开使用.  

```  
<profiles>
  <profile> 
    <id>release</id>
    <build>
      ...
      javadoc, source and gpg plugin from above
      ...
    </build>
  </profile>
</profiles>

```  



<span id = "执行快照部署" ></span>  

## 执行快照部署  

当版本以 ` -SNAPSHOT ` 结束时执行快照部署. 执行快照部署时不需要满足要求, 简单在工程上运行  

```  
mvn clean deploy
```  

快照版本不同步到中央库. 如果希望你的用户消费快照版本, 他们需要添加快照仓库到他们Nexus Repository Manager, settings.xml或 pom.xml. 成功地部署SNAPSHOT版本将出现在 https://oss.sonatype.org/content/repositories/snapshots/ .  



<span id = "执行发布部署" ></span>  

## 执行发布部署  

为了执行发布部署, 需要编辑所有POM文件的 ` version `使用发布版本. 意味着不能使用  ` -SNAPSHOT `结尾, 并且依赖声明也不能使用快照版本. 确保仅依赖其它发布组件. 理想地它们全部在中央库里有效. 确保你的用户可以在中央库检索你的组件和它的依赖.  

工程版本的改变, 多个模块上一层依赖的设置, 可以手动地执行或使用Maven版本插件的帮助.  

```  
mvn versions:set -DnewVersion=1.2.3
```  

一旦更新所有版本并确信构建通过没有部署, 可以使用 ` release `profile的用法执行部署:  

```  
mvn clean deploy -P release  

```  

这个过程完全地独立于SCM系统的工作流. 如果希望确保在中央库里的指定版本符合SCM系统里的指定版本, 它是一个好的实践. 你可以二选一像下面一样手动地提交:  

- 开发, 开发, 开发  
- 提交显著的变动  
- 验证构建通过  
- 更新版本到发布版本  
- 提交发布版本  
- 运行部署  
- 更新版本到下一个快照版本  
- 提交新的快照版本  
- 开发, 开发, 开发并且重新和重复  

或者你能选择包含配置的运行在CI服务上的脚本自动地使用它, 或者使用Maven发布插件, 下面是文档.    



<span id = "使用Maven发布插件执行发布部署" ></span>  

## 使用Maven发布插件执行发布部署  

[Maven发布插件](http://maven.apache.org/components/maven-release/maven-release-plugin/) 能被用于自动更改Maven POM文件, 合理性检查, SCM操作要去和实际部署执行.  

Maven发布插件的配置应该包含禁用的release profile, 它是Maven Super POM的一部分, 自从使用自己的profile, 指定部署目前和激活 `release` profile是一起的.  

```  
<plugin>
  <groupId>org.apache.maven.plugins</groupId>
  <artifactId>maven-release-plugin</artifactId>
  <version>2.5.3</version>
  <configuration>
    <autoVersionSubmodules>true</autoVersionSubmodules>
    <useReleaseProfile>false</useReleaseProfile>
    <releaseProfiles>release</releaseProfiles>
    <goals>deploy</goals>
  </configuration>
</plugin>

```  

使用SCM连接正确地配置, 可以执行发布部署到OSSRH使用:  

```  
mvn release:clean release:prepare
```  

通过应答版本和标签的提示, 下面通过  

```  
mvn release:perform
```  

一下子执行部署到OSSRH并且发布到中央库, 感谢Nexus Staging Maven插件用法将autoReleaseAfterClose设置为true.  



<span id = "手动发布部署到中央库" ></span>  

## 手动发布部署到中央库  

如果使用autoReleaseAfterClose设置为false或者使用默认的Maven部署插件, 可以[手动地检查和潜在地发布部署构建](http://central.sonatype.org/pages/releasing-the-deployment.html).  

作为一种选择, 如果已经使用Nexus Staging Maven插件部署, 并且部署成功, 可以直接地在命令行发布到仓库. 之后立即部署包含所有信息要求在目标目录里的属性文件, 可以简单地发布到staging仓库使用  

```  
mvn nexus-staging:release
```  

如果你已经使用Maven发布插件运行部署发布完成的一部分, 部署完成从版本控制系统检出到 target/checkout, 这样需要从这里运行Nexus Staging插件:  

```  
mvn release:perform
...
cd target/checkout
mvn nexus-staging:release

```  

通过在部署后添加执行目标, 可以使用发布插件配置这个目标作为发布部署的一部分自动地运行  

```  
<plugin>
  <groupId>org.apache.maven.plugins</groupId>
  <artifactId>maven-release-plugin</artifactId>
  <configuration>
    <goals>deploy nexus-staging:release</goals>
    ...
	
```  



<span id = "附加信息" ></span>  

## 附加信息  

- [使用本地仓库管理和OSSRH](http://central.sonatype.org/articles/2014/Mar/25/using-a-local-repo-manager-and-ossrh/). 使用OSSRH临时的组件部署的一种方法  
- [样例工程](https://github.com/simpligility/ossrh-demo)和[视频](https://www.youtube.com/watch?time_continue=2&v=N8_2-hpTnFA)展示完整工程创建和部署, 系列视频[使用Nexus Staging Suite授权发布](http://www.sonatype.org/nexus/members-only/video-gallery-2/free-training/)的一部分  
- 使用样例工程使用文档和视频展示使用BitBucket Pipelines[博客地址](http://www.sonatype.org/nexus/2016/05/24/sonatype-automated-deployments-with-atlassian-bitbucket-pipelines/])  
- [maven 标记](http://central.sonatype.org/tag/maven.html)所有条款  





















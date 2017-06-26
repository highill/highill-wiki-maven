

# deploy_with_apache_ant

<span id = "Ant部署" ></span>  

# Ant部署  

- [介绍使用Apache Ant部署到OSSRH](#介绍使用Apache_Ant部署到OSSRH)  
- [编译和创建Jar](#编译和创建Jar)  
- [Java文档和源文件创建Jar](#Java文档和源文件创建Jar)  
- [使用Maven Ant任务签名和部署](#使用Mave_Ant任务签名和部署)  
- [签名组件](#签名组件)  
- [使用Apache Ivy部署](#使用Apache_Ivy部署)  
- [使用Aether Ant任务部署](#使用Aether_Ant任务部署)  
- [Ant例子](#Ant例子)  


<span id = "介绍使用Apache_Ant部署到OSSRH" ></span>  

## 介绍使用Apache_Ant部署到OSSRH     

Apache Ant能使用多种方式配置组件部署到中央库的完整要求. 事实上, Apache Ant是自己被发布到中央库.  

Apache Ant提供创建组件要求的任务. 使用Apache Ivy或Aether Ant任务能执行部署它自己. Eclipse Aether仓库访问组件使用Maven 3+. 老版本Maven Ant任务尽管使用废弃的Maven 2也能使用.   

下面的例子假设工程目录设置为:  

```  
build.xml
pom.xml
src/
lib/
...

```  

` src ` 目录包含Java源文件代码和 完整要求的` pom.xml `. 位置被存储在 build.xml文件的属性里:  

```  
<property name="src" location="src" />
<property name="build" location="build" />
<property name="dist" location="dist" />

```  

` build ` 和 ` dist `嵌套 ` lib `目录被创建在 ` init `任务.  

```  
<target name="init">
  <mkdir dir="${build}" />
  <mkdir dir="${dist}/lib" />
</target>
```  

组件坐标和名称使用Maven仓库命名规范声明:  

```  
<!-- define Maven coordinates -->
<property name="groupId" value="com.juvenxu" />
<property name="artifactId" value="ant-demo" />
<property name="version" value="1.0-SNAPSHOT" />
<!-- define artifacts' name, which follows the convention of Maven -->
<property name="jar" value="${dist}/lib/${artifactId}-${version}.jar" />
<property name="javadoc-jar" value="${dist}/lib/${artifactId}-${version}-javadoc.jar" />
<property name="sources-jar" value="${dist}/lib/${artifactId}-${version}-sources.jar" />

```  

为简单被Aether或Maven Ant任务使用, 访问OSSRH的证书存储在Maven ` setting.xml `里. Ivy用法使用一个property文件.  



<span id = "编译和创建Jar" ></span>  

## 编译和创建Jar  

在例子里, 编译和创建jar文件使用下面的命令:  

```  
<target name="compile" depends="init">
  <javac srcdir="${src}" destdir="${build}" />
</target>

<target name="jar" depends="compile">
  <!-- build the main artifact -->
  <jar jarfile="${jar}" basedir="${build}" />
</target>
```  


这个任务的主要输出是jar文件, 想要部署的, 命名定义在 ` dist/lib ` 目录 ` jar ` 属性位置的文件, 部署任务将从这里选择它们.   


<span id = "Java文档和源文件创建Jar" ></span>  

## Java文档和源文件创建Jar  

Java文档和源文件jar创建使用下面定义完成的.  

```  
<target name="dist" depends="jar">
  <!-- build the javadoc jar -->
  <javadoc sourcepath="${src}" destdir="${dist}/javadoc" />
  <jar jarfile="${javadoc-jar}">
    <fileset dir="${dist}/javadoc" />
  </jar>

  <!-- build the sources jar -->
  <jar jarfile="${sources-jar}">
    <fileset dir="${src}" />
  </jar>
</target>

```  

此外, 主要结果是适当命名的jar文件在 ` dist/lib `目录里.  


<span id = "使用Mave_Ant任务签名和部署"></span>  

## 使用Mave_Ant任务签名和部署  

Maven Ant任务能被Maven 部署插件执行.  

在设置上, Maven Ant任务在Ant执行的环境变量上有效, 可以定义 ` stage ` 目标发布到OSSRH.  

```  
<project name="ant-demo" default="deploy" basedir="." xmlns:artifact="antlib:org.apache.maven.artifact.ant">

  <!-- defined maven snapshots and staging repository id and url -->
  <property name="ossrh-snapshots-repository-url" 
    value="https://oss.sonatype.org/content/repositories/snapshots/" />
  <property name="ossrh-staging-repository-url" 
    value="https://oss.sonatype.org/service/local/staging/deploy/maven2/" />
  <!-- there server id in the Maven settings.xml -->
  <property name="ossrh-server-id" value="ossrh" />

  <target name="deploy" depends="dist" description="deploy snapshot version to Maven snapshot repository">
    <artifact:mvn>
      <arg value="org.apache.maven.plugins:maven-deploy-plugin:2.6:deploy-file" />
      <arg value="-Durl=${ossrh-snapshots-repository-url}" />
      <arg value="-DrepositoryId=${ossrh-server-id}" />
      <arg value="-DpomFile=pom.xml" />
      <arg value="-Dfile=${jar}" />
    </artifact:mvn>
  </target>

  <!-- before this, update project version (both build.xml and pom.xml) from SNAPSHOT to RELEASE -->
  <target name="stage" depends="dist" description="deploy release version to Maven staging repository">
    <!-- sign and deploy the main artifact -->
    <artifact:mvn>
      <arg value="org.apache.maven.plugins:maven-gpg-plugin:1.3:sign-and-deploy-file" />
      <arg value="-Durl=${ossrh-staging-repository-url}" />
      <arg value="-DrepositoryId=${ossrh-server-id}" />
      <arg value="-DpomFile=pom.xml" />
      <arg value="-Dfile=${jar}" />
      <arg value="-Pgpg" />
    </artifact:mvn>

    <!-- sign and deploy the sources artifact -->
    <artifact:mvn>
      <arg value="org.apache.maven.plugins:maven-gpg-plugin:1.3:sign-and-deploy-file" />
      <arg value="-Durl=${ossrh-staging-repository-url}" />
      <arg value="-DrepositoryId=${ossrh-server-id}" />
      <arg value="-DpomFile=pom.xml" />
      <arg value="-Dfile=${sources-jar}" />
      <arg value="-Dclassifier=sources" />
      <arg value="-Pgpg" />
    </artifact:mvn>

    <!-- sign and deploy the javadoc artifact -->
    <artifact:mvn>
      <arg value="org.apache.maven.plugins:maven-gpg-plugin:1.3:sign-and-deploy-file" />
      <arg value="-Durl=${ossrh-staging-repository-url}" />
      <arg value="-DrepositoryId=${ossrh-server-id}" />
      <arg value="-DpomFile=pom.xml" />
      <arg value="-Dfile=${javadoc-jar}" />
      <arg value="-Dclassifier=javadoc" />
      <arg value="-Pgpg" />
    </artifact:mvn>
  </target>

  <target name="clean" description="clean up">
    <delete dir="${build}" />
    <delete dir="${dist}" />
  </target>
</project>

```  

将注意到 ` stage `目标调用 ` artifact:mvn `三次, 每次使用一个 ` -Pgpg ` 的参数. 这里假定已经在 ` .m2/settings.xml ` 文件里创建概要文件叫做 ` gpg `. 你可以指定密码解锁私钥. 看下面 ` settings.xml `的例子:  

```  
<settings>
  <servers>
    <server>
      <id>ossrh</id>
      <username>your-username</username>
      <password>your-password</password>
    </server>
  </servers>
  <profiles>
    <profile>
      <id>gpg</id>
      <properties>
        <! -- Optionally specify a different path and name for the gpg executable
              if it differs from the default of "gpg"              
        <gpg.executable>gpg2</gpg.executable>
        -->
        <gpg.passphrase>xxxxxx</gpg.passphrase>
      </properties>
    </profile>
  </profiles>
</settings>
```  

注意这里的在 ` server `块之上的 ` id ` 元素匹配 ` build.xml `使用的变量 ` ossrh-server-id `的值. 这是ant任务当部署到OSSRH时将如何查找你的证书.  



<span id = "签名组件" ></span>  

## 签名组件  

如果你决定直接地使用Ant签名组件, 可以使用[Ant任务签名](#http://commons.apache.org/sandbox/commons-openpgp/signer.html).  


<span id = "使用Apache_Ivy部署" ></span>  

## 使用Apache_Ivy部署  

[Apache Ivy](#https://ant.apache.org/ivy/) 同样地允许解决发布组件到仓库. 签名的组件使用[发布任务](#http://ant.apache.org/ivy/history/2.2.0/use/publish.html)能被部署到OSSRH.  



<span id = "使用Aether_Ant任务部署" ></span>  

## 使用Aether_Ant任务部署    

[Aether Ant任务](#https://github.com/eclipse/aether-ant) 使用相同的组件与Maven仓库Apache Maven交互 - Eclipse Aether. 能使用 ` deploy ` 任务 发布签名的组件.  


<span id = "Ant例子"></span>  

## Ant例子  

- [使用Ant和Nexus仓库管理里的Nexus Staging Suite](#https://books.sonatype.com/error.html)  
- [Ant和Aether在Nexus 仓库管理例子文档和例子工程](#https://github.com/sonatype/nexus-book-examples/)  
- [Ant和Ivy在Nexus仓库管理例子文档和例子工程](#https://github.com/sonatype/nexus-book-examples)  
- [Apache Cassandra使用Maven Ant任务](#https://git-wip-us.apache.org/repos/asf?p=cassandra.git;a=blob_plain;f=build.xml;hb=HEAD)  



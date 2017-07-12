
# use_maven_submit_artifact.md  

Maven是一款软件项目管理和理解工具. 基于工程对象模型(project object model - POM)的概念, Maven可以从一段中心信息管理工程的构建, 报告, 文档. 

Maven所依赖的组件大部分存放在中央库. 将通用组件上传到中央库也方便用户或协作团队使用.  

下面是Maven和中央库相关文档 

- [Maven主页](http://maven.apache.org/)  
- [中央库文档](http://central.sonatype.org/)  
- [中央库提交构件文档](http://central.sonatype.org/pages/producers.html)  

中央库提交构件文档列表还有 OSSRH Guide, Project Requirements, PGP Signing, Deploy, Release等文档.  


# 中央库构件要求  

- 提供Java文档和源代码  
- 使用GPG/PGP签名文件  
- 完整的POM工程信息和依赖组件信息  
- 坐标完整. groupId artifactId, version  
- 许可信息  
- 开发者信息  
- SCM信息  

向中央库提交构件, 需要创建账号并申请新工程工单.  

- [在中央库创建JIRA账号](https://issues.sonatype.org/secure/Signup!default.jspa)  
- [新工程申请工单](https://issues.sonatype.org/secure/CreateIssue.jspa?issuetype=21&pid=10134)  


# Java工程  

## 许可信息  

```  
	<licenses>
		<license>
			<name>The Apache License, Version 2.0</name>
			<url>http://www.apache.org/licenses/LICENSE-2.0.txt</url>
		</license>
	</licenses>

```  

## 开发者信息  

```  
	<developers>
		<developer>
			<name>Li Dongxu</name>
			<email>hapfish@vip.qq.com</email>
			<organization>highill</organization>
			<organizationUrl>https://github.com/highill</organizationUrl>
		</developer>
	</developers>
```  

##　SCM  

```  
	<scm>
		<connection>scm:git:git://github.com/highill/highill-base.git</connection>
		<developerConnection>scm:git:ssh://github.com/highill/highill-base.git</developerConnection>
		<url>https://github.com/highill/highill-base</url>
	</scm>
	
```  

## OSSRH配置  

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
	
	需要在setting.xml配置  
	
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


## Java源代码和文档  

```  
    <build>
		<plugins>

			<!-- maven java source plugin -->
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

			<!-- maven java doc plugin -->
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


## 安装GPG  

下载GPG 
https://www.gnupg.org/download/ 

Windows下载地址  https://www.gpg4win.org/download.html  

```  

安装GPG生成密钥对 

>gpg --version
gpg (GnuPG) 2.0.30 (Gpg4win 2.3.4)
libgcrypt 1.7.8
Copyright (C) 2015 Free Software Foundation, Inc.
License GPLv3+: GNU GPL version 3 or later <http://gnu.org/licenses/gpl.html>
This is free software: you are free to change and redistribute it.
There is NO WARRANTY, to the extent permitted by law.

Home: C:/Users/东旭/AppData/Roaming/gnupg
Supported algorithms:
Pubkey: RSA, RSA, RSA, ELG, DSA
Cipher: IDEA, 3DES, CAST5, BLOWFISH, AES, AES192, AES256, TWOFISH,
        CAMELLIA128, CAMELLIA192, CAMELLIA256
Hash: MD5, SHA1, RIPEMD160, SHA256, SHA384, SHA512, SHA224
Compression: Uncompressed, ZIP, ZLIB, BZIP2

>gpg2 --version
gpg (GnuPG) 2.0.30 (Gpg4win 2.3.4)
libgcrypt 1.7.8
Copyright (C) 2015 Free Software Foundation, Inc.
License GPLv3+: GNU GPL version 3 or later <http://gnu.org/licenses/gpl.html>
This is free software: you are free to change and redistribute it.
There is NO WARRANTY, to the extent permitted by law.

Home: C:/Users/东旭/AppData/Roaming/gnupg
Supported algorithms:
Pubkey: RSA, RSA, RSA, ELG, DSA
Cipher: IDEA, 3DES, CAST5, BLOWFISH, AES, AES192, AES256, TWOFISH,
        CAMELLIA128, CAMELLIA192, CAMELLIA256
Hash: MD5, SHA1, RIPEMD160, SHA256, SHA384, SHA512, SHA224
Compression: Uncompressed, ZIP, ZLIB, BZIP2

>gpg2 --list-keys
>gpg2 --list-secret-keys

>gpg --gen-key

gpg (GnuPG) 2.0.30; Copyright (C) 2015 Free Software Foundation, Inc.
This is free software: you are free to change and redistribute it.
There is NO WARRANTY, to the extent permitted by law.

Please select what kind of key you want:
   (1) RSA and RSA (default)
   (2) DSA and Elgamal
   (3) DSA (sign only)
   (4) RSA (sign only)
Your selection? 4
RSA keys may be between 1024 and 4096 bits long.
What keysize do you want? (2048) 4096
Requested keysize is 4096 bits
Please specify how long the key should be valid.
         0 = key does not expire
      <n>  = key expires in n days
      <n>w = key expires in n weeks
      <n>m = key expires in n months
      <n>y = key expires in n years
Key is valid for? (0) 0
Key does not expire at all
Is this correct? (y/N) y

GnuPG needs to construct a user ID to identify your key.

Real name: Li Dongxu
Email address: hapfish@vip.qq.com
Comment: Li Dongxu RSA 4096
You selected this USER-ID:
    "Li Dongxu (Li Dongxu RSA 4096) <hapfish@vip.qq.com>"

Change (N)ame, (C)omment, (E)mail or (O)kay/(Q)uit? O
You need a Passphrase to protect your secret key.

We need to generate a lot of random bytes. It is a good idea to perform
some other action (type on the keyboard, move the mouse, utilize the
disks) during the prime generation; this gives the random number
generator a better chance to gain enough entropy.
gpg: key E5BBB37F marked as ultimately trusted
public and secret key created and signed.

gpg: checking the trustdb
gpg: 3 marginal(s) needed, 1 complete(s) needed, PGP trust model
gpg: depth: 0  valid:   1  signed:   0  trust: 0-, 0q, 0n, 0m, 0f, 1u
pub   4096R/E5BBB37F 2017-07-12
      Key fingerprint = C450 299C B1C0 B6D1 FF27  385E 1D03 4131 E5BB B37F
uid       [ultimate] Li Dongxu (Li Dongxu RSA 4096) <hapfish@vip.qq.com>

Note that this key cannot be used for encryption.  You may want to use
the command "--edit-key" to generate a subkey for this purpose.

>gpg2 --list-keys
C:/Users/东旭/AppData/Roaming/gnupg/pubring.gpg
-----------------------------------------------
pub   4096R/E5BBB37F 2017-07-12
uid       [ultimate] Li Dongxu (Li Dongxu RSA 4096) <hapfish@vip.qq.com>


>gpg2 --list-secret-keys

C:/Users/东旭/AppData/Roaming/gnupg/secring.gpg
-----------------------------------------------
sec   4096R/E5BBB37F 2017-07-12
uid                  Li Dongxu (Li Dongxu RSA 4096) <hapfish@vip.qq.com>

>gpg2 -ab C:\Downloads\gnupg-2.1.21.tar.bz2
>gpg2 --verify C:\Downloads\gnupg-2.1.21.tar.bz2.asc
gpg: assuming signed data in 'C:\\Downloads\\gnupg-2.1.21.tar.bz2'
gpg: Signature made 07/12/17 18:14:14 中国标准时间 using RSA key ID E5BBB37F
gpg: Good signature from "Li Dongxu (Li Dongxu RSA 4096) <hapfish@vip.qq.com>" [ultimate]



分发公钥 
>gpg2 --keyserver hkp://pool.sks-keyservers.net --send-keys E5BBB37F
gpg: sending key E5BBB37F to hkp server pool.sks-keyservers.net

其他人导入公钥 
gpg2 --keyserver hkp://pool.sks-keyservers.net --recv-keys E5BBB37F

```  



## GPG签名  




```  

			<!-- maven pgp sign plugin -->
			<plugin>
				<groupId>org.apache.maven.plugins</groupId>
				<artifactId>maven-gpg-plugin</artifactId>
				<version>1.6</version>
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


settings.xml需要配置

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

	
			
			

```  



# 准备部署  

```  
com.highill.base has been prepared, now user(s) hapfish can:

    Deploy snapshot artifacts into repository https://oss.sonatype.org/content/repositories/snapshots
    Deploy release artifacts into the staging repository https://oss.sonatype.org/service/local/staging/deploy/maven2
    Promote staged artifacts into repository 'Releases'
    Download snapshot and release artifacts from group https://oss.sonatype.org/content/groups/public
    Download snapshot, release and staged artifacts from staging group https://oss.sonatype.org/content/groups/staging

please comment on this ticket when you promoted your first release, thanks

先部署到snapshots仓库验证  
mvn clean deploy 


https://oss.sonatype.org/content/repositories/snapshots/com/highill/base/highill-base/

https://oss.sonatype.org/content/groups/public/com/highill/base/highill-base/  

https://oss.sonatype.org/content/groups/staging/com/highill/base/highill-base/


正式部署  

>mvn versions:set -DnewVersion=0.0.0.1
>mvn clean deploy -P release

http://search.maven.org/



# 在cmd命令行下, 无法使用git没有权限提交代码  
>mvn versions:set -DnewVersion=0.0.0.1-SNAPSHOT
>mvn release:clean 
>mvn release:prepare

>mvn 








```  








  


# working_with_pgp_signatures  




<span id = "PGP签名" ></span>  

# PGP签名  

- [安装GnuPG](#安装GnuPG)  
- [生成密钥对](#生成密钥对)  
- [密钥列表](#密钥列表)  
- [文件签名](#文件签名)  
- [分发公钥](#分发公钥)  
- [使用构建工具签名](#使用构建工具签名)  
- [处理过期的密钥](#处理过期的密钥)  
- [删除子密钥](#删除子密钥)    

发布组件到中央库的一个条件是, 它们已经被PGP签名. GnuPG或GPG是OpenPGP标准的免费地可用的实现. GPG提供生成签名的能力, 管理密钥, 验证签名. 这也文档使用GPG关联到中央仓库. 在容器里需要:  

- 创建你的密钥对  
- 发布它到密钥服务, 方便用户能够验证它  



<span id = "安装GnuPG"></span>  

## 安装GnuPG  

从 https://www.gnupg.org/download/ 下载GPG或使用喜欢包管理安装, 并且运行带有版本标记的gpg命令验证.  

```  
$ gpg --version
gpg (GnuPG) 1.4.18
Copyright (C) 2014 Free Software Foundation, Inc.
License GPLv3+: GNU GPL version 3 or later <http://gnu.org/licenses/gpl.html>
This is free software: you are free to change and redistribute it.
There is NO WARRANTY, to the extent permitted by law.

Home: ~/.gnupg
Supported algorithms:
Pubkey: RSA, RSA-E, RSA-S, ELG-E, DSA
Cipher: IDEA, 3DES, CAST5, BLOWFISH, AES, AES192, AES256, TWOFISH,
        CAMELLIA128, CAMELLIA192, CAMELLIA256
Hash: MD5, SHA1, RIPEMD160, SHA256, SHA384, SHA512, SHA224
Compression: Uncompressed, ZIP, ZLIB, BZIP2

```  

注意一些系统使用更新的gpg2:  

```  
$ gpg2 --version
gpg (GnuPG) 2.0.28
libgcrypt 1.6.3
Copyright (C) 2015 Free Software Foundation, Inc.
License GPLv3+: GNU GPL version 3 or later <http://gnu.org/licenses/gpl.html>
...

```  


<span id = "生成密钥对"></span>  

## 生成密钥对  

密钥对允许你使用GPG签名构件, 用户随后能验证插件被你签名. 可以生成密钥:  

```  
$ gpg --gen-key
```  

询问类型(RSA)和数量(2048bit)选择密钥默认值. key的有效期默认是永远不过期. 尽管如此一般地建议使用一个值小于两年. 一旦密钥过期能够扩展它, 提供你自己的密钥和已知的密码.  

下一步需要提供姓名, 邮箱和密钥的注释. 这些标识符是必需的, 它们将被下载软件构件的任何人查看以及验证签名. 最后, 你可以提供密码保护你的私钥. 要点是选择安全的密码并且不能泄露给任何人. 这个密码和私钥都是签名构件必须的.  




<span id = "密钥列表"></span>  

## 密钥列表  

一旦密钥对被创建, 可以连同其它安装的密钥一起列出它们:  

```  
$ gpg2 --list-keys

/home/juven/.gnupg/pubring.gpg
------------------------------
pub   1024D/C6EED57A 2010-01-13
uid                  Juven Xu (Juven Xu works at Sonatype) <juven@sonatype.com>
sub   2048g/D704745C 2010-01-13
```  

输出显示了公钥文件的路径. 开始行使用 ` pub `显示了长度(1024D), 密钥标识(C6EED57A), 以及公钥的创建日期(2010-01-13).  

下一行显示了密钥的UID, 它由姓名, 注释和邮箱组成. 最后一行显示了子密钥, 现在不需要关心这些.  

列出私钥可以使用:  

```  
$ gpg2 --list-secret-keys

/home/juven/.gnupg/secring.gpg
------------------------------
sec   1024D/C6EED57A 2010-01-13
uid                  Juven Xu (Juven Xu works at Sonatype)
ssb   2048g/D704745C 2010-01-13
```  

输出和刚才提供的公钥类似.  


<span id = "文件签名"></span>  

## 文件签名  

为任何文件创建一个ACSII格式的签名, 运行下面的gpg命令:  

```  
$ gpg2 -ab temp.java
```  

` -a `选项告诉gpg创建ASCII装甲的输出, ` -b `选项告诉gpg制作一个分离的签名. 如果私钥有密码, 将要被要求密码. 没有密码, 有人伪造构件签名仅需要你的私钥. 密码是保护的额外等级.    

GPG将创建像 ` temp.java.asc `这样的文件. 它是 ` temp.java `的签名. 它需要和主文件一起分发, 因此其他人能使用你的公钥验证主文件.  

```  
$ gpg2 --verify temp.java.asc
```  



<span id = "分发公钥"></span>  

## 分发公钥  

由于其他人需要你的公钥验证你的文件, 你必须分发你的公钥到密钥服务:  

```  
$ gpg2 --keyserver hkp://pool.sks-keyservers.net --send-keys C6EED57A
```  

` -keyserver ` 参数标识目标密钥服务地址, 使用` -send-keys `是希望分发密钥的密钥标识. 可能同步列出公约列表获取密钥标识. 一旦提交到密钥服务, 公钥将被同步到其它密钥服务.  

现在其他人能从密钥服务导入你的公钥到他们本地机器:  

```  
$ gpg2 --keyserver hkp://pool.sks-keyservers.net --recv-keys C6EED57A
```  




<span id = "使用构建工具签名"></span>  

## 使用构建工具签名  

现在已经创建并分发你的密钥, 能继续获取组件最为构件的一部分自动签名. 依赖于构建工具,这个设置都不一样. 查明更多关于这些下一步在指定的章节:  

- [Apache Maven](#http://central.sonatype.org/pages/apache-maven.html)  
- [Apache Ant](#http://central.sonatype.org/pages/apache-ant.html)  
- [Grade](#http://central.sonatype.org/pages/gradle.html)  
- [sbt](#http://central.sonatype.org/pages/sbt.html)  
- [Manual Staging Bundle Creation and Deployment](#http://central.sonatype.org/pages/manual-staging-bundle-creation-and-deployment.html)  


<span id = "处理过期的密钥"></span>  

## 处理过期的密钥  

当生成PGP密钥时, 需要指定密钥多长时间有效. 在那周期之后你可以编辑已存在密钥扩展它的有效时间.  

举个例子, 有一个密钥对有效期在2012-02-27:  

```  
$ gpg2 --list-keys
/Users/juven/.gnupg/pubring.gpg
-------------------------------
pub   2048R/A6BAB25C 2011-08-31 [expires: 2012-02-27]
uid                  Juven Xu (for testing) <test@juvenxu.com>
sub   2048R/DD289F64 2011-08-31 [expires: 2011-02-27]

```  

下面命令使用密钥标识作为参数能编辑密钥:  

```  
$ gpg2 --edit-key A6BAB25C
gpg (GnuPG/MacGPG2) 2.0.17; Copyright (C) 2011 Free Software Foundation, Inc.
This is free software: you are free to change and redistribute it.
There is NO WARRANTY, to the extent permitted by law.

Secret key is available.

pub  2048R/A6BAB25C  created: 2011-08-31  expires: 2012-02-27  usage: SC
                     trust: ultimate      validity: ultimate
sub  2048R/DD289F64  created: 2011-08-31  expires: 2011-02-27  usage: E
(1). Juven Xu (for testing) <test@juvenxu.com>
```  

这里仅有一个密钥, 因此选择1:  

```  
gpg> 1 
pub  2048R/A6BAB25C  created: 2011-08-31  expires: 2012-02-27  usage: SC
                     trust: ultimate      validity: ultimate
sub  2048R/DD289F64  created: 2011-08-31  expires: 2011-02-27  usage: E
(1)* Juven Xu (for testing) <test@juvenxu.com>

```  

将看到 ` * `在 (1)后面, 这意味着选中了这个密钥来编辑. 编辑密钥有效期, 键入下面的命令:  

```  
gpg> expire
Changing expiration time for the primary key.
Please specify how long the key should be valid.
         0 = key does not expire
      <n>  = key expires in n days
      <n>w = key expires in n weeks
      <n>m = key expires in n months
      <n>y = key expires in n years

```  

键入需要的, 例如10m(10个月), 然后确认. 编辑的最后一步是保存你完成的:  

```  
gpg> save
```  

现在可以看到密钥的有效时间更新了:  

```  
$ gpg2 --list-keys
pub   2048R/A6BAB25C 2011-08-31 [expires: 2012-06-26]
uid                  Juven Xu (for testing) &lt;test@juvenxu.com&gt;
sub   2048R/DD289F64 2011-08-31 [expires: 2011-02-27]
```  

最后, 再次分发公钥:  

```  
$ gpg2 --keyserver hkp://pool.sks-keyservers.net --send-keys A6BAB25C
```  



<span id = "删除子密钥"></span>  

## 删除子密钥  

一些PGP工具生成子密钥并且默认使用它们签名. 但是制作Maven工具识别签名, 必须使用主密钥签名构件.  

一些PGP工具默认生成子签名密钥并且使用它签名替代使用主密钥签名. 如果使用它签名构件和部署构件到中央库这是一个问题, 因为Maven和Nexus Repository Manager一样仅能依靠主密钥验证.  

修复这个问题需要删除子签名密钥,这样PGP将使用主密钥签名. 一个想法不论是否有子签名密钥, 使用独有的密钥标识运行下面的命令:  

```  
$ gpg2 --edit-key A6BAB25C
gpg (GnuPG/MacGPG2) 2.0.17; Copyright (C) 2011 Free Software Foundation, Inc.
This is free software: you are free to change and redistribute it.
There is NO WARRANTY, to the extent permitted by law.

Secret key is available.

pub  2048R/A6BAB25C  created: 2011-08-31  expires: 2012-06-26  usage: SC
                     trust: ultimate      validity: ultimate
sub  2048R/DD289F64  created: 2011-08-31  expired: 2011-09-30  usage: E
sub  2048R/8738EC86  created: 2011-12-19  expires: 2012-06-16  usage: S
(1). Juven Xu (for testing) &lt;test@juvenxu.com&gt;
```  

从上面的例子可以看到, 这个密钥有2个子密钥使用标识 ` DD289F64  ` 和 ` 8738EC86  `. 输出也显示了创建时间和过期时间. 这些密钥的用法是重要的. E为了加密, 因此子密钥 ` DD289F64  `仅被用于加密. S为了签名, 因此子密钥 ` 8738EC86  ` 仅被用于签名.  

如果主密钥有S子密钥, 它将用做签名. 否则, 它自己将处理签名工作. 因此, 在我们的例子, 希望删除子密钥 ` 8738EC86  `.  

首先选择希望删除的子密钥, 因为它的索引是2(索引从0开始), 运行命令:  

```  
gpg> key 2
pub  2048R/A6BAB25C  created: 2011-08-31  expires: 2012-06-26  usage: SC
                     trust: ultimate      validity: ultimate
sub  2048R/DD289F64  created: 2011-08-31  expired: 2011-09-30  usage: E
sub* 2048R/8738EC86  created: 2011-12-19  expires: 2012-06-16  usage: S
[ultimate] (1). Juven Xu (for testing) &lt;test@juvenxu.com&gt;
```  

从输出能够看到, 子密钥 ` 8738EC86  `被标记为 ` * `. 现在删除它:  

```  
gpg> delkey
Do you really want to delete this key? (y/N) y

pub  2048R/A6BAB25C  created: 2011-08-31  expires: 2012-06-26  usage: SC
                     trust: ultimate      validity: ultimate
sub  2048R/DD289F64  created: 2011-08-31  expired: 2011-09-30  usage: E
[ultimate] (1). Juven Xu (for testing) &lt;test@juvenxu.com&gt;
```  

小建议    

如果你已经分发公钥, 最好废除签名子密钥替代删除它. 尽管你能控制主密钥作为签名密钥. 废除子密钥, 使用 ` revkey ` 命令代替 ` delkey `.  

现在 ` 8738EC86  ` 不会被列出, 最后一步是保存和改变:  

```  
gpg> save
```  

就是这样, 现在你能铜鼓偶签名文件测试修改, 然后验证它. 输出应该包含一些类似的:  

```  
gpg: Signature made ************************* using *** key ID [YOUR-PRIMARY-KEY-ID]  
```  




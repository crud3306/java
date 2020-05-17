什么是 Maven
==============
Maven 是 Apache 组织下的一个跨平台的项目管理工具，它主要用来帮助实现项目的构建、测试、打包和部署。Maven 提供了标准的软件生命周期模型和构建模型，通过配置就能对项目进行全面的管理。它的跨平台性保证了在不同的操作系统上可以使用相同的命令来完成相应的任务。Maven 将构建的过程抽象成一个个的生命周期过程，在不同的阶段使用不同的已实现插件来完成相应的实际工作，这种设计方法极大的避免了设计和脚本编码的重复，极大的实现了复用。


Maven vs Ant
==============
Ant 也是 Apache 组织下的一个跨平台的项目构建工具，它是一个基于任务和依赖的构建系统，是过程式的。开发者需要显示的指定每一个任务，每个任务包含一组由 XML 编码的指令，必须在指令中明确告诉 Ant 源码在哪里，结果字节码存储在哪里，如何将这些字节码打包成 JAR 文件。Ant 没有生命周期，你必须定义任务和任务之间的依赖，还需要手工定义任务的执行序列和逻辑关系。这就无形中造成了大量的代码重复。

Maven 不仅是一个项目构建工具还是一个项目管理工具。它有约定的目录结构（表 1）和生命周期，项目构建的各阶段各任务都由插件实现，开发者只需遵照约定的目录结构创建项目，再配置文件中生命项目的基本元素，Maven 就会按照顺序完成整个构建过程。Maven 的这些特性在一定程度上大大减少了代码的重复。



maven安装
==============
下载一个压缩包，解压，配置即可。
maven解压后的目录结构
```
bin
boot
conf
lib
```
下载地址：http://maven.apache.org/download.cgi
选择一个版本的maven下载后，先解压到你想放的位置。

配置机器环境变量-系统变量
添加MAVEN_HOME，即你的maven包解压的目录
编辑PATH，追加%MAVEN_HOME%\bin


iead中使用maven
==============
idea集成maven插件
--------------
1 确认电脑中安装了idea  
2 确认电脑中安装了maven  
> mvn -v

打开idea首选项，左侧搜索maven，然后选中Maven，  
更改右侧的maven路径(maven home directory)，  
选择配置文件(settings flie)  



idea创建maven项目
--------------
- 使用骨架创建  
注意：确保当前机器可以连网  
new project，左侧选中Maven，右侧勾选上Create from archetype

- 使用骨架创建  
new project，左侧选中Maven，右侧不要勾选Create from archetype




maven作用
==============
依赖管理：maven工程对jar包的管理过程  
传统的java项目，jar包放在项目中；mavan开发的项目，jar包放在jar包仓库中，maven项目中只是放了jar包的坐标。  


一键构建  
我们的项目，往往要经历编译、测试、运行、打包、安装、部署等一第列过程。  
什么是构建？  
指项目从译、测试、运行、打包、安装、部署整个过程都交给maven进行管理。  
一键构建：指整个构建过程，使用maven一个命令可以轻松完成整个工作。  




maven仓库种类：
==============
一般有三种  
- 本地仓库 local  
本地仓库位置可通过maven配置文件:MAVEN_HOME/conf/settings.xml中查找  
```
<!-- localRepository
   | The path to the local repository maven will use to store artifacts.
   |
   | Default: ${user.home}/.m2/repository
  <localRepository>/path/to/local/repo</localRepository>
  -->
默认位置：Default: ${user.home}/.m2/repository
也可通过localRespository自行指定其它位置
<localRepository>D:\xxx\xxx</localRepository>
```

- 远程仓库（私服） b2b   
一般的公司，都会在内网中搭建自已的仓库(私服)，然后提前在私服中放好常用的jar包    
maven查找jar包时，本地仓库没有时会从这个私服中下载，如果私服中也没有测去中央仓库下载到私服，再到本地仓库  

- 中央仓库 center  
放置了几乎所有开源的jar包


maven查找jar包的方式  
个人开发时   
maven工程-通过jar包位置，先去本地仓库中查找jar包，本地仓库也没有则会去中央仓库下载  

企业开发时：企业一般会有自已的远程仓库(私服)  
maven工程-通过jar包位置，先去本地仓库中查找jar包，本地仓库没有则去远程仓库中下载，远程仓库也没有则会去中央仓库下载




maven标准目录结构
==============
通常我们一个项目的代码，主要包含以下几个部分  
核心代码部分  
配置文件部分  
测试代码部分  
测试配置文件  

- 普通的项目  
项目名  
	src  
	config  
	resource  

- maven项目标准目录结构   
src/main/java   核心代码部分  
src/main/resources  配置文件部分  
src/test/java   测试代码部分  
src/test/resources  测试配置文件  
src/main/webapp   页面资源，js，css，图片等；非webapp一般没有此目录  



maven命令
==============
清除项目编译信息:mvn clean   
清除项目编译信息，即：删除项目下的target目录。  
一般用于，拿到了他人的代码后，不需要他人的编译信息，即target目录下东东  


编译：mvn compile  
编译生成target目录，该目录下有一个classes目录，里面是编译好的java class文件(xxx.class)


测试：mvn test  
编译test，会在target目录下多一个test-classes目录，里面是编译好的java test class文件(xxx.class)  
其实mvn，不仅重编译了classes，同时也编译了test-classes


打包：mvn package  
项目打包，成jar或war，具体是哪种通pom.xml来配置  
打包的文件在target目录下  


安装：mvn install  
打包，并把打好的包装入本地仓库中  


发布：mvn deploy  


注意：执行mvn compile/test/package/install 命令后，如果target目录不存在，会自动创建

也可结合clean与其它指令一起用  
如：  
先clean再package  
mvn clean package  
或带上更多参数  
mvn clean package -DskipTests  
```
在使用mvn package进行编译、打包时，Maven会执行src/test/java中的JUnit测试用例，有时为了跳过测试，会使用参数-DskipTests和-Dmaven.test.skip=true，这两个参数的主要区别是：

-DskipTests， 不执行测试用例，但编译测试用例类生成相应的class文件至target/test-classes下。
-Dmaven.test.skip=true， 不执行测试用例，也不编译测试用例类。
```



maven概念模型
==============
主要分两部分
- 依赖管理
- 一键构建

依赖管理
---------------
####项目对象模型
pom.xml
- 项目自身信息
- 项目运行所依赖的jar包信息
- 项目运行环境信息，比如：jdk、tomcat信息


####依赖管理模型
公司组织的名称：groupId  
项目名：artifactId  
版本号：version  
包的依赖范围：scope  
```
<dependency>
    <groupId>org.apache.flink</groupId>
    <artifactId>flink-streaming-java_2.11</artifactId>
    <version>1.8.0</version>
    <scope>provided</scope>
</dependency>
```

包的依赖范围：scope  
默认scope为：compile  
```
依赖范围		对于编译classpath有效		对于测试classpath有效		对于运行classpath有效		例子
compile		Y						Y						Y						spring-core
test		-						Y						-						Junit
provided	Y						Y						-						servlet-api
runtime		-						Y						Y						JDBC驱动
system		Y						Y						-						本地的,Maven仓库外的类库
```


###一键构建
==============
默认生命周期：compile、test、package、install、delpoy





maven中央仓库中找jar包
==============
https://mvnrepository.com/  
在里面搜索想要的jar包，在搜索列表中，点击进去，然后点击你想要的版本。  
里面有dependency示例代码，拷贝即可  



maven工程运行环境修改
==============
即更改运行maven工程所需的jdk、tomcat等  
通过更改pom.xml中的build实现  
```xml
<build>
	<plugins>
		<plugin>
			<groupId>org.apache.tomcat.maven</groupId>
			<artifactId>tomcat7-maven-plugin</artifactId>
			<version>2.2</version>
			<configuration>
				<port>8888</port>
			</configuration>
		</plugin>
		<plugin>
			<groupId>org.apache.maven.plugins</groupId>
			<artifactId>maven-compiler-plugin</artifactId>
			<configuration>
				<target>1.8</target>
				<source>1.8</source>
				<encoding>UTF-8</encoding>
			</configuration>
		</plugin>
	<plugins>
</build>
```

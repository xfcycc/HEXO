---
title: Web项目部署到阿里云Taomcat的一系列配置
copyright: true
date: 2019-03-24 15:50:48
tags: [Java,Tomcat,Linux,IDEA]
categories: 疑难杂症
top:
---
### Web项目部署到阿里云的Tomcat

#### IDEA打包成war包

1. 点击【File】->【Project Structure】菜单。

2. 在【ProjectStructure】中选择左侧的【Artifacts】标签。

3. 点击左上角的绿色加号，选择【WebApplication:Archive】-> 【empty】。

4. 点击中间的绿色加号，选择【Directory Content】菜单，选中web文件根目录（与src目录同级）。

5. 新建文件夹【WEB-INF】->【classes】,再次点击中间的加号，在这个目录下，选择【Module Output】菜单，OK。

此时如图

![img](https://oss.caiguoyu.cn/pictures/olds/651335cfgy1g1dxyjtlkyj20n104nq31.jpg)

6. 选择输出的目录，保存设置。然后点击菜单【Build】-> 【Build Artifacts】,完成war包。

<!--more-->

>如果导致本地环境混乱，新建一个新的打包机制，选择【WebApplication:Exploded】->【From Modules】,IDEA本地运行项目选择这个打包方式，不支持war包。

#### 将war包发送到服务器的Tomcat目录

由于各种环境问题，我一般使用手动传输，使用Xshell。

1. 找到Tomcat项目路径，大同小异，我的是在`/www/server/apache-tomcat-default/webapps/`。

```shell
cd /www/server/apache-tomcat-default/webapps/
```

2. 利用sftp上传war包，Tomcat会自动解压。（Xshell自带sftp功能）

```shell
put C:\Users\caigu\Desktop\ROOT.war
```

3. 切换到项目路径，一般可以看到解压的项目文件夹，因为我将文件名改为了ROOT，因此会解压到默认目录，根据需求决定即可。

4. 项目里的配置文件大部分使用的`localhost`，为了不出现许多bug，建议还是ROOT好，如果需要多个项目访问，要改为`localhost:8080/xxx`。

5. 项目内的配置指向要改成服务器地址,端口号根据实际情况选择8443或8080,为了安全可以使用内网访问，如连接池配置文件。
如：

```xml
jdbc:mysql://内网ip:3306/
```

6. 完成后，重启Tomcat，即可访问。

```html
http://ip:8080
```

------

### 域名相关配置

#### 子域名重定向

以阿里云为例，在域名解析里面，选择【增加记录】。

```
记录类型：显性URL/隐性URL  （建议要使用https协议的使用显性）

主机记录：输入要重定向的子域名 如，tom.xxx.com

记录值：如， https://xxx.com:8443 或者 http://xxx.com:8080 (后面会说如何使用https)
```

>显性URL会暴露真实地址，根据需求决定

#### 使用https协议

之前说过如何使用NGINX搭载，大同小异。

1. 首先下载Tomcat专用的ssl证书，解压后分别为`xxx.pfx`和一个密码文件。

2. 找到你的Tomcat安装目录，新建cert目录，存放证书。

```shell
cd /www/server/apache-tomcat-default/
mkdir cert
cd cert
#sftp: put 本地目录/a.pfx
```

3. 找到配置文件，一般在安装目录下的conf文件夹。

```shell
vim server.xml
```

4. 使用以下命令搜索指定内容。

```shell
:
/8443
```

5. 你会看到以下内容。

```xml
<Connector port="8080" protocol="HTTP/1.1"
               connectionTimeout="20000"
               redirectPort="8443" /> <!-- 这里代表转发到8443，Tomcat的https端口-->
```
6. 在下面增加以下内容

```xml
<Connector port="8443"
    protocol="HTTP/1.1"
    SSLEnabled="true"
    scheme="https"
    secure="true"
    keystoreFile="cert/a.pfx"
    keystoreType="PKCS12"
    keystorePass="证书密码"
    clientAuth="false"
    SSLProtocol="TLSv1+TLSv1.1+TLSv1.2"
ciphers="TLS_RSA_WITH_AES_128_CBC_SHA,TLS_RSA_WITH_AES_256_CBC_SHA,TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA,TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256,TLS_RSA_WITH_AES_128_CBC_SHA256,TLS_RSA_WITH_AES_256_CBC_SHA256"/>

```

7. 重启Tomcat，尝试使用8443端口访问，也可以在阿里云域名解析中直接重定向。

>每一次下载证书都需要更新

-------

### Tomcat默认访问文件配置

直接访问Tomcat，会访问位于`webapps/ROOT`目录下的`index.jsp`文件，可以通过conf文件夹下的server.xml和web.xml文件进行修改。

#### 默认路径

在`server.xml`中，寻找以下语句，增加`Context path="" docBase="helloworld"  reloadable="true"`。

```xml
<Host name="47.101.214.198"  appBase="webapps"
            unpackWARs="true" autoDeploy="true">

        <!-- SingleSignOn valve, share authentication between web applications
             Documentation at: /docs/config/valve.html -->
        <!--
        <Valve className="org.apache.catalina.authenticator.SingleSignOn" />
        -->

        <!-- Access log processes all example.
             Documentation at: /docs/config/valve.html
             Note: The pattern used is equivalent to using pattern="common" -->
<Valve className="org.apache.catalina.valves.AccessLogValve" directory="logs"
       prefix="localhost_access_log" suffix=".txt"
       pattern="%h %l %u %t &quot;%r&quot; %s %b" />
<Context path="" docBase="helloworld"  reloadable="true"/>

```
此时，默认访问目录就会变成`helloworld`

#### 默认文件

在web.xml中，寻找以下语句，并加入`<welcome-file>login.html</welcome-file>`。

```xml
<welcome-file-list>
        <welcome-file>login.html</welcome-file>
        <welcome-file>index.html</welcome-file>
        <welcome-file>index.htm</welcome-file>
        <welcome-file>index.jsp</welcome-file>
    </welcome-file-list>

```
此后默认访问的文件便是`login.html`了。

> 必须只有一种，如果有多个可能会报错。
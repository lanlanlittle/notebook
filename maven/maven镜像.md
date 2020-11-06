阿里镜像：https://maven.aliyun.com/mvn/view

在maven的settings.xml文件里的mirrors节点，添加如下子节点：

<mirror>      

​	<id>nexus-aliyun</id>      

​	<mirrorOf>central</mirrorOf>        

​	<name>Nexus aliyun</name>      

​	<url>http://maven.aliyun.com/nexus/content/groups/public</url>   

</mirror> 
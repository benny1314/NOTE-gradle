## 1. 安装

### 1.1 下载 Gradle

[gradle3.3下载链接](https://services.gradle.org/distributions/gradle-3.3-bin.zip)

### 1.2 配置环境变量

```bash
vi ~/.bash_profile

export GRADLE_HOME=/usr/local/gradle/gradle3.3  
export PATH=$PATH:$GRADLE_HOME/bin

source ~/.bash_profile
```

### 1.3 验证安装

```
[root@benny ~]# gradle -v                                                                                                                             

------------------------------------------------------------                                                                                                 
Gradle 3.3                                                                                                                                                   
------------------------------------------------------------                                                                                                 
                                                                                                                                                             
Build time:   2017-01-03 15:31:04 UTC                                                                                                                        
Revision:     075893a3d0798c0c1f322899b41ceca82e4e134b                                                                                                       

Groovy:       2.4.7                                                                                                                                          
Ant:          Apache Ant(TM) version 1.9.6 compiled on June 29 2015                                                                                          
JVM:          1.8.0_121 (Oracle Corporation 25.121-b13)                                                                                                      
OS:           Linux 3.10.0-327.22.2.el7.x86_64 amd64  

```


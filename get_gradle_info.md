## 项目列表

执行 `gradle projects` 命令会为你列出子项目名称列表.

### 收集项目信息

#### 1.使用 `gradle projects` **需要进入到当前项目所在的目录**

`gradle -q projects` 命令的输出结果

```
> cd ~/edu-parent
> gradle -q projects
------------------------------------------------------------
Root project
------------------------------------------------------------

Root project 'edu-parent'
+--- Project ':edu-common'
+--- Project ':edu-common-config'
+--- Project ':edu-common-core'
+--- Project ':edu-common-web'
+--- Project ':edu-facade-user'
+--- Project ':edu-service-user'
\--- Project ':edu-web-main'

To see a list of the tasks of a project, run gradle <project-path>:tasks
For example, try running gradle :edu-common:tasks

BUILD SUCCESSFUL

Total time: 0.912 secs

```

这份报告展示了每个项目的描述信息. 当然你可以在项目中用 `description` 属性来指定这些描述信息.

#### 使用 `gradle -p 项目所在文件夹 project` 则可以不需要进入项目所在目录

`gradle -p ~/edu-parent/ projects` 命令的输出结果

```
MacBook-Pro:edu-parent benny$ gradle -p ~/edu-parent/  projects
:projects

------------------------------------------------------------
Root project
------------------------------------------------------------

Root project 'edu-parent'
+--- Project ':edu-common'
+--- Project ':edu-common-config'
+--- Project ':edu-common-core'
+--- Project ':edu-common-web'
+--- Project ':edu-facade-user'
+--- Project ':edu-service-user'
\--- Project ':edu-web-main'

To see a list of the tasks of a project, run gradle <project-path>:tasks
For example, try running gradle :edu-common:tasks

BUILD SUCCESSFUL

Total time: 0.912 secs

```
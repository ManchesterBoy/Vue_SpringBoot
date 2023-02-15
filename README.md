
# Vue-SpringBoot-后台管理系统
这是一个前后端分离项目，前端框架为VUE，后端框架为SpringBoot，集成的一个后台管理系统项目
=======
# Vue-Springboot-
Vue+Springboot 管理系统

###### 配置参考

后端端口号为:http://localhost:9090
前端端口号为:http://localhost:8080

###### 此项目为前后端分离项目

如需要修改后端端口号需在application.yml中的server: port: 自行修改
如若修改了后端端口号，请在对应前端页面中将9090改为你所修改的端口号(Person、User、Menu、File)

同时若前端端口不为8080，则需在config包的CorsConfig中的跨域方案进行调整

数据库密码修改在 application.yml 中，数据库名称为leslie，数据都在leslie.sql中

记得从Maven中导入所需的项目依赖

前端运行需通过终端进入到vue的文件中使用命令:npm run serve （需要有node.js情况下才能启动）
后端运行通过启动 SbootApplication 即可

登录页面为http://localhost:8080/login
帐号:admin    密码:admin

### PS
**初次登录会直接进入到后台管理系统，但此时由于TOKEN的时长限制，并无法查询任何内容，需退出重新登录**

**若前端启动时遇到 《'vue-cli-service' 不是内部或外部命令，也不是可运行的程序》时，请从终端进入到vue的目录输入以下命令安装所需资源 《npm i -D @vue/cli-service》**
### ps：记得是以管理员身份进入cmd模式，目录跳转命令 cd /d 你所在的路径**

**权限、token、登陆、顶级域名**

 

**权限控制**

**控制台**

**定义及编写权限控制方法**

目录：k8s-console-front/src/directive\permission\permission.js

![IMG_256](file:///C:/Users/KevinLiu/AppData/Local/Temp/msohtmlclip1/01/clip_image002.jpg)

目录：k8s-console-front/src/directive\permission\permissionHelper.js

![IMG_257](file:///C:/Users/KevinLiu/AppData/Local/Temp/msohtmlclip1/01/clip_image004.jpg)![IMG_258](file:///C:/Users/KevinLiu/AppData/Local/Temp/msohtmlclip1/01/clip_image006.jpg)

目录：k8s-console-front/src/directive\permission\index.js

![IMG_259](file:///C:/Users/KevinLiu/AppData/Local/Temp/msohtmlclip1/01/clip_image008.jpg)

目录：k8s-console-front/src/main.js

![IMG_260](file:///C:/Users/KevinLiu/AppData/Local/Temp/msohtmlclip1/01/clip_image010.jpg)

**控制菜单**

目录：k8s-console-front/src/views/layout/components/Sidebar/SidebarItem.vue

![IMG_261](file:///C:/Users/KevinLiu/AppData/Local/Temp/msohtmlclip1/01/clip_image012.jpg)

![IMG_262](file:///C:/Users/KevinLiu/AppData/Local/Temp/msohtmlclip1/01/clip_image014.jpg)

![IMG_263](file:///C:/Users/KevinLiu/AppData/Local/Temp/msohtmlclip1/01/clip_image016.jpg)

![IMG_264](file:///C:/Users/KevinLiu/AppData/Local/Temp/msohtmlclip1/01/clip_image018.jpg)

**权限控制菜单是否显示**

目录：k8s-console-front/src/router/index.js

![IMG_265](file:///C:/Users/KevinLiu/AppData/Local/Temp/msohtmlclip1/01/clip_image020.jpg)

![IMG_266](file:///C:/Users/KevinLiu/AppData/Local/Temp/msohtmlclip1/01/clip_image022.jpg)

![IMG_267](file:///C:/Users/KevinLiu/AppData/Local/Temp/msohtmlclip1/01/clip_image024.jpg)

![IMG_268](file:///C:/Users/KevinLiu/AppData/Local/Temp/msohtmlclip1/01/clip_image026.jpg)

![IMG_269](file:///C:/Users/KevinLiu/AppData/Local/Temp/msohtmlclip1/01/clip_image028.jpg)

![IMG_270](file:///C:/Users/KevinLiu/AppData/Local/Temp/msohtmlclip1/01/clip_image030.jpg)

 

**无权限页面**

权限验证,当访问地址无权限访问则跳转到无权限访问页面

目录：k8s-console-front/src/permission.js

![IMG_271](file:///C:/Users/KevinLiu/AppData/Local/Temp/msohtmlclip1/01/clip_image032.jpg)

**将权限数据通过iframe传给另一个项目使用**

目录：k8s-console-front/src/utils/accessControl.js

![IMG_272](file:///C:/Users/KevinLiu/AppData/Local/Temp/msohtmlclip1/01/clip_image034.jpg)

 

**获取地址栏中的权限信息**

目录：docker_manage_front/src/utils/urlParam.js

![IMG_275](file:///C:/Users/KevinLiu/AppData/Local/Temp/msohtmlclip1/01/clip_image036.jpg)

目录：docker_manage_front/src/directive/permission/permission.js

![IMG_276](file:///C:/Users/KevinLiu/AppData/Local/Temp/msohtmlclip1/01/clip_image038.jpg)

目录：docker_manage_front/src/directive/permission/index.js

![IMG_277](file:///C:/Users/KevinLiu/AppData/Local/Temp/msohtmlclip1/01/clip_image040.jpg)

目录：docker_manage_front/src/main.js

![IMG_278](file:///C:/Users/KevinLiu/AppData/Local/Temp/msohtmlclip1/01/clip_image042.jpg)

**控制按钮**

![IMG_279](file:///C:/Users/KevinLiu/AppData/Local/Temp/msohtmlclip1/01/clip_image044.jpg)

 

**token****获取、请求携带及失效**

**控制台**

**获取token**

逻辑：当登陆进入页面前先跳转到一个加载页面(k8s-console-front/src/views/load.vue)，加载页面处理如下

1、获取集群信息，存储到sessionStorage中

2、判断地址栏中是否存在token（如果存在则为setup跳转进入的控制台）

3、判断是否存在code，

3.1、存在code，解析code，解析成功获取并存储token信息并调用获取权限接口，否则跳转登陆页面

3.2、不存在code，判断是否存在token，如存在token（setup跳转进入的控制台）调用获取权限接口并跳转首页

3.3、不存在code并且不存在token，跳转登陆页面

 

**请求携带token**

目录：k8s-console-front/src/utils/request.js

![IMG_280](file:///C:/Users/KevinLiu/AppData/Local/Temp/msohtmlclip1/01/clip_image046.jpg)

![IMG_281](file:///C:/Users/KevinLiu/AppData/Local/Temp/msohtmlclip1/01/clip_image048.jpg)

**token****失效**

目录：k8s-console-front/src/utils/request.js

![IMG_282](file:///C:/Users/KevinLiu/AppData/Local/Temp/msohtmlclip1/01/clip_image050.jpg)

**跳转登陆页面**

window.location.href="https://auth."+this.clusterInfo.appExtensiveDomain+"/logout?id_token_hint=&state=&post_logout_redirect_uri=http://console."+this.clusterInfo.appExtensiveDomain;

**跳转登陆页面有四处：**

用户点击“退出登陆”按钮(k8s-console-front/src/views/layout/components/Headers.vue)

获取code失败(k8s-console-front/src/views/load.vue)

token失效(k8s-console-front/src/utils/request.js)

无权限页面，点击“回到登陆页面”按钮(k8s-console-front/src/views/noPermission.vue)

**删除顶级域名**

document.cookie = "dexUserName=;domain=."+this.clusterInfo.appExtensiveDomain+"; max-age=-1";

**删除顶级域名有三处：**

用户点击“退出登陆”按钮(k8s-console-front/src/views/layout/components/Headers.vue)

token失效(k8s-console-front/src/utils/request.js)

无权限页面，点击“回到登陆页面”按钮(k8s-console-front/src/views/noPermission.vue)

 

 

 

 

 

 

 

**nks****、离线版本修改的地方**

注意：nks版本不包含“租户管理服务端”项目

**setup****项目（nks）**

1、关于

![IMG_256](file:///C:/Users/KevinLiu/AppData/Local/Temp/msohtmlclip1/01/clip_image052.jpg)

2、图标

![img](file:///C:/Users/KevinLiu/AppData/Local/Temp/msohtmlclip1/01/clip_image053.png)

3、认证配置默认改完UAA显示

 

4、向导开始页面

![IMG_258](file:///C:/Users/KevinLiu/AppData/Local/Temp/msohtmlclip1/01/clip_image055.jpg)5、导入已有环境-设置应用域名，有"PKS密码" ![IMG_259](file:///C:/Users/KevinLiu/AppData/Local/Temp/msohtmlclip1/01/clip_image057.jpg)

6、导入已有环境-附加组件，有“使用私有仓库镜像”选项并且默认为勾选状态

![IMG_260](file:///C:/Users/KevinLiu/AppData/Local/Temp/msohtmlclip1/01/clip_image059.jpg)

7、导入已有环境-导入，有“上传离线镜像” ![IMG_261](file:///C:/Users/KevinLiu/AppData/Local/Temp/msohtmlclip1/01/clip_image061.jpg)

**setup****（离线）**

1、license验证页面，屏蔽掉“租户注册”

![IMG_262](file:///C:/Users/KevinLiu/AppData/Local/Temp/msohtmlclip1/01/clip_image063.jpg)

2、向导开始页面，只有部署没有导入

![IMG_263](file:///C:/Users/KevinLiu/AppData/Local/Temp/msohtmlclip1/01/clip_image065.jpg)

3、附加组件，版本+离线版

![IMG_264](file:///C:/Users/KevinLiu/AppData/Local/Temp/msohtmlclip1/01/clip_image067.jpg)

 

4、部署

![img](file:///C:/Users/KevinLiu/AppData/Local/Temp/msohtmlclip1/01/clip_image068.png)

5、管理页面，去掉帮助文档

![IMG_266](file:///C:/Users/KevinLiu/AppData/Local/Temp/msohtmlclip1/01/clip_image070.jpg)

 

**应用商店（离线）**

![IMG_267](file:///C:/Users/KevinLiu/AppData/Local/Temp/msohtmlclip1/01/clip_image072.jpg)

 

![IMG_268](file:///C:/Users/KevinLiu/AppData/Local/Temp/msohtmlclip1/01/clip_image074.jpg)

![IMG_269](file:///C:/Users/KevinLiu/AppData/Local/Temp/msohtmlclip1/01/clip_image076.jpg)

所有图片地址上都拼接泛域名

![IMG_270](file:///C:/Users/KevinLiu/AppData/Local/Temp/msohtmlclip1/01/clip_image078.jpg)

![IMG_271](file:///C:/Users/KevinLiu/AppData/Local/Temp/msohtmlclip1/01/clip_image080.jpg)

![IMG_272](file:///C:/Users/KevinLiu/AppData/Local/Temp/msohtmlclip1/01/clip_image082.jpg)

控制台环境地址修改

![IMG_275](file:///C:/Users/KevinLiu/AppData/Local/Temp/msohtmlclip1/01/clip_image084.jpg)

![IMG_276](file:///C:/Users/KevinLiu/AppData/Local/Temp/msohtmlclip1/01/clip_image086.jpg)

![IMG_277](file:///C:/Users/KevinLiu/AppData/Local/Temp/msohtmlclip1/01/clip_image088.jpg)

![IMG_278](file:///C:/Users/KevinLiu/AppData/Local/Temp/msohtmlclip1/01/clip_image090.jpg)

![IMG_279](file:///C:/Users/KevinLiu/AppData/Local/Temp/msohtmlclip1/01/clip_image092.jpg)

![IMG_280](file:///C:/Users/KevinLiu/AppData/Local/Temp/msohtmlclip1/01/clip_image094.jpg)

![IMG_281](file:///C:/Users/KevinLiu/AppData/Local/Temp/msohtmlclip1/01/clip_image096.jpg)

![IMG_282](file:///C:/Users/KevinLiu/AppData/Local/Temp/msohtmlclip1/01/clip_image098.jpg)

![IMG_283](file:///C:/Users/KevinLiu/AppData/Local/Temp/msohtmlclip1/01/clip_image100.jpg)

![IMG_284](file:///C:/Users/KevinLiu/AppData/Local/Temp/msohtmlclip1/01/clip_image102.jpg)

 

Devops流水线图形化创建串并行任务的实现及上传问题

 

![img](file:///C:/Users/KevinLiu/AppData/Local/Temp/msohtmlclip1/01/clip_image104.jpg)

 

![img](file:///C:/Users/KevinLiu/AppData/Local/Temp/msohtmlclip1/01/clip_image106.jpg)

 

监控告警自定义图表的实现

![img](file:///C:/Users/KevinLiu/AppData/Local/Temp/msohtmlclip1/01/clip_image108.jpg)

 

日志管理产品切换控制

![img](file:///C:/Users/KevinLiu/AppData/Local/Temp/msohtmlclip1/01/clip_image110.jpg)

 

镜像管理退出登录的操作

 

![img](file:///C:/Users/KevinLiu/AppData/Local/Temp/msohtmlclip1/01/clip_image112.jpg)
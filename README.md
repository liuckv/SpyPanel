# 简介
spy panel是基于[Pear Admin](https://gitee.com/pear-admin/)框架开发的一款支持本地虚拟化部署的综合性面板。支持脚本定时、监听运行、消息转发、代码拉取等等功能，具有用户分权机制，可根据不同权限展示不同的功能。依然保留青龙的对接。更多功能大家自己摸索吧。

亮点：

- 支持多用户分权控制；

- 任务运行分为**定时运行**和**监控运行**，通过不同的设置页面进行管理；

- 同一个脚本同时运行多个，且可控，目前限定死3个，后续开放自定义；

- web shell 直接运行命令，方便后台维护；


# 前期准备

加入授权群：[https://t.me/spy_auth](https://t.me/spy_auth)，扯犊子群：[https://t.me/spy_happy](https://t.me/spy_happy)

# 安装方法

- 建立持久化目录：mkdir spy_panel_data

- 进入持久化目录：cd spy_panel_data

- 拉取镜像并创建容器：docker run -dit --restart=always --name=spy_panel --log-opt max-size=100m --log-opt max-file=3 -p 9081:9081 -p 9082:9082 -p 9083:9083 -v "$(pwd)"/Script:/spy/Script -v "$(pwd)"/history:/spy/history -v "$(pwd)"/config:/spy/config -v "$(pwd)"/run_config:/spy/run_config -v "$(pwd)"/logs:/spy/logs xieshang1111/spy_panel:latest

- 访问：http://ip:9081 ，ip为宿主机的IP，默认账密：admin/123456，**请及时修改账密！！**

![image.png](https://cdn.nlark.com/yuque/0/2024/png/251249/1706948009482-94b6f495-23bd-4c13-8228-f69029002ec2.png#averageHue=%23141729&clientId=u287a8cd1-faf1-4&from=paste&height=407&id=u5749a55a&originHeight=509&originWidth=634&originalType=binary&ratio=1.25&rotation=0&showTitle=false&size=76610&status=done&style=none&taskId=u22fec42a-fd61-4b3b-b60c-f354f2ab133&title=&width=507.2)

![image.png](https://cdn.nlark.com/yuque/0/2024/png/251249/1706948110814-5090a584-758b-4f19-822d-e93b40a3fa37.png#averageHue=%23f5f3f1&clientId=u287a8cd1-faf1-4&from=paste&height=577&id=ubf0fc3ff&originHeight=721&originWidth=1200&originalType=binary&ratio=1.25&rotation=0&showTitle=false&size=44291&status=done&style=none&taskId=u22744b96-d421-4050-a98d-94fda503064&title=&width=960)

![image.png](https://cdn.nlark.com/yuque/0/2024/png/251249/1706948144524-97f5183b-f5dc-4494-8d09-338561cc281b.png#averageHue=%23fafafa&clientId=u287a8cd1-faf1-4&from=paste&height=1146&id=u33676e04&originHeight=1432&originWidth=2560&originalType=binary&ratio=1.25&rotation=0&showTitle=false&size=75346&status=done&style=none&taskId=ue9b4a770-58a6-4efe-a346-6189a14e778&title=&width=2048)

## 说明

端口开放3个：9081--面板界面  9082/9083--为以后的代理池等功能预留

默认账密：admin/123456

nolan pro的接入：用法与青龙相同

目录说明：

Script--拉取的代码存放处

history--存放监控、运行历史

config--配置、定时任务、环境变量、TG授权文件等

logs--运行日志

run_config--配置文件等


# 使用教程

## TG相关

### TG登录
点击右侧菜单-->基础设置-->TG登录

![chrome_VOgjiuivfu.png](https://cdn.nlark.com/yuque/0/2024/png/251249/1706948253816-4f799e3b-4ba3-4554-a7c2-902bd2597e7d.png#averageHue=%23e9d6a3&clientId=u287a8cd1-faf1-4&from=paste&height=388&id=uc97f34d7&originHeight=485&originWidth=798&originalType=binary&ratio=1.25&rotation=0&showTitle=false&size=34253&status=done&style=none&taskId=u2876c7a4-f0a1-4cc7-af88-862869b263b&title=&width=638.4)

选择“人形”，后续将开放机器人模式

![chrome_Vw7ClCkSxn.png](https://cdn.nlark.com/yuque/0/2024/png/251249/1706948424273-64f79669-059f-467f-b7b1-665dc711cb8f.png#averageHue=%23fdfcfb&clientId=u287a8cd1-faf1-4&from=paste&height=620&id=u2c304c6a&originHeight=775&originWidth=1545&originalType=binary&ratio=1.25&rotation=0&showTitle=false&size=69961&status=done&style=none&taskId=u667cdbd5-8307-496c-8357-f1affd7dff9&title=&width=1236)

根据你的网络状态进行填写：

1、国外机：可以直接访问TG，则留空；

2、国内机：若设置了全局代理，可以尝试不填写代理，如果无法获取到二维码或验证码，则根据下面的代理填写规则按照你的代理类型进行填写，**推荐socks5和mtproxy，http/https在测试过程中感觉不是很稳定**。

若选择二维码登录，则会跳出二维码，请使用手机APP进行扫描：Settings->Devices->Link Desktop Device（按钮），扫描完成后，点击“已扫描”按钮。

![chrome_kISQ7BZQTf.png](https://cdn.nlark.com/yuque/0/2024/png/251249/1706948692183-410f6e18-be52-4e4d-a54d-fc9fe9b6248b.png#averageHue=%23edebea&clientId=u287a8cd1-faf1-4&from=paste&height=471&id=u9cd08b00&originHeight=756&originWidth=571&originalType=binary&ratio=1.25&rotation=0&showTitle=false&size=30168&status=done&style=none&taskId=u78971004-9f11-4f97-a972-2e90ef42944&title=&width=355.8000183105469)![image.png](https://cdn.nlark.com/yuque/0/2024/png/251249/1706948867583-8a8f4f7b-129a-46e7-a0e3-046f9615671a.png#averageHue=%23c5d3be&clientId=u287a8cd1-faf1-4&from=paste&height=299&id=u8e9203d9&originHeight=583&originWidth=702&originalType=binary&ratio=1.25&rotation=0&showTitle=false&size=97521&status=done&style=none&taskId=u38da039a-acf2-4abb-a6f9-32191645e92&title=&width=359.6000061035156)


若设置了二验密码，请在后续的页面中填写密码。

![image.png](https://cdn.nlark.com/yuque/0/2024/png/251249/1706948946798-351fdc82-ba75-4259-a001-42db6c372a9a.png#averageHue=%23fef5f3&clientId=u287a8cd1-faf1-4&from=paste&height=275&id=ua40cb73c&originHeight=344&originWidth=483&originalType=binary&ratio=1.25&rotation=0&showTitle=false&size=11878&status=done&style=none&taskId=u420a13d9-bda4-46f8-aca5-fc958d00ef6&title=&width=386.4)


登录成功，刷新首页也将显示状态。

![image.png](https://cdn.nlark.com/yuque/0/2024/png/251249/1706948991233-9365d92d-158e-4aeb-bb4c-96d4555cb028.png#averageHue=%23fefdfd&clientId=u287a8cd1-faf1-4&from=paste&height=252&id=uab6c75f4&originHeight=315&originWidth=457&originalType=binary&ratio=1.25&rotation=0&showTitle=false&size=11862&status=done&style=none&taskId=ufbbdebed-a644-4a5f-8033-8429932644a&title=&width=365.6)![image.png](https://cdn.nlark.com/yuque/0/2024/png/251249/1706949021997-916710df-7221-43a4-a8ec-cd8e1aca928f.png#averageHue=%23fcfcfb&clientId=u287a8cd1-faf1-4&from=paste&height=132&id=u4b0066bc&originHeight=165&originWidth=413&originalType=binary&ratio=1.25&rotation=0&showTitle=false&size=8744&status=done&style=none&taskId=ucbd9a72a-398b-4bda-a79f-1550903aa86&title=&width=330.4)


## 任务管理
任务管理分为**定时任务**和**监控任务**。


vue安装及配置
首先下载node.js要求版本在8.9以上        官网：https://nodejs.org/zh-cn/

下载完可检查在windows任务命令行里输入node -v

使用淘宝NPM镜像源下载比较快    命令：npm install -g cnpm --registry=https://registry.npm.taobao.org

安装vue-cli（全局安装vue-cli）    命令：cnpm install -g @vue/cli

检查环境是否安装上：vue -V

* 创建vue项目：

- 使用可视化界面创建界面:vue ui

- 在命令行里输入命令：vue init webpack vue_demo（创建名字为‘vue_demo’的文件夹）

- 然后进入此文件夹：cd vue_demo

- 然后手动下载：cnpm install

- 最后运行程序：npm run dev        

- 运行之后会导出网址：http://localhost:8080

- 在网页上输入上面的网址即可


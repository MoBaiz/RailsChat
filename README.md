# RailsChat 

RailsChat是一款由Rails开发的实时Web聊天室，在[Render_sync](https://github.com/chrismccord/render_sync)的基础上完成，有需要即时通讯的应用可以考虑这个Example

### [RailsChat详细教程-传送门](http://blog.csdn.net/ppp8300885/article/details/59109778)

## 目前功能

* 即时通讯
* 增添好友
* 创建聊天
* 拉人，删人
* 转移房屋权限

## Todo

1. UI界面修改（类似WeChat）
2. 未读信息的提醒（包括声音）
3. 加入更多的ajax提高用户体验

## Usage 

1. Fork项目

  ```
  git clone https://github.com/your_user_name/RailsChat
  cd RailsChat
  bundle install
  rails server
  ```

2. 然后再打开另外一个终端，运行以下命令启动另外一个server来监听聊天室的用户并实时推送最新的消息：

  ```
  rackup sync.ru -E production
  ```

### Note：如果要部署到云上或者本地局域网内，需要修改`config/sync.yml`文件

以本地局域网为例：

1. 若本机的ip地址为192.168.0.14（使用`ifconfig`查看），那么需要将config/sync.yml中的localhost全改为此ip地址，例如
 
 ```
  development:
    server: "http://192.168.0.14:9292/faye"
    adapter_javascript_url: "http://192.168.0.14:9292/faye/faye.js"
    auth_token:  "97c42058e1466902d5adfac0f83e84c1794b9c3390e3b0824be9db8344eae82b"
    adapter: "Faye"
    async: true
    
  test:
    ...
  production:
    ...
  ```

2. 然后运行rake tmp:clear来清除缓存，不然修改不会生效（运行前先将所有相关的运行停止：如rails s,rackup sync.ru等）

3. 再次运行rails服务器和监听程序，并指定监听程序运行的ip地址

  ```
  rails s
  rackup sync.ru -E production --host 192.168.0.14 
  ```



## Debug

1. 当遇到消息并没有实时推送的情况时，先F12查看浏览器的Js文件加载情况，若faye.js加载成功则一般不会出现问题

2. 以上加载完成但是仍然没有推送的时候，请查看Rails服务器的log文件

3. 需要在两个浏览器中登录不同的账号来检验聊天室功能


## 截图

<img src="/lib/Snip20170301_2.png">

<img src="/lib/Snip20170301_3.png">

<img src="/lib/Snip20170301_4.png">

<img src="/lib/Snip20170301_5.png">



**如果觉得好，请给项目点颗星来支持吧～～** 

有什么好的建议，请在issue中提出，欢迎contributors！


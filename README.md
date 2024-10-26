ymbotpy
=======

**ymbotpy** 是基于 机器人开放平台API <https://bot.q.qq.com/wiki/develop/api/> 实现的机器人框架，目的提供一个易使用、开发效率高的开发框架，此版本为webhook版本，非Tencent官方SDK。


特性
----

- 兼容 Python 3.7+
- 简单、易用、快速集成，过滤垃圾消息以及消息鉴权
- 可无缝替换websocket版本qq-botpy

安装
-----

``` bash
pip install ymbotpy
```
``注意: 由于通信方式的变化, 不再需要在本地注册监听事件，只需要编写具体的事件代码即可，事件开关在平台控制``

快速上手
--------
1.  频道内@自动回复
    ``` python
    import ymbotpy
    from ymbotpy.message import Message

    class MyClient(ymbotpy.Client):
        async def on_at_message_create(self, message: Message):
            """频道内@"""
            await message.reply(content=f"机器人{self.robot.name}收到你的@消息了: {message.content}")

    if __name__ == "__main__":
        BOT_APPID = 'botid'
        BOT_SECRET = 'secert'
        client = MyClient()
        client.run(appid=BOT_APPID,secret=BOT_SECRET,port=8080,system_log=True)
    ```

    
2.  在开发平台应配置的回调地址为：example.com/qbot/webhook，您可以通过以下方式来修改回调URL自定义webhook的url
    ``` python
    client.run(appid=BOT_APPID,secret=BOT_SECRET,port=8080,system_log=True,hook_route='/your_url')
    ```

3.  配置SSL以直接实现域名直接访问

    ```python
    client.run(appid=BOT_APPID,secret=BOT_SECRET,port=443,system_log=True,
        ssl_keyfile='ssl/private.key',ssl_certfile='ssl/public.crt')
    ```

文档
----

有关此 SDK 更多用法，请查阅qq-botpy <https://github.com/tencent-connect/botpy>

### 欢迎访问镜芯科技
1.  天狼星框架：[https://www.siriusbot.cn/](天狼星框架)
2.  镜芯API：[https://api2.wer.plus/](镜芯API)
3.  林枫云_站长首选云服务器：[https://www.dkdun.cn/](林枫云)
---
id: index
slug: /api/drivers/
---

# NoneBot.drivers 模块

## 后端驱动适配基类

各驱动请继承以下基类

## _class_ `Driver`

基类：`abc.ABC`

Driver 基类。

### `_adapters`

- **类型**

  `Dict[str, Adapter]`

- **说明**

  已注册的适配器列表

### `_bot_connection_hook`

- **类型**

  `Set[T_BotConnectionHook]`

- **说明**

  Bot 连接建立时执行的函数

### `_bot_disconnection_hook`

- **类型**

  `Set[T_BotDisconnectionHook]`

- **说明**

  Bot 连接断开时执行的函数

### `__init__(env, config)`

- **参数**

  - `env: Env`: 包含环境信息的 Env 对象

  - `config: Config`: 包含配置信息的 Config 对象

### `env`

- **类型**

  `str`

- **说明**

  环境名称

### `config`

- **类型**

  `Config`

- **说明**

  配置对象

### `_clients`

- **类型**

  `Dict[str, Bot]`

- **说明**

  已连接的 Bot

### _property_ `bots`

- **类型**

  `Dict[str, Bot]`

- **说明**

  获取当前所有已连接的 Bot

### `register_adapter(adapter, **kwargs)`

- **说明**

  注册一个协议适配器

- **参数**

  - `name: str`: 适配器名称，用于在连接时进行识别

  - `adapter: Type[Bot]`: 适配器 Class

  - `**kwargs`: 其他传递给适配器的参数

### _abstract property_ `type`

驱动类型名称

### _abstract property_ `logger`

驱动专属 logger 日志记录器

### _abstract_ `run(*args, **kwargs)`

- **说明**

  启动驱动框架

- **参数**

  - `*args`

  - `**kwargs`

### _abstract_ `on_startup(func)`

注册一个在驱动启动时运行的函数

### _abstract_ `on_shutdown(func)`

注册一个在驱动停止时运行的函数

### `on_bot_connect(func)`

- **说明**

  装饰一个函数使他在 bot 通过 WebSocket 连接成功时执行。

- **函数参数**

  - `bot: Bot`: 当前连接上的 Bot 对象

### `on_bot_disconnect(func)`

- **说明**

  装饰一个函数使他在 bot 通过 WebSocket 连接断开时执行。

- **函数参数**

  - `bot: Bot`: 当前连接上的 Bot 对象

### `_bot_connect(bot)`

在 WebSocket 连接成功后，调用该函数来注册 bot 对象

### `_bot_disconnect(bot)`

在 WebSocket 连接断开后，调用该函数来注销 bot 对象

## _class_ `ForwardDriver`

基类：`nonebot.drivers.Driver`, `nonebot.drivers.ForwardMixin`

Forward Driver 基类。将客户端框架封装，以满足适配器使用。

## _class_ `ReverseDriver`

基类：`nonebot.drivers.Driver`

Reverse Driver 基类。将后端框架封装，以满足适配器使用。

### _abstract property_ `server_app`

驱动 APP 对象

### _abstract property_ `asgi`

驱动 ASGI 对象

## _class_ `HTTPServerSetup`

基类：`object`

## _class_ `WebSocketServerSetup`

基类：`object`

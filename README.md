# WebIM ie8

## 上传失败

-> IE8下的上传功能 需要必须以web服务的方式访问，请不要直接打开以 file:// 协议的方式访问
-> 看网络 crossdomain.xml 文件是否能正常访问，如果是400或500之类的，就是服务器配置问题

## 提示 “拒绝访问”

- XDomainRequest
	- 安全协议源必须匹配请求的URL。（http到http, https到https）。 如果不匹配，请求会报“拒绝访问”错误
	- 被请求的URL服务器需要支持CORS，必须有 `Access-Control-Allow-Origin: *` 的头

## 同一时间出现多个长轮询的连接

-> ie8下 strophe自带心跳机制，不需要额外设置心跳机制

## 重写send方法时，oldsend 处报错

IE下XDomainRequest的send方法是object而不是function无法重写

-> 单独赋值 `xhr.readyState = 2`

## strict 模式下不允许分配到只读属性

window.XDomainRequest && (xhr.readyState = 2)

-> 去掉 `use "strict"`

## 图片上传失败

-> 上传接口总是失败，需要确认服务端是否设置 `crossdomain.xml`
-> ie下通过flash上传，之前flash组件是嵌入到demo当中的，所以需要单独摘出
-> flash的是选择图片上传后自动发送消息，不需要单独点击发送消息
-> uploadShim 逻辑并不完善，需要自己完善，里面有引用 Demo. 的部分都需要更换

## 创建群组流程修改

-> 先创建群组 -> 接收创建成功回调 -> 设置群组信息 -> 完成, 拉去群组信息

## ie下不支持贴图功能

-> 依赖于 URL 属性，理论上ie11才支持

## 各种错误

-> 确保自己是的控制台文档模式在 ie8 下面

## sdk下的status.js 存放各种错误信息简介
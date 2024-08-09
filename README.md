# fakeMSI

1. fakeMSI对外提供统一的桥能力以支持上层业务的调用  能够有效地提高桥的标准化程度 提高桥的复用率
   对所有相关的api提供统一的管理 暂时只支持方法型api 后续可以考虑增加对于事件型api的支持

2. APIPortal是整个框架的核心 也是fakeMSI框架对外暴露的唯一接口
    * APIPortal在其初始化阶段主要负责所有api的注册任务 以及保存用户传递进来的context上下文的保存工作
    * APIPortal初始化工程中涉及到两个重要的类 *ApiCallManager* 和 *FakeServiceLoader* 分别用于api调用的处理以及所有api类的加载帮助api管理类进行加载
    * APIPortal对外提供Invoke接口实现api的调用 该函数负责解析客户传递的 requestData json格式的字符串生成对应的 request后续通过中间件链路完成api的调用并将结果以json字符串的格式返回 用户也可以通过在 初始化时传递的dispatcher自定义返回数据的使用方式 APIPortal负责在api执行结束后调用dispatcher中注册的回调函数
3. APIPortal.Invoke() 通过中间件链路完成api的执行 下面简单介绍一下中间件链路的设计
    * 具体的链路采用洋葱模型实现可以实现调用前执行 调用后按照反方向再次执行
        * 路由
        * 权限检查（应该没啥可检查的😂？）
        * 参数校验（通过annotations实现参数的校验）
        * 执行


大体的框架就是上述的这样 后续会有更多的设计方案加进来 包括 apiNode BaseApiMethod 等类的设计思路 以后再说吧

--*未完成* 
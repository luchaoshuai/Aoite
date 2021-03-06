# Aoite(Any one item!)
一个适于任何 .Net Framework 4.0+ 项目的快速开发整体解决方案。

# 介绍
本项目从2009年孵化（V->Sofire->Aoite），至今已度过5个年头。一直在优化，一直在重构，一直在**商用**。有十分完整的单元测试用例。可以放心使用（我吹牛了，请暂时不要商用，目前开源版还未彻底完成所有功能，请等到 CommandModel 模块完成。）。更多内容请关注我的[博客园](http://www.cnblogs.com/sofire)。

# Changelog

**2015-01-23**

1. 增加模块 `Aoite.CommandModel` 以及对应的单元测试。
2. 改善 `System.Db.IsThreadContext` 在没有设置 `System.Db.Engine` 相关信息时返回 false，而不是抛出错误。
3. 新增 `Aoite.Data.DbEngine.ResetContext` 方法，可以通过调用此方法，释放当前上下文的 `Aoite.Data.DbContext` 对象。
4. 将 `Aoite.Redis.RedisManager.Reset` 重命名为 `ResetContext`。
5. 恢复 `Aoite.Serialization.QuicklySerializer` 的命名空间缩写功能，并修复对 Nested Class 的支持。
6. 增加 `System.IIocContainer.GetFixedService<T>` 方法。用于获取手工注册的服务（不会自动解析）。
7. 改善 `System.ObjectFactory.AllType` 的取值方式。

**2015-01-21**

1. 增加 `Aoite.Redis.RedisSessionStateStoreProvider`，可将 Redis 用于 ASP.NET 应用程序的会话状态。通过 `web.config` 文件配置（配置详见 Code.1）。
2. `IRedisClient` 增加扩展方法：Lock（分布式锁）、HGetAll<T>（可以通过 Redis Hash 泛型出一个对象）。
3. `Aoite.Serialization.QuicklySerializer` 增加：CustomAttribute 类和ISerializable 接口，用于序列化/反序列化特殊的类型使用。增加 `Aoite.Serialization.QuicklySerializer.CustomAttributes` 用于动态注册特性。
4. 移除 `Aoite.Serialization.QuicklySerializer` 在序列化过程中对命名空间进行缩写的功能（因为这会导致 Nested Class 无法序列化，虽然可以解决这个问题，但最终还是删除了这块功能）。

**code.1**

	<system.web>
	  <sessionState mode="Custom" customProvider="RedisSessionStateProvider">
	    <providers>
	      <clear />
	      <add name="RedisSessionStateProvider" 
	           type="Aoite.Redis.RedisSessionStateStoreProvider" 
	           address="localhost:6379" password="" />
	    </providers>
	  </sessionState>
	</system.web>

# Project Plan （2015-01-19 ~ 2015-01-24）
1. <s>完成 Redis 的 95%+ 命令</s>。
	* 考虑实现基于面向对象扩展方式。
	* RealCall 单元测试前期可能不会实现所有命令。
	* Pub/Sub 模块。
2. <s>完成 Cache 模块（融入到 CommandModel 模块中）2015-01-23 完成</s>。
3. <s>完成 CommandModel 模块（这个模块是 Aoite 最大亮点之一，暂时保密用途）2015-01-23 完成</s>。
4. 完成 ASP.NET MVC CommandModel 模块。
5. 编写文档（2015-01-24 以后，从博客园首发）。

# 已完成重要模块介绍
##Aoite
1. Aoite.Data：数据库交互模块。你从未有过的数据库连接体验方式。
2. Aoite.LevelDB：Google LevelDB 封装。需要的人很需要，不需要的人可以略过。
3. Aoite.Logger：日志模块。小巧易用好扩展，居家旅行，排查解读。
4. Aoite.Net：其实这块以前费了很大心思（以前的Sofire版就是这样的），但是由于存在内存泄漏，这次的重构，暂时不放出来。
5. Aoite.Reflection：感谢[Fasterflect](http://fasterflect.codeplex.com/)。版权归其所有。
6. Aoite.Serialization：一个快速的二进制序列化器。

## System
1. System.Mapping：绝对干货。快速反射。
2. System.IOC：智能 Ioc 模式。从此告别依赖。
3. System.Random：最好用的随机模块。

## 更多内容
在文档尚未撰写完毕之前，你可以通过单元测试了解整个框架。欢迎批评指导~

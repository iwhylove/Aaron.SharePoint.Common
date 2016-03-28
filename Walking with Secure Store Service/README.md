# 做SharePoint开发时你想把敏感信息存在哪里? #

做Web开发的小伙伴们经常遇到的场景之一就是连接外部数据源做增删改查的操作,那么做为敏感信息的链接字符串是放在什么地方的呢?ASP.NET中的Web.config貌似是一个不错的选择,那么在开发同样是基于ASP.NET的SharePoint应用时,你会把他们存放到哪里呢?

有的小伙伴说,我还是可以放在Web.config里面啊,没错我们可以,但是如果当前的SP Farm中包含有多台前端的时候问题来了,你需要修改每一台前端的Web.config,不能遗漏任意一台,而且您可能有所不知,SharePoint本身有一套机制用来控制和管理他所对应的Web.config文件,这可以保证在某些出错的情况下SharePoint可以利用保存的信息自动恢复最后一次成功记录下来的Web.config内容,这样我们手动修改的内容可能在不知不觉中就消失了. 话说回来,即使你下定决心要手动修改了Web.config文件,那么随之而来的就是IIS服务的重启.这种情况在正式环境上一般是不允许随意操作的.

有没有其他的更好的办法呢?很明显是有的,有不小小伙伴会把这些信息存放到相应对应的PropertyBag中,这样可以通过代码方便的进行存取.做的更体面一些的小伙伴们会把敏感信息先加密后再存放.这样做无疑是非常好的,但是这样做对与不同的Web,SiteCollection甚至WebApplication我们就要维护几套相同的内容.

SharePoint中有没有提供这样一种服务,可以让我们把需要的信息集中存放在一处,而且可以共享给与之关联的WebApplication呢?答案是有的.可能在那么多大名鼎鼎的服务中他并不起眼,他的名字叫**Secure Store Service**. 虽然他不是很起眼,但是他在SharePoint平台所起的作用绝对不可忽视. <br />

首先我们来看看MSDN中是怎么介绍它的.
*Secure Store Service 是运行在应用程序服务器上的授权服务。Secure Store Service 提供一个用于存储凭据的数据库。这些凭据通常由用户标识和密码组成，不过也可包含您定义的其他字段。例如，SharePoint Server 2013 可以使用安全存储数据库来存储和检索用于访问外部数据源的凭据。Secure Store Service 为存储多个后端系统的多组凭据提供了支持。
<br />
安全存储的使用方案包括：
<br />
Excel Services 可使用安全存储提供对已发布工作簿中的外部数据源的访问。这可以用作将用户凭据传递给数据源（此过程通常需要配置 Kerberos 委托）的替代方式。如果您需要为数据身份验证配置无人参与服务帐户，则 Excel Services 需要安全存储。
<br />
Visio Services 可使用安全存储提供对已发布的数据连接图表中的外部数据源的访问。这可以用作将用户凭据传递给数据源（此过程通常需要配置 Kerberos 委托）的替代方式。如果您需要为数据身份验证配置无人参与服务帐户，则 Visio Services 需要安全存储。
<br />
PerformancePoint Services 可使用安全存储提供对外部数据源的访问。如果您需要为数据身份验证配置无人参与服务帐户，则 PerformancePoint Services 需要安全存储。
<br />
Power Pivot 需要安全存储以便对 PowerPivot 工作簿进行计划刷新。
<br />
Microsoft Business Connectivity Services 可使用安全存储将用户凭据映射到外部系统中的一组凭据。您可将每个用户的凭据映射到外部系统中的唯一帐户，也可以将一组经过身份验证的用户映射到单个组帐户。Business Connectivity Services 还可以使用安全存储来存储用于访问 SharePoint Online 中的本地数据源的凭据。
<br />
SharePoint 运行时可使用安全存储来存储与 Azure 服务进行通信所必需的凭据（如果任何用户应用程序需要 SharePoint 运行时来设置和使用 Azure 服务）。* 

题外话:请告诉我看了这段文字后的第一感觉是什么?是不是感觉很晕,不知道他在说什么?那就对了,虽说阿尔法狗在围棋上已经超越了几乎所有的人类,但是至少在英文翻译成正常的中文方面,可能还需要不少时间来进化.


简单说来这个Secure Store Service可以帮您存储用户名密码以及其他敏感信息也不用担心被破解.还为链接其他外部服务或系统提供支持. 

你是不是会说:哎哟,不错,碉堡了,我想现在就用上它.请快告诉我怎么配置,使用和维护吧.
好吧,还是国际惯例的先给自己挖个坑,你们想要的这些内容应该不久就会填上的,请大家相信我.

参考文档: <br />
*https://technet.microsoft.com/zh-cn/library/ee806889.aspx <br />
https://technet.microsoft.com/en-us/library/ee806889.aspx*









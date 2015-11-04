##Content Type Hub
做SharePoint开发应该都比较熟悉一些术语其中之一就是Content Type (下文会简称成CT). 打一个不太恰当的比方,CT可以简单理解成SharePoint环境中的一个可重用部件,带有自己的属性(字段),当然也可以被继承.在之前版本的SharePoint中,跨SiteCollection共享CT是无法实现的,如果你真的有这方面的需求,那么在部署,维护的过程中可能就会给你带来了很多困扰.<br />


#### 题外话1

在从MOSS 2007演进到SP2010的过程中, MS对整个SP的架构做了不少的改变,其中最为显著的改变之一就是把之前臃肿的 SharedService 组件重新设计成 Service Application 架构. 在SP 2010中 Service Application 无处不在,从你熟悉的 UserProfileService, ExcelService 到新加入的Managed Metadata Service等等都是以 Service Application 的形式创建并且提供服务的.

与之前SSP的方式相比, SP 2010 的Service Appliciton 在提供服务时更加轻便与灵活.
MOSS2007时代的SSP,不管你用到多少SP的服务(当时默认提供的服务也不是很多),你都必须和SSP整体做绑定,假设其中的SearchService崩溃了,那么SSP也无法继续提供其他服务了. SP2010中可以只关联用到的Service,各个Service Application也是相互独立,在一般情况下自身的错误与崩溃并不会影响其他Service Application.

#### 回到正题
SP2010中, 默认提供了一种新的Service Application,名字叫Managed Metadata Service (下文中会简称成MMS).有了这个Service,管理员可以维护Farm中允许使用的术语以及对应的层次结构. 我们在创建字段时可以使用预先定义的术语集. 同时MMS还提供了另一个功能,和CT相关,那就是 Content Type Hub

Content Type Hub是一个集中发布CT的站点,所有订阅了相同的Content Type Hub的Site Collection 都能获得在Content Type Hub 站点上发布的CT.


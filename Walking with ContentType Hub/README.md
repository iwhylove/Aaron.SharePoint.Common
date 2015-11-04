##Content Type Hub
做SharePoint开发应该都比较熟悉一些术语其中之一就是ContentType. 打一个不太恰当的比方,ContentType可以简单理解成SharePoint环境中的一个类,带有自己的属性(字段),当然也可以被继承.在之前版本的SharePoint中,跨SiteCollection共享ContentType是无法实现的,如果你真的有这方面的需求,那么在部署,维护的过程中可能就会给你带来了很多困扰.<br />


#### 题外话1

在从MOSS 2007演进到SP2010的过程中, MS对整个SP的架构做了不少的改变,其中最为显著的改变之一就是把之前臃肿的 SharedService 组件重新设计成 Service Application 架构. 在SP 2010中 Service Application 无处不在,从你熟悉的 UserProfileService, ExcelService到新加入的Managed Metadata Service等等都是以 Service Application 的形式创建并且提供服务的.

与之前SSP的方式相比, SP 2010 的Service Appliciton 在提供服务时更加轻便与灵活.与之前SSP不管你用到多少服务,你都必须和SSP整体做绑定,假设其中的SearchService崩溃了,那么SSP也无法继续提供其他服务了.


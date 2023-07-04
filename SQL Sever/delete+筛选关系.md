表 "User" 是star table

表 "User_Module" 是 关系表

目的:

删除表"User_Module"中的某些行,筛选条件包含表"User"中的信息

使用关键词:

using

不能使用inner join 因为delete不能和inner join 一起用

代码:
    Select * from "User"
    inner join "User_Module"
    on "User_Module"."UserId" = "User"."Id" 
    where "HappEnabled"='false' and "ModuleNormalizedName"='HAPP_FAQS'

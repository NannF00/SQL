表 "User" 是star table

表 "User_Module" 是 关系表

目的:

删除表"User_Module"中的某些行,筛选条件包含表"User"中的信息

使用关键词:

using

不能使用inner join 因为delete不能和inner join 一起用

查看将要被删除的行:

    Select * from "User"
    inner join "User_Module"
    on "User_Module"."UserId" = "User"."Id" 
    where "HappEnabled"='false' and "ModuleNormalizedName"='HAPP_FAQS'

删除行:

    Delete
    FROM "User_Module"
    using "User"
    where "User_Module"."UserId" = "User"."Id"
    and "User"."HappEnabled"='false'
    and "User_Module"."ModuleNormalizedName"='HAPP_FAQS'


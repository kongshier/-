> ✨作者：猫十二懿
>
> ❤️‍🔥账号：[CSDN](https://blog.csdn.net/qq_56098191) 、[掘金](https://juejin.cn/user/3320978695270526) 、[个人博客](https://kongshier.github.io/) 、[Github](https://github.com/kongshier) 
>
> 🎉公众号：猫十二懿

# 练习

**规范化案例分析与设计**

假设对电子商务系统的业务描述如下： 

- 商品（Product）信息包括编号（P_id）、名称（P_Name）、类别（P_ Category）、价格（P_ Price）、生产厂家（P_Facturer）、入库时间（P_time）、详细信息（P_ Descn）、缩略图（P_ Image）。 
- 订单（Order）信息包括：编号（O_id）、提交时间（O_Time）和当前状态（O_Status）。 
- 购买人（Customer）信息包括姓名（C_Name）、性别（C_Sex）、联系方式（C_Contact）、电子邮箱（C_Email）。

其中，电子邮箱确定唯一购买人，联系方式统一存储了购买者的送货地址（C_Addr）、邮政编码（C_Zip）和购买人的手机号码（C_phone）。 订单的购买商品信息包括：商品的名称（P_Name）、商品的类别（P_Category）、商品的缩略图（Image）、商品的购买数量（Qty）、商品的销售单价（P_ Price1）。上述信息需与商品信息对应。 销售过程为：购买人下单生成订单（Generate），然后再挑选（Pick）商品加入到订单中。 

根据以上描述定义如下关系模式： 

- Product (P_id,P_Name,P_ Category,P_ Price,P_Facturer,P_time,P_ Descn,P_ Image) 
- Order(O_id,O_Time,O_Status,C_Email) 
- Customer(C_Name,C_Sex,C_Contact,C_Email) 
- Pick(O_id,P_id,Qty,P_ Price1)

1 写出每个关系的最小依赖集（基本的函数依赖集，不是导出的函数依赖）；指出是否存在传递函数依赖；对于函数依赖左部是多属性的情况，讨论其函数依赖是完全函数依赖还是部分函数依赖，指出各关系的候选码。

（1）Product

函数依赖集：{P_id->P_Name,P_id->P_Category,P_id->P_Price,P_id->P_Facturer,P_id->P_time,P_id->P_Descn,P_id->P_Image}

传递函数依赖：无

部分函数依赖：无

完全函数依赖：{P_id->P_Name,P_id->P_Category,P_id->P_Price,P_id->P_Facturer,P_id->P_time,P_id->P_Descn,P_id->P_Image}

候选码：P_id



（2）Order

函数依赖集：{O_id->O_Time,O_id->O_Status,O_id->C_Email}

传递函数依赖：无

部分函数依赖：无

完全函数依赖：{O_id->O_Time,O_id->O_Status,O_id->C_Email}	

候选码：O_id



（3）Customer

函数依赖集：{C_Email->C_Contact,C_Contact->C_Name,C_Contact->C_Sex}

传递函数依赖：C_Name对C_Email传递函数依赖；C_Sex对C_Email传递函数依赖

部分函数依赖：无

完全函数依赖：{C_Email->C_Contact,C_Contact->C_Name,C_Contact->C_Sex}

候选码：C_Email



（4）Pick

函数依赖集：{(O_id,P_id)->Qty,(O_id,P_id)->P_Price1}

传递函数依赖：无

部分函数依赖：无

完全函数依赖：{(O_id,P_id)->Qty,(O_id,P_id)->P_Price1}

候选码：(O_id,P_id)



2.使用数据规范化分析方法，分析每个关系模式属于第几范式。

（1）属于第三范式。每一个属性都是原子属性，没有部分函数依赖于主键，没有传递依赖于主键

（2）属于第三范式。每一个属性都是原子属性，没有部分函数依赖于主键，没有传递依赖于主键

（3）非范式模式。C_Email属性还可以再分为其他的属性，第一范式不满足。

（4）属于第三范式。每一个属性都是原子属性，没有部分函数依赖于主键，没有传递依赖于主键










经理培养计划

# 项目背景
人力部门每年都进行管理层访谈，以评估管理层人员的能力和待提高方向。为了更好地跟踪评估结果并分析数据，人力部门正在推进信息数字化。

然而，现有的跟踪评估方式存在规范性不足的问题。因此，人力部门希望能够以更加规范的方式进行长时间的跟踪评估，并以更直观的方式分析数据。

同时，信息中心希望能够打通部门数据共享，以帮助更好地评估管理层人员的能力和待提高方向。

# 业务需求
为HR部门制作访谈表单，帮助发放、记录和回收访谈问卷，同时能够提供跨部门的数据分析仪表盘。

## 具体需求

### 1.问卷发送（5.29已完成）

人力部门能够进行总控，当确定被访谈人后，能够自动关联上下级，手动填写相关方。


### 2.设计两个访谈页面

2.1 页面1是展示单次访谈中，被访谈者提到过的对【管理层人员】评价；

2.2 页面2是展示汇总访谈中，【管理层人员】的总体得分情况和问题汇总。

### 3.数据分析
要求使用数据仪表盘，展示两个报表。

3.1 报表1需要显示评价者的基本信息（姓名，关系，对于开放问题的回答）

3.2 报表2则只使用数字，计算各维度均分，和得分低于6分的维度次数。

PS：例如有两个人评价A的维度1低于6分，则【得分低于6分的维度次数】为2


### PS：参考《成长访谈》表单。


## 问卷发送

### 需求说明
1.人力部门能够进行总控，当确定被访谈人后，能够自动关联上下级，手动填写相关方。

### 完成情况
5.29已完成。

### 字段设计

#### 被评价者姓名
被评价者姓名-成员单选-可选范围（自定义）-允许重复值-可见/可编辑

#### 关系
受访人与被评价者的关系-单选按钮-使用显隐规则进行选择

#### 姓名联动
联动表单：基础数据-人员信息

🌟需要申请【跨应用授权】

##### 上级姓名
if (简道云账号 == 管理层姓名){当前表单 上级姓名 == 联动表单 直接主管} 

##### 下级姓名
if (联动表单 直接主管 == 当前表单 管理层姓名){当前表单 下级姓名 == 简道云账号}


##### 相关方姓名
需要手动输入，由于单选按钮显隐规则仅支持固定文本，所以另提供单行文本供录入。

相关方姓名-成员单选

相关方关系-单行文本（提供默认值“受访人是该管理层人员的xx”）


## A组访谈页面

### 需求说明
页面1是展示单次访谈中，被访谈者提到过的对【管理层人员】评价；

### 字段设计

有默认的主被评价人，但是访谈中出现的其他管理层人员也需要被记录到表中，请使用新增数据。

🌟✨问题：需要使用子表单进行收集，但是子表单会过长，不利于问卷收集人员的填写。

要不就是提交单个表单，让业务人员多交几次。


#### 被评价人
被评价人-成员单选

🌟问题在于如何联动？？写哭了

美女变包公，让HR手动输入下名字确认（感觉会被骂死）。

一个方法：

{"text":"IFS(AND(ISEMPTY(A)==0,ISEMPTY(B),ISEMPTY(C)),A,AND(ISEMPTY(B)==0,ISEMPTY(A),ISEMPTY(C)),B,AND(ISEMPTY(C)==0,ISEMPTY(A),ISEMPTY(B)),C)","marks":[],"cmf":true}

#### 量化分数
##### 维度1分数
维度1分数-单选按钮组（1-10分）
##### 维度2分数
维度2分数-单选按钮组（1-10分）
##### 维度3分数
维度3分数-单选按钮组（1-10分）
##### 其他建议
其他问题（HR填写）-多行文本-问题记录

#### 开放性问题
##### 问题1
问题1（IT人员设置）-多行文本
##### 问题2
问题2（IT人员设置）-多行文本
##### 问题3
问题3（IT人员设置）-多行文本
##### 其他问题
其他问题（HR填写）-多行文本-问题记录

其他问题回答（HR填写）-多行文本-回答记录
##### 问题总结
问题总结（HR填写）-多行文本-总结记录

#### 确认按钮
该按钮作用是为了让HR填写尽可能全面的访谈记录

确认按钮-单选按钮（是/否）-【是否已记录访谈中提到的所有管理层人员评价？】

## FAQ
### 【成员单选】的字段设置
成员单选字段类型的数据源并不来自于其他表单，而是来自于当前表单所属的应用中的成员列表。


### 智能助手
如果要更新表单数据，使用智能助手比较方便，就不是表单联动的问题，是直接新增新数据。


### 工作记录
5.30 今天尝试解决多表单数据联动问题，还是没有想清楚主key的设计，无法很准确地描述自己的问题。在开始动工前先搞清楚要的是什么，再动手。先做设计然后再开始拖拽写码！

聚合表也需要企业授权。

#### 数据联动和关联其他表单
数据联动是指在一个表单中填写或修改某个字段的值后，自动触发另一个或多个表单中相关字段的值的更新。例如，在一个销售订单表单中填写客户名称后，自动更新客户联系人、电话等信息。

关联其他表单则是指在一个表单中添加一个字段，该字段可以与另一个或多个表单中的字段建立关联，以便在当前表单中显示关联表单中的相关信息。例如，在一个客户信息表单中添加一个“订单”字段，可以与销售订单表单建立关联，以便在客户信息表单中查看该客户的所有订单信息。

因此，数据联动适用于在同一表单中不同字段之间的数据交互，而关联其他表单则适用于不同表单之间的数据交互。

### 术语
#### 鉴权authentication
假设你是一个管理者，手里有一把万能钥匙，可以打开公司里所有的房间。但是，有些房间你不希望员工进去，因此你给这些房间锁上了门，并且只给了特定的员工一把钥匙。数据源表单就像是这些被锁上的房间，只有特定的员工（有权限的表单）才能用万能钥匙（数据管理表）打开这些房间（进行操作）。

### 表格状态
#### 问卷发送
上下级使用公式联动，有些人员可以，有些人员不行。原因未知，感觉可能和数据库的设计方式有关系。
IFS(AND(ISEMPTY(上级姓名)==0,ISEMPTY(下级姓名),ISEMPTY(相关方姓名)),TEXTUSER(上级姓名,\"name\"),AND(ISEMPTY(下级姓名)==0,ISEMPTY(上级姓名),ISEMPTY(相关方姓名)),TEXTUSER(下级姓名,\"name\"),AND(ISEMPTY(相关方姓名)==0,ISEMPTY(上级姓名),ISEMPTY(下级姓名)),TEXTUSER(相关方姓名,\"name\"))

需要增加辅助字段表

## 关联选择
使用关联数据，无法使用子表单。
规则设计：关联a组访谈页面，选择数据时的显示字段-评价人姓名，表单中的显示字段-评价人姓名；过滤条件：被评价人姓名=被评价人姓名，允许新填充-评价人姓名

无法实现多个评价人的情况



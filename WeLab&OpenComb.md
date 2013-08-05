## 技术细节说明

### 命名约定

* 扩展名和扩展目录一致，且只能使用小写字母，_,- ，这个规则和 npm 兼容

* 数据表(collection) 的名称规范：  <扩展名>/<数据表名>
例如：用户数据表的完成名称是 "ocframework/users"
其中 "ocframework“ 是扩展名， users 是属于这个扩展的数据表名称

使用 helper.db ，可以省略 "<扩展名>/" 部分，只是用数据表名。 helper.db 根据源代码文件所在的扩展自动补充 扩展名。




## Git服务器
使用两个 git 服务， bitbucket, github  。 OpenComb的代码在 github 上， WeLAB的私有代码在 bitbucket 上。

## OpenComb扩展和git库 说明

### 1. CRM（客户关系管理）扩展
repo: https://github.com/aleechou/ocCRM
微信的 关注用户/注册用户 使用 CRM扩展，便于以后实现微信渠道以外的营销方式，例如：群发email, sms短信, weibo 甚么的。
也就是说，微信的用户 实际上是读写 CRM扩展 的数据表；在写入时 增加微信所需的扩展。

#### 数据表：occrm/customers   

字段： 
_id             主键
realname     姓名
gender        性别
birthday      生日(年龄)
city             城市
---(以上字段显示在 list 页)
priovince     省份
email          电子邮件
mobile        移动电话
tel              电话
fax              传真

#### 数据表：occrm/customerTags 
客户的标签

字段：
tagname    标签名称
uid            外键：occrm/customers 表 _id 字段
createtime  创建时间

索引：
uid
tagname, uid (唯一)
createTime


### 2. 微信扩展
repo: https://github.com/aleechou/ocWeChat
微信的API授权，用户和用户二次注册。也包括WeLAB的 layout 。



#### 数据表：occrm/customers （使用 ocCRM 的数据表）

增加字段：
wechatApiId     微信 api id
followTime      关注时间
registerTime    注册时间（无此字段，或此字段空，表示未完成二次注册，仅为关注用户）
sessions        会话次数
lastSessionTime 最近会话时间


#### 数据表：ocwechat/messages

字段：
_id             主键
uid             外键：occrm/customers 表 _id 字段
time            发送时间
type            类型： "text", "image", "audio", "location"
contents        内容
hitKeyword      命中关键字

索引：
uid
hitKeyword


### 3. CMS扩展
repo: https://github.com/aleechou/ocCMS
内容管理部分。







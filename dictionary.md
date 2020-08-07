# 租房项目数据库字典

### 目录

- 功能概述
- 数据对照表


---

**1\. 功能概述**

&emsp;&emsp;项目主要功能包括：
包含权限管理、用户管理、菜单管理、文章管理、房源管理、订单管理等基本模块；

---
**2\. 数据对照表**

### 通用字段说明

| 字段 | 类型 | 说明 |
| ------ | :------: | ------ |
| id | int(11)| 主键：该数据ID |
| listorder | int(11) | 自定义排序 |
| img_array | varchar(100) | 图片组 |
| create_time | int(11) | 创建时间 |
| update_time | int(11) | 更新时间 |
| delete_time | int(11) | 删除时间 |
| thirdapp_id | int(11) | 关联thirdapp |
| user_no | varchar(255) | 关联user |
| user_type | tinyint(2) | 用户类型0.前端2.cms |
| status | tinyint(2) | 状态:1正常；-1删除 |



### user表

| 字段 | 类型 | 说明 |
| ------ | :------: | ------ |
| login_name | varchar(100) | 登录名 |
| password | varchar(255) | 密码 |
| nickname | varchar(255) | 微信昵称 |
| openid | varchar(50) | 微信openid |
| headImgUrl | varchar(9999) | 微信头像 |
| role | int(11) | 权限角色 |
| primary_scope | int(11) | 权限级别：60.项目管理员;30.门店;10用户 |
| user_type | tinyint(2) | 0,小程序用户;q,门店;2,cms用户; |
| user_no | varchar(255) | 用户编号 |



### user_info表

| 字段 | 类型 | 说明 |
| ------ | :------: | ------ |
| name | varchar(255) | 名称 |
| address | varchar(255) | 地址 |
| phone | varchar(255) | 电话 |



### label表

| 字段 | 类型 | 说明 |
| ------ | :------: | ------ |
| title | varchar(40) | 菜单名称 |
| description| varchar(255) | 描述 |
| parentid| int(11) | 父级菜单ID |
| type | tinyint(2) |  1,文章;2,问题类别;3,租房;4,二手房;5,办公; |
| behavior | tinyint(2) | 租房:1.标签2.配套设施 |



### article表-update

| 字段 | 类型 | 说明 |
| ------ | :------: | ------ |
| menu_id | int(11) | 租房 |
| title | varchar(100) | 标题 |
| description | varchar(255) | 房源编号 |
| addressImg | text | 地址图 |
| headImg | text | 头像 |
| contact | varchar(100) | 联系人 |
| shop | varchar(100) | 门店名称 |
| mainImg | text | 主图 |
| bannerImg | text | 轮播图 |
| phone | varchar(255) | 手机号 |
| renovation | varchar(20) | 装修：豪装/精装/中装/简装/毛坯 |
| pay_type | varchar(20) | 付款方式：押一付三/押一付一/押一付二/半年付/年付/其他 |
| orientation | varchar(20) | 朝向：东/南/西/北/东南/东北/西南/西北/南北通透 |
| price | int(11) | 价格 |
| room | varchar(20) | 几室 |
| layout | varchar(20) | 房型 |
| area | int(11) | 面积 |
| floor | varchar(20) | 楼层 |
| elevator | varchar(10) | 电梯 |
| years | varchar(20) | 年代 |
| building_type | varchar(20) | 建筑类型 |
| building_num | varchar(20) | 房屋总数 |
| property | varchar(50) | 物业 |
| property_fee | varchar(20) | 物业费 |
| developer | varchar(50) | 开发商 |
| village | varchar(50) | 小区 |
| address | varchar(100) | 地址 |
| second_price | varchar(20) | 二手房价 |
| longitude | varchar(255) | 经度 |
| latitude | varchar(255) | 纬度 |
| hot | tinyint(2) | 热门：0.否1.是 |
| excellent | tinyint(2) | 优选：0.否1.是 |
| facilities | varchar(255) | 设施 |
| tag | varchar(255) | 特色标签 |


| menu_id | int(11) | 二手 |
| title | varchar(100) | 标题 |
| description | varchar(255) | 房源编号 |
| addressImg | text | 地址图 |
| headImg | text | 头像 |
| contact | varchar(100) | 联系人 |
| shop | varchar(100) | 门店名称 |
| mainImg | text | 主图 |
| bannerImg | text | 轮播图 |
| phone | varchar(255) | 手机号 |
| price | int(11) | 售价 |
| room | varchar(20) | 几室 |
| layout | varchar(20) | 房型 |
| area | int(11) | 面积 |
| orientation | varchar(20) | 朝向：东/南/西/北/东南/东北/西南/西北/南北通透 |
| unit_price | decimal(10,2) | 单价 |
| show_time | varchar(20) | 挂牌 |
| floor | varchar(20) | 楼层 |
| elevator | varchar(10) | 电梯 |
| renovation | varchar(20) | 装修：豪装/精装/中装/简装/毛坯 |
| years | varchar(20) | 年代 |
| purpose | varchar(20) | 用途 |
| ownership | varchar(20) | 权属 |
| building_type | varchar(20) | 建筑类型/楼型 |
| building_num | varchar(20) | 房屋总数 |
| property | varchar(50) | 物业 |
| property_fee | varchar(20) | 物业费 |
| developer | varchar(50) | 开发商 |
| village | varchar(50) | 小区 |
| address | varchar(100) | 地址 |
| second_price | varchar(20) | 二手房价 |
| longitude | varchar(255) | 经度 |
| latitude | varchar(255) | 纬度 |
| hot | tinyint(2) | 热门：0.否1.是 |
| excellent | tinyint(2) | 优选：0.否1.是 |
| tag | varchar(255) | 特色标签 |


| menu_id | int(11) | 办公 |
| title | varchar(100) | 标题 |
| description | varchar(255) | 房源编号 |
| addressImg | text | 地址图 |
| headImg | text | 头像 |
| contact | varchar(100) | 联系人 |
| shop | varchar(100) | 门店名称 |
| mainImg | text | 主图 |
| bannerImg | text | 轮播图 |
| phone | varchar(255) | 手机号 |
| price | int(11) | 价格 |
| area | int(11) | 面积 |
| region | varchar(20) | 区域 |
| location | varchar(20) | 位置 |
| station | int(11) | 工位 |
| elevator | varchar(10) | 电梯 |
| renovation | varchar(20) | 装修：豪装/精装/中装/简装/毛坯 |
| room | varchar(20) | 房间：整栋租赁/带办公家具/整层租赁/独立会议室 |
| years | varchar(20) | 年代 |
| purpose | varchar(20) | 用途 |
| ownership | varchar(20) | 权属 |
| building_type | varchar(20) | 建筑类型/楼型 |
| building_num | varchar(20) | 房屋总数 |
| property | varchar(50) | 物业 |
| property_fee | varchar(20) | 物业费 |
| developer | varchar(50) | 开发商 |
| village | varchar(50) | 小区 |
| address | varchar(100) | 地址 |
| second_price | varchar(20) | 二手房价 |
| longitude | varchar(255) | 经度 |
| latitude | varchar(255) | 纬度 |
| hot | tinyint(2) | 热门：0.否1.是 |
| excellent | tinyint(2) | 优选：0.否1.是 |
| tag | varchar(255) | 热门标签 |


| menu_id | int(11) | 车位 |
| title | varchar(100) | 标题 |
| description | varchar(255) | 车位编号 |
| addressImg | text | 地址图 |
| headImg | text | 头像 |
| contact | varchar(100) | 联系人 |
| shop | varchar(100) | 门店名称 |
| mainImg | text | 主图 |
| bannerImg | text | 轮播图 |
| phone | varchar(255) | 手机号 |
| price | int(11) | 价格 |
| area | int(11) | 面积 |
| ground | varchar(20) | 地下/室外 |
| unit_price | decimal(10,2) | 单价 |
| region | varchar(20) | 区域 |
| village | varchar(50) | 小区 |
| pay_type | varchar(20) | 付款方式：月付/季付/年付 |
| longitude | varchar(255) | 经度 |
| latitude | varchar(255) | 纬度 |
| hot | tinyint(2) | 热门：0.否1.是 |
| excellent | tinyint(2) | 优选：0.否1.是 |


| menu_id | int(11) | 关于我们 |
| title | varchar(100) | 关于我们 |
| phone | varchar(255) | 手机号 |
| description | varchar(255) | 微信号 |
| content | text | 文章内容 |


| menu_id | int(11) | 轮播 |
| description | varchar(255) | 跳转链接 |
| mainImg | text | 主图 |



### relation表

| 字段 | 类型 | 说明 |
| ------ | :------: | ------ |
| relation_one | varchar(255) | 主表ID |
| relation_one_table | varchar(255) | 主表Article |
| relation_two | varchar(255) | 关联ID |
| relation_two_table | varchar(255) | 关联表Label |



### message表-反馈问题

| 字段 | 类型 | 说明 |
| ------ | :------: | ------ |
| title | varchar(255) | 标题 |
| phone | varchar(255) | 手机号 |
| content | text | 内容 |
| mainImg | text | 主图 |

---
[TOC]

# 分站

## 前台
> 前台采用 Yaf 框架, 具体可先查看 [Yaf 官方文档][url_yaf] 熟悉基本用法

### 目录结构
> 目录结构大致与 Yaf 框架的目录结构一致, 个别地方有一些差别
```
├── admin                                       
├── application
│   ├── Bootstrap.php                    前台应用初始化
│   ├── controllers
│   │   ├── Error.php                    捕获异常相关代码, 比如路由配置错误, 报404在这里可以捕获
│   │   ├── Img.php
│   │   ├── Index.php                    默认主页控制器
│   │   ├── Message.php
│   │   ├── Region.php
│   │   ├── Rewrite.php
│   │   ├── Static.php
│   │   └── Test.php
│   ├── modules                          控制器相关, 具体目录都可对应url页面, 作用和命名差不多
│   │   ├── Ajax
│   │   ├── Api                          移动端相关接口
│   │   ├── Cart
│   │   ├── Checkout
│   │   ├── Goods
│   │   ├── Keywords
│   │   ├── News
│   │   ├── Specials                     主要用到Promotion, 后台设置的专题页面内容会在这里渲染
│   │   ├── User
│   │   └── \Webservice                   主要用到Cache, 清空对应View静态页面缓存
│   └── plugins                          服装网站用的不多
├── conf                                 配置相关
│   ├── admin.ini
│   ├── application.ini                  如果需要在`/application` 增加新的模块, 需要在这里设置对应的配置`modules`
│   ├── common.ini
│   ├── errcode.php
│   ├── inc_constant.php
│   ├── init.ini
│   └── mobile.ini
├── customhtml
├── data
│   ├── google
│   ├── log                              日志, 具体代码可以查看library/Pub_Log, 查看 paypal 记录可以在这里查找
│   │   ├── pinkclassy.com
│   └── ssu
│       ├── fairyseason.com
│       └── pinkclassy.com
├── index.php
├── library                              类库
│   ├── Cls                                     
│   │   ├── Bibit.php
│   │   ├── Bonus.php
│   │   ├── \CacheWebservice.php
│   │   ├── Consignee.php                会员收件人地址资料（逻辑处理类）
│   │   ├── Flow.php
│   │   ├── GlobalCollect.php
│   │   ├── Goodinfo.php
│   │   ├── GoodSearch.php               商品搜索专用类, sphinx相关设置在这里
│   │   ├── HeidelpayXML.php
│   │   ├── Images.php
│   │   ├── Main.php
│   │   ├── ObsCart.php
│   │   ├── ObsMailOld.php
│   │   ├── ObsMail.php                  发送邮件代码相关逻辑, 具体可以从这里追踪
│   │   ├── ObsMailwebpower.php
│   │   ├── Order.php
│   │   ├── Page.php
│   │   ├── SearchKeywords.php
│   │   ├── Ssu.php
│   │   ├── ThirdPartyCode.php
│   │   ├── Urhere.php
│   │   └── Userinfo.php                 账户相关的基本信息（逻辑处理类）
│   ├── Core
│   │   ├── Adapter.php                  数据库链接适配器, Mongo读主相关逻辑在这
│   │   ├── ADController.php
│   │   ├── Cls.php
│   │   ├── Controller.php               项目控制器基类, 方法@show_message 经常用到
│   │   ├── DBWr.php                            
│   │   ├── Exception.php                系统核心异常处理类
│   │   ├── Models.php
│   │   ├── Module.php
│   │   ├── MongoRecordIterator.php      Mongo迭代器实现
│   │   ├── MongoRecord.php              MongoDB数据表模型基类
│   │   ├── MongoWr.php
│   │   ├── MysqlWr.php                  数据库“增删改”操作，其他DBWr，MongoWr用的不多，数据写入主要从这里
│   │   ├── Observer.php
│   │   ├── Plugins.php
│   │   ├── SoapServer.php
│   │   ├── Subject.php
│   │   ├── Validate.php
│   │   ├── View.php                     V视图相关实现，采用smarty
│   │   └── \Webservice.php               \Webservice(Yar)请求基类，前台与后台的通信主要走这里，包括数据库CURD
│   ├── Diff
│   │   ├── diffAbs.php
│   │   └── PageFirstfun.php
│   ├── Ext
│   │   ├── base_facebook.php
│   │   ├── Facebook.php
│   │   ├── Payment                      支付相关, paypal用到最多
│   │   ├── Shipping
│   │   ├── ShippingCustom.php
│   │   └── View                         Smarty具体的实现
│   ├── Firebase
│   │   └── JWT
│   ├── Fuc
│   │   ├── Api
│   │   ├── Lib
│   │   ├── Payment
│   │   └── Smarty                       Smarty公共函数
│   ├── Lib                              公共函数
│   │   ├── lib_common.php
│   │   ├── lib_goods.php
│   │   └── lib_main.php
│   ├── M                                每新增一个表的, 需要在这里增加一个Model
│   │   ├── ...
│   ├── Pub
│   │   ├── Aecmp.php                    AECMP 基础类，许多初始化和检测都在这
│   │   ├── Cache.php                    缓存相关
│   │   ├── Captcha2.php                 验证码
│   │   ├── Captcha.php                  验证码
│   │   ├── Chinese.php
│   │   ├── Curl.php                     curl相关操作类
│   │   ├── Debug.php                    调试相关, 如果request包含debug_aecmp参数则会显示调试信息
│   │   ├── Des.php
│   │   ├── Error.php
│   │   ├── Image.php
│   │   ├── Inflector.php
│   │   ├── Json.php
│   │   ├── Lan.php
│   │   ├── Log.php                      日志实现
│   │   ├── Mail.php                     发送邮件类的具体实现
│   │   ├── Mod.php
│   │   ├── Params.php
│   │   ├── Quid.php
│   │   ├── RedisClient.php
│   │   ├── Redis.php                    Redis相关操作
│   │   ├── Rpc.php
│   │   ├── Session.php
│   │   ├── SphinxClient.php
│   │   ├── Template.php
│   │   ├── Token.php
│   │   ├── Url.php
│   │   ├── User.php
│   │   └── Validate.php
│   └── Sub
│       ├── Basic.php
│       ├── Comment.php
│       ├── Login.php
│       ├── Password.php
│       ├── Register.php
│       └── Resetpwd.php
├── mobile  
├── m-web                                移动端，采用 Vue 全家桶
├── rewrite.conf
├── temp
├── test1.txt
├── test.txt
├── themes                               Smarty视图层
│   ├── pinkclassy
│   ├── tablet-pc
├── upload_log.txt
└── user_up
```

### Paypal-In-Context 功能
> 这个功能是 paypal 提供的一种快捷支付方式, 
* [开发者中心][url_paypal1] 需要注册一个个人帐号, 然后创建测试环境买家帐号, 卖家帐号, 线上环境帐号需要业务申请
* [官方文档][url_paypal2]
* [官方Api 文档][url_paypal3]
* [官方 demo][url_paypal4] 可以下载demo到本地调试，对流程会有一个更清洗的认识
* [测试环境][url_paypal5]
* 前台核心代码都在 `\web\library\Ext\Payment\PaypalInContext.php`, 所有方法基本与 demo 一致

### 卡券
> 卡券涉及4张表 
> * `operation_coupon` 卡券详情信息表
> * `operation_coupon_goods_list` 限制商品类卡券 限制的商品
> * `operation_coupon_list` 用户卡券表
> * `operation_coupon_user_list` 在分站没有用到
>
> 卡券涉及到的逻辑在 `\web\library\M\Coupon.php`, 分站推送卡券数据的逻辑不影响分站前台逻辑, 分站用到卡券的地方目前在以下6个地方：
> 
> 1.结算页面获取当前用户可用卡券列表
>> 代码位置 `\web\library\M\Coupon.php @getAvailableCoupons`

![][img_coupon1]
>> 
```
这里会根据购物车的商品计算计算几个值与卡券的条件比较, 如
相同SPU的总额: `mapGoodsIdTotal`
购物车总额: `cartTotal` 对应 不限商品的卡券 的条件
分类商品集合: 根据 `mapCatGoodsIds, mapGoodsIdTotal` 计算相同分类的总额, 再与限制品类的卡券最小金额比较
扩展分类商品集合: 根据 `mapExtCatGoodsIds, mapGoodsIdTotal` 计算相同扩展分类的总额, 再与限制扩展卡券最小金额比较
限制商品的卡券商品集合: 根据`limitGoodsCouponIds, mapGoodsIdTotal` 计算限制商品卡券的商品总额, 再与最小金额比较
```
>> 具体卡券优惠金额计算在 `\web\library\M\OrderInfo.php @order_fee` 商品组合和订单促销也是在这个方法

![][img_coupon2]
>> 
```
卡券目前有两种优惠方式
    * 打折 
        具体是折算成单价, 比如满足条件的商品有A和B, 单价分别为10和5, 
        打5折, 则单价为5和2.5, 
        在与数量想成计算优惠后的金额, 而优惠金额是之前的总额减去优惠后的金额得到优惠金额, 
        注意顺序, 是先计算单价四舍五入再乘以数量, 而不是先乘以数量再四舍五入, 否则算出来导致优惠不正确
    * 满减
        会把满减金额累计在原来红包码的满减金额上, 其他流程与存储字段与上面一致, 
        当然红包码其他也为空, 只是红包码优惠也会显示优惠券满减金额
```


> 2.创建订单，计算卡券的优惠, 
>> 这里会把优惠金额再计算一次, 执行流程与上面一致，然后再把对应的优惠字段传给接口创建订单
>> 
>> 用户在创建订单之后, 支付之前不会调用平台的接口, 把平台对应卡券的数据更新使用状态, 而只有在支付完成之后才会调用平台接口
>> 
>> `\web\application\modules\Checkout\controllers\Done.php @successAction`

![][img_coupon3]
>> `\web\application\modules\User\controllers\Order.php @UpdateCouponStatus`

![][img_coupon4]

>> 
>> 有一种情况, 如果用户在创建订单之后不支付, 然后点击订单继续购买会恢复卡券的使用状态
>> 
>> `\web\library\M\Coupon.php @buy_againAction`

![][img_coupon5]
>> `\web\application\modules\User\controllers\Order.php @recoverCoupon`

![][img_coupon6]
> 3.个人中心，显示当前用户的卡券列表, 
>> 这个功能比较简单, 获取当前用户所有的优惠券然后判断是否过期, 是否可用
>> 需要注意一个地方, 卡券是否可用的状态在前台 有的是按图片显示 有的是按文字显示
> 4.卡券领取页面
> 5.注册送卡券
> 6.订阅送卡券


## 后台
> 后台采用 [yii1.1框架][url_yii1]

### 目录结构
> 目录结构参考 yii1.1, 目前后台基本没有新功能的开发，几乎都迁移至平台统一管理
> 
> 目前后台代码的核心是 Rpc 接口, 平台推送数据，前后台查看和更新数据都是同个 Rpc 接口
> 
> 接口采用的 PHP官方 [Yar 拓展][url_yar]
> 
> 文件目录如下
```
├── components
│   ├── base_facebook.php
│   ├── CURDdata.php
│   ├── DataAbs.php
│   ├── Datajson.php
│   ├── Dataphp.php
│   ├── Dataxml.php
│   ├── Facebook.php
│   ├── PaypalReconcilitation.php
│   ├── RpcAbs.php                              前台修改数据库需要在这里增加表名
│   ├── Rpc.php
│   └── YarController.php
├── controllers
│   ├── IndexController.php
│   ├── Order_erp_createController.php
│   ├── TgoodsController.php
│   └── TicketController.php
├── models
│   ├── Cart.php
│   ├── Commonlog.php
│   ├── EmailSendlist.php
│   ├── GoodsActivity.php
│   ├── PayLog.php
│   ├── PromotionsAction.php
│   ├── PromotionsVoted.php
│   ├── Thirdparty_email_webpowerlist.php
│   ├── TicketMessage.php
│   ├── Ticket.php
│   ├── TicketType.php
│   └── UserBonus.php
├── rpc
│   ├── activity
│   │   └── ActivityRpc.php
│   ├── ad
│   │   └── AdRpc.php
│   ├── ApiEmail.php
│   ├── ApiEmailService.php
│   ├── article
│   │   └── ArticleRpc.php
│   ├── BuyRpc.php                              创建订单
│   ├── CartRpc.php
│   ├── CatchGoodsRpc.php                       平台推送商品，删除商品相关方法
│   ├── CatchTopicRpc.php
│   ├── category
│   │   └── CategoryRpc.php
│   ├── CategoryRpc.php
│   ├── cfg
│   │   ├── DbRpc.php
│   │   ├── LanRpc.php
│   │   ├── NewsalesorderRpc.php
│   │   ├── SalesorderRpc.php
│   │   ├── ShopconfigRpc.php
│   │   ├── SiteinfoRpc.php
│   │   └── SystemRpc.php
│   ├── comment
│   │   └── CommentRpc.php
│   ├── coupon
│   │   ├── SynchronousCouponGoodsList.php
│   │   ├── SynchronousCouponList.php
│   │   ├── SynchronousCoupon.php
│   │   └── SynchronousCouponUserList.php
│   ├── DbRpc.php
│   ├── ErpOrderStatusRpc.php
│   ├── GetannlikeRpc.php
│   ├── GetgoodswarningRpc.php
│   ├── GetimgRpc.php
│   ├── goods
│   │   ├── BrandsRpc.php
│   │   ├── GoodsattrRpc.php
│   │   └── GoodsRpc.php
│   ├── GoodsRpc.php
│   ├── LanpackRpc.php
│   ├── MailRpc.php
│   ├── MainRpc.php
│   ├── NewsalesorderRpc.php
│   ├── OrderInfoRpc.php
│   ├── OtherRpc.php
│   ├── PaymentRpc.php
│   ├── PaypalInContextLogRpc.php               paypal-in-context 日志记录相关
│   ├── PromotionActivityRpc.php                促销活动(商品组合, 订单打折
│   ├── PromotionGoodsRpc.php                   商品促销(商品促销，商品抢购，商品批发)
│   ├── PromotionTopicRpc.php                   专题活动, 打标签活动
│   ├── RegionsRpc.php
│   ├── TicketController.php
│   ├── TicketRpc.php
│   ├── uc
│   │   ├── AccountLogRpc.php
│   │   ├── CollectGoodsRpc.php
│   │   ├── FeedbackRpc.php
│   │   ├── RegRpc.php
│   │   ├── UserAccountRpc.php
│   │   ├── UserAddressRpc.php
│   │   ├── UserExtRpc.php
│   │   └── UserRpc.php
│   ├── users
│   │   ├── SynchronousSiteUsers.php
│   │   └── SynchronousUsers.php
│   └── WebpowerRpc.php
├── views
│   └── default
│       └── index.php
└── YarModule.php
```

### 数据库新增表
* ![][img_db1]
* ![][img_db2]
* redis表字段如图：
* ![][img_db3]
* 注意删除表单默认的密码，更新之后需要清除 redis

### 数据库CRUD
* 前台如果要对数据库进行增删改操作需要编辑文件: `\webservice\protected\modules\yar\components\RpcAbs.php` 增加对应的表
* ![][img_db4]
* Rpc接口一般用 model 方法操作数据库, 需要导入配置的site_id, language_id 如下图
* 因为有一些model的表名增加了站点名字的表前缀，否认会找不到对应的表，插不进数据
* ![][img_db5]
* ![][img_db6]
* 前端在查询数据库的时候，前台代码文件：`\web\library\Core\MongoRecord.php` 也给条件加上了site_id, language_id两个字段, 所以最好每一张表都有site_id, language_id两个字段, 否认可能查询不到数据 或者有精力优化重构一下
* ![][img_db7]
* model CURD的条件可能与Yii1.1 有一点出入, 具体代码可以查看 `\webservice\protected\components\MongoCommand.php` 结合Yii1.1 文档,调试打印即可
* ![][img_db8]

### 前台路由配置
* ![][img_router1]
* ![][img_router2]
* 具体参数参考 [yaf 官方文档][url_yaf] `路由和路由协议设置`
* PS: routes.coupons.map.1= 字段不能省略, 可结合前端 `\web\application\controllers\Error.php` 捕获异常
* ![][img_router3]

### 增加支付方式
* 具体可以参考文件 `\webservice\protected\modules\master\controllers\PaymentController.php` 代码,如下
* ![][img_payment1]
* 可以看到只需要在 `\webservice\protected\include\payment\` 目录增加一个配置文件即可
    - 系统总控 -> 支付总控 -> 安装 -> 启用
    - 站点配置 -> 支付设置 -> 启用
    - 具体操作如下图
* ![][img_payment2]

## 服务器信息相关

### 测试服装网站站点信息
* Fairyseason
    - ip: 10.100.1.207
    - 前台url: www.fairyseason.test.com
    - 后台url: manage.fairyseason.test.com admin 123
    - 前台svn: svn://10.100.1.207/svn-web/web
    - 后台svn: svn://10.100.1.207/svn-admin/webservice
    - redis: `redis-cli -h 10.100.1.207`
    - mongo: `mongo 10.100.1.207/aecmp-cache`
    - mysql: `mysql -h 10.100.1.207 -uroot -paukeys@2016.com` 
* Bellelily
    - ip: 10.100.1.208
    - 前台url: www.bellelily.test.com
    - 后台url: manage.bellelily.test.com admin 123
    - 前台svn: svn://10.100.1.208/svn-web/web
    - 后台svn: svn://10.100.1.208/svn-admin/webservice
    - redis: `redis-cli -h 10.100.1.209`
    - mongo: `mongo 10.100.1.208/aecmp-cache`
    - mysql: `mysql -h 10.100.1.208 -uroot -paukeys@2016.com` 
* Chicgrace 
    - ip: 10.100.1.209
    - 前台url: www.fr.chicgrace.test.com
    - 后台url: manage.fr.chicgrace.test.com admin 123
    - 前台svn: svn://10.100.1.209/svn-web/web
    - 后台svn: svn://10.100.1.209/svn-admin/webservice
    - redis: `redis-cli -h 10.100.1.209`
    - mongo: `mongo 10.100.1.209/aecmp-cache`
    - mysql: `mysql -h 10.100.1.209 -uroot -paukeys@2016.com` 
* Plusinlove 
    - ip: 10.100.1.210
    - 前台url: www.plusinlove.test.com
    - 后台url: manage.plusinlove.test.com admin 123
    - 前台svn: svn://10.100.1.210/svn-web/web
    - 后台svn: svn://10.100.1.210/svn-admin/webservice
    - redis: `redis-cli -h 10.100.1.210`
    - mongo: `mongo 10.100.1.210/aecmp-cache`
    - mysql: `mysql -h 10.100.1.210 -uroot -paukeys@2016.com` 
* Chicgal 
    - ip: 10.100.1.211
    - 前台url: www.chicgal.test.com
    - 后台url: manage.chicgal.test.com admin 123
    - 前台svn: svn://10.100.1.211/svn-web/web
    - 后台svn: svn://10.100.1.211/svn-admin/webservice
    - redis: `redis-cli -h 10.100.1.211`
    - mongo: `mongo 10.100.1.211/aecmp-cache`
    - mysql: `mysql -h 10.100.1.211 -uroot -paukeys@2016.com` 
* Fr.Chicgrace 
    - ip: 10.100.1.213
    - 前台url: www.fr.chicgrace.test.com www.fr.chicgrace.test.com
    - 后台url: manage.fr.chicgrace.test.com admin 123 manage.fr.chicgrace.test.com admin 123
    - 前台svn: svn://10.100.1.213/svn-web/web
    - 后台svn: svn://10.100.1.213/svn-admin/webservice
    - redis: `redis-cli -h 10.100.1.213`
    - mongo: `mongo 10.100.1.213/aecmp-cache`
    - mysql: `mysql -h 10.100.1.213 -uroot -paukeys@2016.com` 
* Pinkclassy 
    - ip: 10.100.1.214
    - 前台url: www.pinkclassy.test.com
    - 后台url: manage.pinkclassy.test.com admin 123
    - 前台svn: svn://10.100.1.214/svn-web/web
    - 后台svn: svn://10.100.1.214/svn-admin/webservice
    - redis: `redis-cli -h 10.100.1.214`
    - mongo: `mongo 10.100.1.214/aecmp-cache`
    - mysql: `mysql -h 10.100.1.214 -uroot -paukeys@2016.com` 
* 管理平台
    - ip: 10.100.1.201
    - svn: svn://10.100.1.201/dress-aukey/
    - mysql:
        + 主: `mysql -h 10.100.1.201 -uroot -paukey_root -Ddress_aukey`
        + 从: `mysql -h 10.100.1.203 -uroot -paukey_root -Ddress_manage`
 
### Host
> 
```
10.100.1.207 manage.fairyseason.test.com
10.100.1.207 www.fairyseason.test.com
10.100.1.208 manage.bellelily.test.com
10.100.1.208 www.bellelily.test.com
10.100.1.209 manage.chicgrace.test.com
10.100.1.209 www.chicgrace.test.com
10.100.1.209 m.chicgrace.test.com
10.100.1.210 manage.plusinlove.test.com
10.100.1.210 www.plusinlove.test.com
10.100.1.211 manage.chicgal.test.com
10.100.1.211 www.chicgal.test.com
10.100.1.213 manage.fr.chicgrace.test.com
10.100.1.213 www.fr.chicgrace.test.com
10.100.1.214 manage.pinkclassy.test.com
10.100.1.214 www.pinkclassy.test.com
10.100.1.201 www.dress-aukey.com
10.100.1.201 www.aukey-api.com
10.100.1.212 pt.myefox.test.com
10.100.1.212 fr.tabouf.test.com
10.100.1.212 de.myefox.test.com
10.100.1.212 it.myefox.test.com
10.100.1.212 fr.myefox.test.com
10.100.1.212 coolmyefox.test.com
10.100.1.212 de.coolmyefox.test.com
10.100.1.212 it.coolmyefox.test.com
10.100.1.212 fr.coolmyefox.test.com
10.100.1.212 es.coolmyefox.test.com
10.100.1.212 pt.coolmyefox.test.com
10.100.1.212 ru.coolmyefox.test.com
10.100.1.212 es.efoxtienda.test.com
10.100.1.212 manage.efoxshop.test.com
```

### Paypal
* 线上环境帐号在对应站点负责人
* 测试环境卖家
    - username :  ak_seller@ak.com
    - password :  ak123456
* 测试环境买家
    - username :  ak_buyer@ak.com
    - password :  ak123456
    
### 前海测试买家帐号
* 卡1：2223000010074471 
    - 年: 2020    
    - 月: 01
    - CVV: 123
* 卡2：376968862623919
    - 年: 2020    
    - 月: 01
    - CVV: 3709




# 几点小建议

# 代码风格
* 目前代码没有统一规范, 推荐 [PHP官方推荐标准 PSR-2][url_psr2]
* 编辑器也没有统一, 有netbeans, phpstorm, sublime, vscode, 而这几个编辑器都支持插件 [editorconfig](http://editorconfig.org/) , 可以统一代码风格
* ![][img_editorconfig]


[url_yaf]: http://www.laruence.com/manual/   "Yaf"
[url_yar]: http://php.net/manual/zh/book.yar.php   "Yar"
[url_yii1]: http://www.yiichina.com/doc/guide/1.1   "yii1.1"
[url_psr2]: https://laravel-china.org/docs/psr/psr-2-coding-style-guide

[url_paypal1]: https://developer.paypal.com/
[url_paypal2]: https://developer.paypal.com/docs/integration/direct/express-checkout/in-context-checkout-overview/
[url_paypal3]: https://developer.paypal.com/docs/api/payments/#definition-transaction
[url_paypal4]: https://demo.paypal.com/c2/demo/navigation?merchant=bigbox&page=shoppingCart&locale.x=en_US&token=EC-7RJ48169DF2838158
[url_paypal5]: https://www.sandbox.paypal.com

[img_db1]: imgs/db1.png
[img_db2]: imgs/db2.png
[img_db3]: imgs/db3.png
[img_db4]: imgs/db4.png
[img_db5]: imgs/db5.png
[img_db6]: imgs/db6.png
[img_db7]: imgs/db7.png
[img_db8]: imgs/db8.png

[img_router1]: imgs/router1.png
[img_router2]: imgs/router2.png
[img_router3]: imgs/router3.png

[img_payment1]: imgs/payment1.png
[img_payment2]: imgs/payment2.gif

[img_coupon1]: imgs/coupon1.png
[img_coupon2]: imgs/coupon2.png
[img_coupon3]: imgs/coupon3.png
[img_coupon4]: imgs/coupon4.png
[img_coupon5]: imgs/coupon5.png
[img_coupon6]: imgs/coupon6.png

[img_editorconfig]: imgs/editorconfig.png




















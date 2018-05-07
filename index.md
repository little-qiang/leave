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
│   │   └── Webservice                   主要用到Cache, 清空对应View静态页面缓存
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
│   │   ├── CacheWebservice.php
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
│   │   └── Webservice.php               Webservice(Yar)请求基类，前台与后台的通信主要走这里，包括数据库CURD
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

## 后台
> 后台采用 [yii1.1框架][url_yii1]

### 目录结构
> 目录结构参考 yii1.1, 目前后台基本没有新功能的开发，几乎都迁移至平台统一管理
> 
> 目前后台代码的核心是 Rpc 接口, 平台推送数据，前后台查看和更新数据都是同个 Rpc 接口
> 
> 接口采用的 PHP官方 [Yar 拓展, 点击查看][url_yar]
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
1. ![][img_dbList1]
2. ![][img_dbList2]
3. ![][img_dbList3]
4. 注意删除表单默认的密码，更新之后需要清除 redis

### 前台路由配置

1. ![][img_router1]
2. ![][img_router2]
3. 具体参数参考 [yaf 官方文档][url_yaf] `路由和路由协议设置`
4. PS: routes.coupons.map.1= 字段不能省略, 可结合前端\web\application\controllers\Error.php 捕获异常
5. ![][img_router3]

## 几点小建议

## 代码风格
- 目前代码没有统一规范, 推荐 [PHP官方推荐标准 PSR-2][url_psr2]
- 编辑器也没有统一, 有netbeans, phpstorm, sublime, vscode, 而这几个编辑器都支持插件 [editorconfig](http://editorconfig.org/) , 可以统一代码风格
- ![][img_editorconfig]


[url_yaf]: http://www.laruence.com/manual/   "Yaf"
[url_yar]: http://php.net/manual/zh/book.yar.php   "Yar"
[url_yii1]: http://www.yiichina.com/doc/guide/1.1   "yii1.1"
[url_psr2]: https://laravel-china.org/docs/psr/psr-2-coding-style-guide
[img_dbList1]: imgs/dbList1.png
[img_dbList2]: imgs/dbList2.png
[img_dbList3]: imgs/dbList3.png
[img_router1]: imgs/router1.png
[img_router2]: imgs/router2.png
[img_router3]: imgs/router3.png
[img_editorconfig]: imgs/editorconfig.png




















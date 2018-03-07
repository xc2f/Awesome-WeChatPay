# **[微信支付开发简介](https://pay.weixin.qq.com/wiki/doc/api/index.html)**
> 作者：秦奋
<br />
> 时间：2018-03-06

## 平台角色
  - 普通商户 
    > 自己开发自己使用，含代金券、现金红包、企业付款功能

  - 服务商
    > 用自己的授权码帮助商户调微信支付接口，进行收钱（[详细](https://www.zhihu.com/question/47965204)），含现金红包功能

  - 银行服务商
    > 自行拓展商户，仅通过微信支付代收商户交易款项，含现金红包、企业付款功能

---

## [支付接入](https://pay.weixin.qq.com/guide/index.shtml)(公众号接入)
  1. 注册公众号（类型须为：服务号、政府或媒体订阅号、企业号）
  2. 认证公众号，认证费：300元/次（有效期一年，到期需重新认证）, [认证方法](http://kf.qq.com/product/weixinmp.html#hid=97)
  3. 申请微信支付, 登录公众平台操作，1~5个工作日
  4. 根据回执商户号在商户平台完成验证
  5. 签署交易协议
  6. 设计开发

---

## 支付开发

### **一、[用户向商户付款](https://pay.weixin.qq.com/wiki/doc/api/index.html)**

  #### 分类
  - 商户扫码
  - 用户扫码
  - 公众号（微信内）
  - H5（微信以外的浏览器）
  - APP
  - 小程序
  - 微信买单（免开发）

  #### 举例：公众号支付
  > 用户通过消息或二维码打开微信网页调起微信支付，如商城

  ##### [设置支付目录和授权域名](https://pay.weixin.qq.com/wiki/doc/api/jsapi.php?chapter=7_3)
  ##### [业务流程](https://pay.weixin.qq.com/wiki/doc/api/jsapi.php?chapter=7_4)<br />![业务流程](./gzhzf.png)
  ##### [接口调用细则](https://pay.weixin.qq.com/wiki/doc/api/jsapi.php?chapter=7_7&index=6)
  
### **二、商户向用户付款**

  #### 分类
  - 代金券或立减优惠
  - 现金红包
  - 企业付款

  #### 举例：企业付款
  > 商户向用户付款，如用户提现

  - [企业付款到用户零钱](https://pay.weixin.qq.com/wiki/doc/api/tools/mch_pay.php?chapter=14_1)

    ##### 开通条件
    1. 商户号已入驻90日
    2. 商户号有30天连续正常交易

    ##### 开通步骤
    1. 在微信公众平台按照相应提示，[申请](https://pay.weixin.qq.com/wiki/doc/api/tools/mch_pay.php?chapter=3_1)相应微信支付模式（审核通过后分配商户号）
    2. 在符合开通条件的情况下登录微信支付商户平台-产品中心，开通企业付款

    ##### 付款方式
    > 企业付款将使用商户的可用余额，需确保可用余额充足

    - [网页端](https://pay.weixin.qq.com/wiki/doc/api/tools/mch_pay.php?chapter=14_1)
    - [接口调用](https://pay.weixin.qq.com/wiki/doc/api/tools/mch_pay.php?chapter=14_2)

    ##### 接口调用规则
    - 给同一个实名用户付款，单笔单日限额2W/2W
    - 不支持给非实名用户打款
    - 一个商户同一日付款总额限额100W
    - 单笔最小金额默认为1元
    - 每个用户每天最多可付款10次，可以在商户平台--API安全进行设置

    ##### [接口调用细则](https://pay.weixin.qq.com/wiki/doc/api/tools/mch_pay.php?chapter=14_2)

    ##### 注意事项
    - 当返回错误码为**SYSTEMERROR**时，一定要使用原单号重试，否则可能造成重复支付等资金风险
    - 接口调用金额单位为**分**，对账金额单位为**元**
    - 标准北京时间，东八区；时间戳取**秒**，10位
    - 订单号唯一，重新发起一笔支付要使用原订单号，避免重复支付；已支付过或已调用关单、撤销的订单号不能重新发起支付
    - [其它](https://pay.weixin.qq.com/wiki/doc/api/tools/mch_pay.php?chapter=4_1)
  - [企业付款到银行卡](https://pay.weixin.qq.com/wiki/doc/api/tools/mch_pay.php?chapter=24_1&index=1)
    > 测试中，后续开放


---
## 结算相关
> 商户给自己的账户充值后，现金管理中的余额可兑换营销资源（代金券、立减优惠、营销规则、现金红包等），也可提现到结算银行账户中

  ### [结算规则、费率、周期说明](http://kf.qq.com/faq/140225MveaUz1504092YFjeM.html)
  - T+1：满足结算条件，则在本日+1（即第二天）结算第一天资金
  - T+7：满足结算条件，前六日的资金则在本日+7（即第八天）结算前六天资金（因账单生成在第七天，是以结算前六天交易资金）

  ### [商户类目对应资质、费率、结算周期](http://kf.qq.com/faq/140225MveaUz1501077rEfqI.html)



## 附
- [微信·公众平台](https://mp.weixin.qq.com/)：用于管理微信公众号（包括订阅号、服务号、企业号），简单说就是微信公众号的后台运营、管理系统
- [微信·开放平台](https://open.weixin.qq.com/)：主要面对移动应用、网站应用开发者、公众号第三方平台，为其提供微信登录、分享、支付等相关权限和服务
- [微信支付·商户平台](https://pay.weixin.qq.com/index.php/core/home/login)：为开通微信支付的商户提供交易查询、支付操作、提现充值等服务

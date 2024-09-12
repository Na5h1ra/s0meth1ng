# URL Schemes & Intent收集与整理

## 更新时间 2024.09.11

## 来源与相关文章：
   酷安[Anywhere-](https://www.coolapk.com/apk/com.absinthe.anywhere_)与[快捷方式](https://www.coolapk.com/apk/com.syyf.quickpay)的评论区

   [小贝塔教程资源导航：安卓软件界面Shell](https://xbta.cc/shell)

   [少数派：入门 iOS 自动化：读懂 URL Schemes](https://sspai.com/post/44591)
   
   [少数派：URL Schemes 使用详解](https://sspai.com/post/31500)
   
   [云端筑梦师的博客：完整参数URL Scheme大全查询](https://www.ydzms.com/archives/58/)

   自己摸索与收集

### 1. 小米系统

可作为磁贴使用，如比较常用的小爱同学

**小米妙播：** 包名`miui.systemui.plugin`，类名`miui.systemui.miplay.MiPlayDetailActivity`

**小米妙享：** 包名`com.milink.service`，类名`com.miui.circulate.world.CirculateWorldActivity`

**小爱同学：** 包名`com.miui.voiceassist`，类名`com.xiaomi.voiceassistant.CTAAlertActivity`，IntentAction为`android.intent.action.ASSIST`

**垃圾清理：** `#Intent;action=miui.intent.action.GARBAGE_CLEANUP;package=com.miui.cleanmaster;end`

**应用数据清理：** `#Intent;component=com.miui.cleanmaster/com.miui.optimizecenter.deepclean.appdata.AppDataActivity;package=com.miui.cleanmaster;S.enter_homepage_way=phone_manage;end`

**原生电池优化界面：** 包名`com.android.settings`，类名`.Settings$HighPowerApplicationsActivity`

**设置默认应用：** 包名`com.android.settings`，类名`.Settings$AdvancedAppsActivity` 或者使用`#Intent;action=android.settings.MANAGE_DEFAULT_APPS_SETTINGS;package=com.android.settings;component=com.android.settings/.Settings%24AdvancedAppsActivity;end`

**小米社区 每日积分签到：** `mio://web.vip.miui.com/page/info/mio/mio/checkIn?ref=longpressshortcuts`

### 2. 支付宝 `com.eg.android.AlipayGphone`
  常用小程序一般为`alipays://platformapi/startapp?appId=数字`
  
  可能后面会跟一些参数

  或是扫一扫`alipayqr://platformapi/startapp?saId=10000007&qrcode=淘宝或支付宝相关的网址`，比如下面的快递取件码

  #### 数字来源1：
  小程序若能分享，则右上角分享出去，得到链接后，在浏览器里打开，得到一串网址后，使用URLdecode解码后可得到appid（通用方法）

  #### 数字来源2：
  小程序若不能分享，且设备能root，可去`/data/data/com.eg.android.AlipayGphone/files/nebulaInstallApps/`路径下，打开每个文件夹里的Manifest.xml（可得到名称和数字），或去查看`/data/data/com.eg.android.AlipayGphone/databases/nebulax_app.db`数据库文件（2021年8月尝试有效，现可能已经失效）
  
  #### 数字来源3：
  他人的分享，比如上面的来源与相关文章

  #### 常用：
|名称|URL Schemes|
|-------------|-------------|
|扫一扫|alipays://platformapi/startapp?appId=10000007|
|付钱/收钱|alipays://platformapi/startapp?appId=20000056|
|出行|alipays://platformapi/startapp?appId=20002047|
|付款码|alipays://platformapi/startapp?appId=20000056|
|收款码|alipays://platformapi/startapp?appId=20000123|
|乘车码|alipays://platformapi/startapp?appId=200011235|
|Apple专区|alipays://platformapi/startapp?appId=2021003125614874&page=pages/index/index|
|快递取件码|alipayqr://platformapi/startapp?saId=10000007&qrcode=https://market.m.taobao.com/app/cn-yz/multi-activity/authCode.html?needStartTake=true&packageId=null&entrance=logisticDetail|
|花呗|alipays://platformapi/startapp?appId=20000199|
|神奇海洋|alipays://platformapi/startapp?appId=2021003115672468|
|蚂蚁森林|alipays://platformapi/startapp?appId=60000002|
|滴滴出行|alipays://platformapi/startapp?appId=2019062865745088|
|车来了|alipays://platformapi/startapp?appId=2019110768932964|
|高德实时公交|alipays://platformapi/startapp?appId=2018051660134749|
|铁路12306|alipays://platformapi/startapp?appId=2018122062695048|
|会员领积分|alipays://platformapi/startapp?appId=20000160&url=%2Fwww%2FmyPoints.html|
|市民中心|alipays://platformapi/startapp?appId=20000178|
|菜鸟裹裹|alipays://platformapi/startapp?appId=2021001141626787|
|运动|alipays://platformapi/startapp?appId=20000869|
|饿了么|alipays://platformapi/startapp?appId=2021001110676437|
|口碑|alipays://platformapi/startapp?appId=2021001108603619|
|酒店出行|alipays://platformapi/startapp?appId=2021001111632299|
|电影演出|alipays://platformapi/startapp?appId=2021001110648550|
|红包|alipays://platformapi/startapp?appId=88886666|
|话费充值|alipays://platformapi/startapp?appId=10000003|
|PockytShop 礼品卡充值(慎用)|alipays://platformapi/startapp?appId=2021003191605547|


### 3. 淘宝 `com.taobao.taobao`
|名称|URL Schemes|
|-------------|-------------|
|淘宝一键价保|tbopen://m.taobao.com/tbopen/index.html?h5Url=https%3A%2F%2Fpages.tmall.com%2Fwow%2Fz%2Fmarketing-tools%2Fmkt%2Fprice-center%3FdisableNav%3DYES%26sourceChannel%3D2%26spm%3Da311a.7996332.0.0&action=ali.open.nav&module=h5&bootImage=0&afcPromotionOpen=false|
|淘宝 快递身份码|taobao://market.m.taobao.com/app/cn-yz/multi-activity/authCode.html?needStartTake=true&packageId=null&entrance=logisticDetail|
|淘宝人生|taobao://pages.tmall.com/wow/z/tblife/solution2/game-tblife?wh_biz=tm&disableNav=YES&uniqueTag=hdtblife&from=mytaobaoqd#/home|
|淘宝店铺的跳转|taobao://shop.m.taobao.com/shop/shop_index.htm?shopId=店铺数字id|


### 4. 网易云音乐 `com.netease.cloudmusic`
|名称|URL Schemes|
|-------------|-------------|
|网易云榜单|orpheus://ranking|
|网易云歌曲跳转|orpheus://song/一串数字 （分享出来的song?id=后面的数字）|
|网易云签到|orpheus://rnpage?component=rn-cloudshell-center|
|网易云音乐 每日推荐|orpheus://songrcmd|
|网易云音乐 听歌识曲|orpheus://identify（iOS版本为orpheuswidget://recognize）|
|网易云音乐 我喜欢的音乐|orpheus://playlist/417760994|
|网易云音乐 私人雷达|orpheus://playlist/3136952023|
|网易云音乐 私人FM|orpheus://radio|

### 5. QQ音乐 `com.tencent.qqmusic`
|名称|URL Schemes|
|-------------|-------------|
|每日30首|qqmusic://qq.com/ui/gedan?p={"id":"4487164108"}|
|我的收藏|qqmusic://qq.com/ui/myTab?p=%7B%22tab%22%3A%22fav%22%7D|
|听歌识曲|qqmusic://qq.com/ui/recognize|

### 6. 京东 `com.jingdong.app.mall`

常用命令openapp.jdmobile://virtual?params={"category":"jump","des":"m","url":"网址"}

|名称|URL Schemes|
|-------------|-------------|
|京东一键价保|openapp.jdmobile://virtual?params={"category":"jump","des":"m","url":"https://h5.m.jd.com/babelDiy/Zeus/2RePMzTqg6UoffvMwtwVeMcnPGeg/index.html?defaultViewTab=0&appId=cuser&type=25#/"}
|京东一键价保2(瞎折腾试出来的，慎用)|openapp.jdmobile://virtual?params={"category":"jump","des":"m","url":"https://h5.m.jd.com/pb/016454810"}
|京东一键价保3(瞎折腾试出来的，慎用)|openapp.jdmobile://virtual?params={"category":"jump","des":"m","url":"https://h5.m.jd.com/pb/016454811"}
|领签到的京豆|openapp.jdmobile://virtual?params={"category":"jump","des":"m","url":"https://bean.m.jd.com"}
|白条账单|openapp.jdmobile://virtual?params={"category":"jump","des":"m","url":"https://m.jr.jd.com/rn/BTMonthBill/index.html?page=page_bill_page&monthlyBillType=0&channelName=&channelcode=Z01"}
|订单列表|openapp.jdmobile://virtual?params={"category":"jump","des":"orderlist"}|

### 7. 高德地图 `com.autonavi.minimap`
|名称|URL Schemes|
|-------------|-------------|
|实时公交|amapuri://realtimeBus/home?from=shortcut&netAcc={"path":"amapservice://amap_bundle_realbus/RequestScheduleService","requestKeys":"busStation"}|
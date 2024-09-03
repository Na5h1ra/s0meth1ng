# URL Schemes 收集与整理

## 更新时间 2024.09.03
## 来源与相关文章：
   酷安[Anywhere-](https://www.coolapk.com/apk/com.absinthe.anywhere_)与[快捷方式](https://www.coolapk.com/apk/com.syyf.quickpay)的评论区

   [小贝塔教程资源导航：安卓软件界面Shell](https://xbta.cc/shell)

   [少数派：入门 iOS 自动化：读懂 URL Schemes](https://sspai.com/post/44591)
   
   [少数派：URL Schemes 使用详解](https://sspai.com/post/31500)
   
   [云端筑梦师的博客：完整参数URL Scheme大全查询](https://www.ydzms.com/archives/58/)

   自己摸索与收集

### 支付宝 com.eg.android.AlipayGphone
  常用小程序一般为alipays://platformapi/startapp?appId=数字

  可能后面会跟一些参数

  #### 数字来源1：
  小程序若能分享，则右上角分享出去，得到链接后，在浏览器里打开，得到一串网址后，使用URLdecode解码后可得到appid（通用方法）

  #### 数字来源2：
  小程序若不能分享，且手机能root，可去/data/data/com.eg.android.AlipayGphone/files/nebulaInstallApps/下，打开每个文件夹里的Manifest.xml（可得到名称和数字），或去查看/data/data/com.eg.android.AlipayGphone/databases/nebulax_app.db数据库文件（2021年8月尝试有效，现可能已经失效）
  
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
|乘车码|alipayqr://platformapi/startapp?saId=200011235|
|花呗|alipays://platformapi/startapp?appId=20000199|
|神奇海洋|alipays://platformapi/startapp?appId=2021003115672468|
|蚂蚁森林|alipays://platformapi/startapp?appId=60000002|
|滴滴出行|alipays://platformapi/startapp?appId=2019062865745088|
|车来了|alipays://platformapi/startapp?appId=2019110768932964|
|高德实时公交|alipays://platformapi/startapp?appId=2018051660134749|
|铁路12306|alipays://platformapi/startapp?appId=2018122062695048|
|会员领积分|alipays://platformapi/startapp?appId=20000160&url=%2Fwww%2FmyPoints.html|
|市民中心|alipays://platformapi/startapp?appId=20000178|
|苹果专区|alipays://platformapi/startapp?appId=20000042&publicId=2017011104987367|
|菜鸟裹裹|alipays://platformapi/startapp?appId=2021001141626787|
|运动|alipays://platformapi/startapp?appId=20000869|
|饿了么|alipays://platformapi/startapp?appId=2021001110676437|
|口碑|alipays://platformapi/startapp?appId=2021001108603619|
|酒店出行|alipays://platformapi/startapp?appId=2021001111632299|
|电影演出|alipays://platformapi/startapp?appId=2021001110648550|
|红包|alipays://platformapi/startapp?appId=88886666|
|话费充值|alipays://platformapi/startapp?appId=10000003|

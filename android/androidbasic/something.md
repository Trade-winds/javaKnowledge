1、联网框架搭建：
	1、封装Retrofit：在Retrofit基础上增加线程控制回调，增加Api返回值统一泛型封装，Retrofit、OKHttpClient对象的统一单例管理，OKHttpClient通过增加	 Interceptor实现链接访问和返回双阶段的实时监控及控制，增加Stetho插件实现在chrome中对app联网及本地数据的检控。
	2、封装Volly和AsyncHttpClient：实现联网引擎，通过工厂模式实现对Volly和AsyncHttpClient的自选调用（避开Volly对文件处理的劣势），统一封装线程控	 制回调及异常处理，通过Map和List对Api对象进行统一的 存储、销毁、cancel操作。
	3、HttpClient和URLConnection的直接封装：通过List及线程池来控制所有异步请求对象的存储和分发，通过泛型控制返回值的解析。

2、图片处理框架的搭建:
	1、封装ImageLoader：在ImagLoader基础上通过单例控制ImageLoader对象，增加圆角图片及指定尺寸图片的封装，增加Option对象的统一控制，增加加载动画		 的控制。
	2、封装glide：增加glide对象的统一管理，增加图片访问链接中图片尺寸参数的指定
	3、手写图片处理：实现三级缓存机制，通过Map集合（pool）以链接网址为键实现bitmap的内存存储和本地文件存储，对图片进行BitmapFactory的尺寸压缩和R	 GB方式的质量压缩以避免OOM，增加内存和磁盘缓存的LRU算法以进行缓存空间大小控制。

3、数据库框架搭建：
	1、封装Realm：在Realm基础上增加线程控制回调。因为Realm对搜索结果的线程使用规定过于死板，且搜索结果Bean不能继承Clonesable（除RealmObject都不		行），所以只能进行手动的结果复制来保证可以跨线程使用。所以，即使Realm有强大的数据表监听机制，和通过搜索结果直接修改数据表等强大新颖的功能		，但整体使用不够优雅、灵活。
	2、手写SqlLite工具：通过类的属性反射建表，字段属性支持全基础类型，建表时实现懒加载，通过自定义注解和反射对数据库进行升级。

4、数据总线框架搭建：
	1、EventBus的使用。
	2、手写全局回调对象：通过维护一个全局的Map<Class,List>来统一存储全局的回调对象，以对象的Class为键在Map中找到全局中所有的回调对象进行统一的回	 调方法执行，以实现广播机制
	3、广播机制：因为国产某些定制手机对广播机制进行了阉割，所以广播机制不怎么可靠

5、APP架构：
  1、MVP架构：将通用的工具及基类放入Library，在app包内根据不同业务功能模块分包，每个功能模块中再分为Model、View、Presenter模块进行业务功能代码解耦。
  2、RxJava：熟悉，并在尝试使用中。
  3、MVC架构：不够优雅且难扩展，已废弃。

6、Activity、Fragment管理：
	1、Activity管理：模仿安卓系统对Activity的维护方式来维护一个全局的Stack，在基类的Oncreate和OnDestroy中对Stack进行增删操作，易于调用和监控App		中所有Activity。
	2、Fragment管理：通过综合OnResume、OnPause和setUserVisibleHint监控Fragment的准确显隐。

7、熟悉并可以快速集成各种第三方SDK功能及功能性框架。

8、熟练掌握安卓原生及内嵌网页数据互通。

9、熟练掌握各种安卓内存优化方案。

10、熟练使用MaterialDesign控件及RecyclerView等新兴控件。

11、熟悉并已初步掌握ReactNatie的使用以实现APP混合跨平台开发。



- Android中View的UI事件是自顶向下传播的;每棵控件树中,都会有一个`andorid.view.ViewParent`与其根空间绑定,该`ViewParent`对象是正棵控件树中**交互事件的控制枢纽**,它会负责将用户操作产生的交互事件传递到控件树的根控件,进而自顶向下进行传播;控件树中的每个控件对象,都会包含指向该`ViewParent`对象的指针,当子控件对象的焦点、尺寸等控件属性发生改变时,会通知该控件树的`ViewParent`对象,由`ViewParent`对象统一向下分发该事件;

- `View`中的**事件函数的返回值**是控制事件传播的重要手段.如果该事件返回`true`,则说明该控件已经接收并完成了该事件的处理,无需将该事件进一步传播;反之,如果事件返回`false`,则说明该控件对象未能处理该事件(或虽然做过处理,但仍需要进一步处理),需要继续传递以寻找能够处理它的控件对象.

- `Android`应用的打包过程是：资源文件（包括数据类型资源文件和值类型资源文件）经appt(andorid application package tool)进行预编译后生成`R`文件，然后和其他jar包和类经SDK编译後生成class.dex文件，然后再和资源文件以及**App._ap** 来生成 android apk文件

- `R`文件中的每个常量都是32位的整型数值，高8位代表**资源包**的信息，次高8位代表的是**资源类型**，低16位代表的是**资源项的索引信息**，那么一个应用中最多包含256个资源包，每个资源包中最多有256中资源类型，每种类型下最多有65536个资源

- Android系统提供的应用资源放置在android包中，对应的R类为`android.R`
```java
final Resources resources = getResources();
XmlResourceParse layout = resources.getLayout(android.R.layout.simple_list_item_2);
```

- 通过`android.view.LayoutInflater`类，可以将任意的layout资源文件实例化成一个资源对象

- android 中的资源文件中，若一个资源文件的名称是另外一个资源名称+“." + 名称，那么即使这个资源文件没有显式使用`parent`来声明，该资源依然是继承自另外一个资源

- 应用运行时，图形或图像资源都会被加载成一个`android.graphics.drawable.Drawable`对象,每个动画资源文件都可以加载成为`android.view.animation.Animation`对象

- android 文件系统中，`system`系统目录，放置android运行所需要的核心库;`data`用来保存应用安装包和运行时产生的数据;`sdcard`扩展存储卡目录，用来存放应用能共享的数据;`mnt`记录Android挂载的外部存储信息

- 在Android中，第三方应用及其数据，都存放在data目录下;其中，应用安装包会被存放到`/data/app/`目录下，每个安装包的文件名都形如：应用包名.apk，以避免重复

- 在Android中，应用的安装，就是将应用的安装包原封不动地拷贝到`data/app/`目录下（当然，此过程需要进行权限校验和用户确认）。每个Android的应用安装包本质上就是一个zip格式的压缩文件，通过这种方式安装，可以最大程度地节约宝贵的只读存储空间

- Android的每个应用，都会在/data/data/目录下创建一个与安装包同名的应用数据目录，用来存放运行数据，即应用数据目录为：**`/data/data/应用包名`/**，例如数据库测存放目录为**`/data/data/应用包名`/databases`**

- Andorid中数据库一般使用`android.database.sqlite.SQLiteOpenHelper`类，该类中封装了一个`SqliteDatabase`对象，可以通过‘SQLiteOpenHelper.getReadalbe-Database’来获取可读数据库对象，通过`SQLiteOpenHelper.getWriteableDatabase`来获取一个可读写的数据库对象  

- `SingleTask`模式是先寻找当前`activity`需要的任务栈（一般都是默认的任务栈），再判断该任务栈中是否已经存在该`activity`，如果已经存在，那么就不在从新创建；并且`SingleTask`模式具有`cleanTop`的作用，即如果栈中存在该`activity`，并且不是在栈顶位置，那么就会把位于该`activity`之上的其他`activity`全部清除出栈  

- `intent-filter`的匹配规则有`action`,`category`,`data`,一个`Activity`可以有多个`intent-filter`,一个`intent`只有能匹配任何一组`intent-filter`即可启动对应的`Activity`,并且要同时匹配一组`intent-filter`列表中的`action`,`category`,`data`信息，也就是说只有一个`Intent`同时匹配`action`类别,`category`类别,`data`类别才能算完全匹配  

- 对于`action`的匹配规则，一个过滤规则中（即一个`intent-filter`中）可以有多个`action`,那么只要`Intent`中的`action`和过滤规则中的任何一个`action`相同即可匹配成功(**注意：一个`Intent`只可以设置一个`action`,通过`setaction()`来设置**)，另外，`action`区分大小写，大小写不同字符串相同的`action`会匹配失败;需要注意的是，`Intent`中如果没有指定`action`，那么匹配失败

- 对于`category`的匹配规则，`Intent`可以设置多个`category`，要求所设置的`category`都必须匹配`intent-filter`其中一个`category`，即必须满足`Intent`中的`category`是`intent-filter`中的`category`的子集，并且如果`Intent`没有设置`category`,也能匹配`intent-filter`,这是因为系统在调用`startActivity`或者`startActivityForResult`方法时，会默认给`Intent`加上`android.intent. category.DEFAULT`这个`category`，同时，为了我们的`activity`能够接收隐式调用，就必须在`intent-filter`中指定`android.intent.category.DEFAULT`这个`category`  

- `data`的匹配规则和`action`类似，如果过滤规则中定义了`data`，那么`Intent`中必须也要定义可匹配的`data`，`data`由两部分组成，`mimeType`和`URI`，`mimeType`指媒体类型，`URI`的结构：
` <scheme>://<host>:<port>/[<path>|<pathPrefix>|<pathPattern>]`  

- 如果要为`Intent`指定完整的`data`，必须要调用`setDataAndType`方法，不能先调用`setData`再调用`setType`，因为这两个方法彼此会清除对方的值  

- 当我们通过隐式方式启动一个`Activity`的时候，可以做一下判断，看是否有`Activity`能够匹配我们的隐式`Intent`，如果不做判断就有可能出现上述的错误了。判断方法有两种：采用`PackageManager`的`resolveActivity`方法或者`Intent`的`resolveActivity`方法，如果它们找不到匹配的`Activity`就会返回null，我们通过判断返回值就可以规避上述错误了。另外，`PackageManager`还提供了`queryIntentActivities`方法，这个方法和`resolveActivity`方法不同的是：它不是返回最佳匹配的`Activity`信息而是返回所有成功匹配的`Activity`信息

- 通过给四大组件指定`android:process`属性，可以在Android中开启多进程，这也是在Android中使用多进程的**唯一方法**

- 对于给`Activity`指定`android:process`进程名，进程名以“:”开头的进程属于当前应用的私有进程，其他应用的组件不可以和它跑在同一个进程中，而进程名不以“:”开头的进程属于全局进程，其他应用通过`ShareUID`方式可以和它跑在同一个进程中

- 在Android中，系统会为每个应用分配一个独立的虚拟机，也就是为每个进程分配一个独立的虚拟机

- 在Android中使用多进程会造成如下一些问题：1、静态成员和单利模式完全失效 2、线程同步机制完全失效 3、`SharedPreferences`的可靠性下降（这是因为`SharedPreferences`不支持两个进程同时进行写操作，否则会导致一定的概率丢失数据，`SharedPreferences`底层是对xml文件进行读写的） 4、`Application`会多次创建  

- 静态成员属于类而不属于对象，是不能序列化和反序列化的；使用`transient`关键字标记的成员变量不参与序列化  

- 

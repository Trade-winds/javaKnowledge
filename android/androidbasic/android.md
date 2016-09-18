

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
- 

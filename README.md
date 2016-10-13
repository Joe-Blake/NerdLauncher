# NerdLauncher
PackageItemInfo类
说明： AndroidManifest.xml文件中所有节点的基类，提供了这些节点的基本信息：a label、icon、 meta-data。它并不
直接使用，而是由子类继承然后调用相应方法。
常用字段：
public int icon           获得该资源图片在R文件中的值 (对应于android:icon属性)
public int labelRes     获得该label在R文件中的值(对应于android:label属性)
public String name   获得该节点的name值 (对应于android:name属性)
public String packagename   获得该应用程序的包名 (对应于android：packagename属性)
常用方法：
Drawable  loadIcon(PackageManager pm)               获得当前应用程序的图像
CharSequence  loadLabel(PackageManager pm)     获得当前应用程序的label

ActivityInfo类  继承自 PackageItemInfo
说明： 获得应用程序中<activity/>或者 <receiver />节点的信息 。我们可以通过它来获取我们设置的任何属性，包括
theme 、launchMode、launchmode等
常用方法继承至PackageItemInfo类中的loadIcon()和loadLabel() 

ServiceInfo 类
说明： 同ActivityInfo类似 ，同样继承自 PackageItemInfo，只不过它表示的是<service>节点信息。

ApplicationInfo类 继承自  PackageItemInfo
说明：获取一个特定引用程序中<application>节点的信息。
字段说明：
　　　   flags字段： FLAG_SYSTEM　系统应用程序
　　　　　             　FLAG_EXTERNAL_STORAGE　表示该应用安装在sdcard中
常用方法继承至PackageItemInfo类中的loadIcon()和loadLabel()

ResolveInfo类
说明：根据<intent>节点来获取其上一层目录的信息，通常是<activity>、<receiver>、<service>节点信息。
常用字段：
public  ActivityInfo  activityInfo     获取 ActivityInfo对象，即<activity>或<receiver >节点信息
public ServiceInfo   serviceInfo     获取 ServiceInfo对象，即<service>节点信息
常用方法： 
Drawable loadIcon(PackageManager pm)             获得当前应用程序的图像
CharSequence loadLabel(PackageManager pm)  获得当前应用程序的label

PackageInfo类
说明：手动获取AndroidManifest.xml文件的信息 。
常用字段：
public String    packageName                   包名
public ActivityInfo[]     activities                   所有<activity>节点信息
public ApplicationInfo applicationInfo       <application>节点信息，只有一个
public ActivityInfo[]    receivers                  所有<receiver>节点信息，多个
public ServiceInfo[]    services                  所有<service>节点信息 ，多个

PackageManger 类
说明： 获得已安装的应用程序信息 。可以通过getPackageManager()方法获得。
常用方法：
public abstract PackageManager  getPackageManager()   
功能：获得一个PackageManger对象
public abstrac  tDrawable    getApplicationIcon(StringpackageName)
参数： packageName 包名
功能：返回给定包名的图标，否则返回null

public abstract ApplicationInfo   getApplicationInfo(String packageName, int flags)

参数：packagename 包名
flags 该ApplicationInfo是此flags标记，通常可以直接赋予常数0即可
功能：返回该ApplicationInfo对象

public abstract List<ApplicationInfo>  getInstalledApplications(int flags)
参数：flag为一般为GET_UNINSTALLED_PACKAGES，那么此时会返回所有ApplicationInfo。我们可以对ApplicationInfo
的flags过滤,得到我们需要的。
功能：返回给定条件的所有PackageInfo

public abstract List<PackageInfo>  getInstalledPackages(int flags) 
参数如上
功能：返回给定条件的所有PackageInfo

public abstractResolveInfo  resolveActivity(Intent intent, int flags)
参数：  intent 查寻条件，Activity所配置的action和category
flags： MATCH_DEFAULT_ONLY    ：Category必须带有CATEGORY_DEFAULT的Activity，才匹配
GET_INTENT_FILTERS         ：匹配Intent条件即可
GET_RESOLVED_FILTER    ：匹配Intent条件即可
功能 ：返回给定条件的ResolveInfo对象(本质上是Activity) 

public abstract  List<ResolveInfo>  queryIntentActivities(Intent intent, int flags)
参数同上
功能 ：返回给定条件的所有ResolveInfo对象(本质上是Activity)，集合对象

public abstract ResolveInfo  resolveService(Intent intent, int flags)
参数同上
功能 ：返回给定条件的ResolveInfo对象(本质上是Service)

public abstract List<ResolveInfo> queryIntentServices(Intent intent, int flags)
参数同上
功能 ：返回给定条件的所有ResolveInfo对象(本质上是Service)，集合对象
# 最火Android开源项目SystemBarTint使用
---
开源地址：[https://github.com/open-android/SystemBarTint](https://github.com/open-android/SystemBarTint "开源项目地址")

修改状态栏颜色，可保持与actionbar 一致


# 运行效果
![](http://i.imgur.com/POLvAit.png)   ![](http://i.imgur.com/nekUev1.png)



* 爱生活,爱学习,更爱做代码的搬运工,分类查找更方便请下载黑马助手app

![黑马助手.png](http://upload-images.jianshu.io/upload_images/4037105-f777f1214328dcc4.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


## 使用步骤

### 1. 在project的build.gradle添加如下代码(如下图)

	allprojects {
	    repositories {
	        ...
	        maven { url "https://jitpack.io" }
	    }
	}

![](http://oi5nqn6ce.bkt.clouddn.com/itheima/booster/code/jitpack.png)


### 2. 在Module的build.gradle添加依赖

    compile 'com.github.open-android:SystemBarTint:v1.0.0'


### 3. 复制如下代码到xml

	<ScrollView xmlns:android="http://schemas.android.com/apk/res/android"
            android:layout_width="match_parent"
            android:layout_height="match_parent"
            android:fitsSystemWindows="true">
	    <TextView
	        android:padding="16dp"
	        android:textSize="18sp"
	        android:layout_width="wrap_content"
	        android:layout_height="wrap_content"
	        android:text="@string/ipsum"/>
	</ScrollView>


### 4. 拷贝以下内容到 res/string.xml中

> 也可以自己定义自己的字符串。

		<string name="ipsum">Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nam ligula sapien, fermentum vitae aliquam sed, lacinia in nibh. Pellentesque euismod diam eget justo interdum, sit amet elementum ipsum vulputate. Aliquam sed purus urna. Vivamus luctus nisi sem, a fringilla velit iaculis id. Donec nec vulputate justo. Fusce vulputate sodales tellus, in fringilla ante posuere non. Vivamus vulputate nisl non augue dignissim, consectetur rutrum risus facilisis. Sed consectetur aliquam dolor, sed pulvinar mi tristique vitae. Donec quis ligula quis velit consequat dictum id eu felis. Mauris ac congue ante, sed elementum eros.\n\nSed eu euismod dolor, a vestibulum lorem. Phasellus euismod volutpat risus sit amet pellentesque.  Proin sed massa eget risus malesuada dignissim et in ipsum..\n\nNullam risus felis, dictum et varius eget, rutrum non nunc. Vestibulum lorem nulla, porttitor ac sapien interdum, porta tristique turpis. Quisque ut dui vitae urna congue scelerisque. Nulla eu commodo felis. Nulla aliquam magna a arcu elementum, vitae tincidunt risus semper. Sed consectetur diam vel magna mattis, sed congue nisi fringilla. Ut in facilisis elit. Etiam aliquet orci urna. Nam interdum nunc fringilla iaculis cursus.</string>

### 5. 拷贝以下内容到 res/color.xml中

> 也可以自己定义颜色。

	    <color name="actionbar_bg">#FF0099EE</color>
    	<color name="statusbar_bg">#FF0099cc</color>

### 6. 拷贝以下内容到res/style.xml 中

		    <style name="ActionBarTheme" parent="android:Theme.Holo.Light.DarkActionBar">
		        <item name="android:actionBarStyle">@style/ActionBarStyle</item>
		    </style>
		
		    <style name="ActionBarStyle" parent="android:Widget.Holo.Light.ActionBar.Solid.Inverse">
		        <item name="android:background">@color/actionbar_bg</item>
		    </style>

###7. 拷贝以下内容到activity中

		@Override
	    protected void onCreate(Bundle savedInstanceState) {
	        super.onCreate(savedInstanceState);
	        setContentView(R.layout.activity_main);
	
	        if (Build.VERSION.SDK_INT >= Build.VERSION_CODES.KITKAT) {
	            setTranslucentStatus(true);
	        }
	
	        SystemBarTintManager tintManager = new SystemBarTintManager(this);
	        tintManager.setStatusBarTintEnabled(true);
	        //设置状态栏颜色
	        tintManager.setStatusBarTintResource(R.color.statusbar_bg);
	
	    }
	
	    @TargetApi(19)
	    private void setTranslucentStatus(boolean on) {
	        Window win = getWindow();
	        WindowManager.LayoutParams winParams = win.getAttributes();
	        final int bits = WindowManager.LayoutParams.FLAG_TRANSLUCENT_STATUS;
	        if (on) {
	            winParams.flags |= bits;
	        } else {
	            winParams.flags &= ~bits;
	        }
	        win.setAttributes(winParams);
	    }

###8 . 注册activity的时候，请指定主题样式为之前定义的主题

		  
        <activity android:name=".MainActivity"
            android:theme="@style/ActionBarTheme">
            <intent-filter>
                <action android:name="android.intent.action.MAIN"/>

                <category android:name="android.intent.category.LAUNCHER"/>
            </intent-filter>
        </activity>
        
* 注意细节

	1. 如果想实现上面右图效果，呈现透明色状态栏的。只需要修改布局的根标签的fitsSystemWindows 为false，并且搭配透明的颜色即可。

				<ScrollView xmlns:android="http://schemas.android.com/apk/res/android"
	            android:layout_width="match_parent"
	            android:layout_height="match_parent"
	            android:fitsSystemWindows="false"> //此处修改为false

	2. 配合透明颜色即可

			  <color name="actionbar_bg">#330000ff</color>
	    	  <color name="statusbar_bg">#33ff0000</color>


* 详细的使用方法在DEMO里面都演示啦,如果你觉得这个库还不错,请赏我一颗star吧~~~

* 欢迎关注微信公众号

![](http://upload-images.jianshu.io/upload_images/4037105-8f737b5104dd0b5d.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

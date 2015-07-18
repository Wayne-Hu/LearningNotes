# Android Development
## Menu

## Application Framework
* **Activity Manager** − Controls all aspects of the application lifecycle and activity stack.
* **Content Providers** − Allows applications to publish and share data with other applications.
* **Resource Manager** − Provides access to non-code embedded resources such as strings, color settings and user interface layouts.
* **Notifications Manager** − Allows applications to display alerts and notifications to the user.
* **View System** − An extensible set of views used to create application user interfaces.

## Application Components
Components             | Description
----------------------:|:-----------------------------------------------------------------
**Activities**         |They dictate the UI and handle the user interaction to the smart phone screen
**Services**           |They handle background processing associated with an application.
**Broadcast Receivers**|They handle communication between Android OS and applications.
**Content Providers**  |They handle data and database management issues.

### Activities
Activity performs actions on the screen.
An activity is implemented as a subclass of Activity.
![Activity](http://www.tutorialspoint.com/android/images/activity.jpg)

Callback     | Description
------------:|------------------------------------------------
onCreate()   |This is the first callback and called when the activity is first created.
onStart()    |This callback is called when the activity becomes visible to the user.
onResume()   |This is called when the user starts interacting with the application.
onPause()    |The paused activity does not receive user input and cannot execute any code and called when the current activity is being paused and the previous activity is being resumed.
onStop()     |This callback is called when the activity is no longer visible.
onDestroy()  |This callback is called before the activity is destroyed by the system.
onRestart()  |This callback is called when the activity restarts after stopping it.

### Services
A service is a component that runs in the background to perform long-running operations. 
A service is implemented as a subclass of Service class.

### Broadcast Receivers
Broadcast Receivers simply respond to broadcast messages from other applications or from the system.
A broadcast receiver is implemented as a subclass of BroadcastReceiver class and ==each message is broadcaster as an Intent object==.

### Content Providers
A content provider component supplies data from one application to others on request. 
A content provider is implemented as a subclass of ContentProvider class and must implement a standard set of APIs that enable other applications to perform transactions.

## Access Resources
* 访问图片

```java
ImageView imageView = (ImageView) findViewById(R.id.myimageview);
imageView.setImageResource(R.drawable.myimage);
```

* 访问字符串

```xml
<?xml version="1.0" encoding="utf-8"?>
<resources>
    <string  name="hello">Hello, World!</string>
</resources>
```

```java
TextView msgTextView = (TextView) findViewById(R.id.msg);
msgTextView.setText(R.string.hello);
```

* 访问layout

```java
public void onCreate(Bundle savedInstanceState) {
   super.onCreate(savedInstanceState);
   setContentView(R.layout.main_activity);
}
```

* 在XML文件中访问资源

```xml
<?xml version="1.0" encoding="utf-8"?>
<resources>
   <color name="opaque_red">#f00</color>
   <string name="hello">Hello!</string>
</resources>

<?xml version="1.0" encoding="utf-8"?>
<EditText xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="fill_parent"
    android:layout_height="fill_parent"
    android:textColor="@color/opaque_red"
    android:text="@string/hello" />
```
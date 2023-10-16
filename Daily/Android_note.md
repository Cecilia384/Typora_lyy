

（掌握虚拟机api
### 9.21

- [x] #todo Android调试，能在虚拟机上面输出Hello World
- [ ] #todo 配置OpenGLRenderer

这个算运行成功嘛AWA(跑了五分钟啊，感觉电脑cpu要炸了)

![[Pasted image 20230921142950.png]]



原始xml
```xml
<?xml version="1.0" encoding="utf-8"?>  
<androidx.constraintlayout.widget.ConstraintLayout xmlns:android="http://schemas.android.com/apk/res/android"  
    xmlns:app="http://schemas.android.com/apk/res-auto"  
    xmlns:tools="http://schemas.android.com/tools"  
    android:layout_width="match_parent"  
    android:layout_height="match_parent"  
    tools:context=".MainActivity">  
  
    <TextView  
        android:id="@+id/textView2"  
        android:layout_width="wrap_content"  
        android:layout_height="wrap_content"  
        android:text="@string/hello_world_nhello_cecilia"  
        app:layout_constraintBottom_toBottomOf="parent"  
        app:layout_constraintEnd_toEndOf="parent"  
        app:layout_constraintStart_toStartOf="parent"  
        app:layout_constraintTop_toTopOf="parent"  
        app:layout_constraintVertical_bias="0.393" />  
    </androidx.constraintlayout.widget.ConstraintLayout>
```

书上代码1
```xml
<?xml version="1.0" encoding="utf-8"?>  
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"  
  
    xmlns:tools="http://schemas.android.com/tools"  
    android:layout_width="match_parent"  
    android:layout_height="match_parent"  
    android:layout_gravity="center"  
    android:orientation="vertical">  
  
    <TextView  
  
        android:layout_width="wrap_content"  
        android:layout_height="wrap_content"  
        android:layout_padding="24dp"  
        android:text="question_text" />  
  
    <LinearLayout  
        android:layout_width="wrap_content"  
        android:layout_height="wrap_content"  
        android:orientation="horizontal">  
  
        <Button  
            android:layout_width="wrap_content"  
            android:layout_height="wrap_content"  
            android:text="True"/>  
  
        <Button  
            android:layout_width="wrap_content"  
            android:layout_height="wrap_content"  
            android:text="@string/false" />  
  
    </LinearLayout>  
  
  
</LinearLayout>
```



#坑 为什么更新了xml文件之后，重新运行虚拟机上的安卓程序没有相应更新

- [解决xml中修改内容，运行在手机上没效果问题](https://www.jianshu.com/p/333177de2e5b)

> 当我们在xml修改一些东西后，运行在手机上可能没效果没效果。一般的原因就是build里面缓存导致。
>  解决方案：
>  1.**需要clean Project 再Rebuild Project后，运行在手机上才能生效。**
>  2.如果在**gradle.properties**里面配置了*android.buildCacheDir=./build/buildCache/* ，把他删除掉，在清理项目，就可以。
>  如图：
>
> ![img](https:////upload-images.jianshu.io/upload_images/3885155-0d4f4475048ff3cf.png?imageMogr2/auto-orient/strip|imageView2/2/w/1200/format/webp)
>
> 



- 删除了mainactivity.kt，新建了相应的java文件

  备份：

  ```kotlin
  package com.example.myapplication
  
  import androidx.appcompat.app.AppCompatActivity
  import android.os.Bundle
  import android.widget.Button
  import android.content.Intent;
  import android.view.View;
  
  
  class MainActivity : AppCompatActivity() {
  
      // Declare a variable for the button
      private lateinit var mbtLogin: Button;
  
      override fun onCreate(savedInstanceState: Bundle?) {
          super.onCreate(savedInstanceState)
          setContentView(R.layout.activity_main)
  
          //1. Find the button by its id
          mbtLogin = findViewById(R.id.button_login);
          // 2. Set a click listener on the button
  
      }
  
  
  }
  ```

  

### 10.8

- [kotlin和java相互转换的实操](https://blog.csdn.net/weixin_43202123/article/details/125747448?ops_request_misc=&request_id=&biz_id=102&utm_term=android%20studio%E6%80%8E%E4%B9%88%E6%8A%8Akotlin%E8%BD%AC%E6%8D%A2%E4%B8%BAjava&utm_medium=distribute.pc_search_result.none-task-blog-2~all~sobaiduweb~default-0-125747448.142^v95^chatgptT3_1&spm=1018.2226.3001.4187)

  > 其实就是互转，下面用Android studio 示范
  >
  > Kotlin 转换Java文件
  >
  >     Tools>Kotlin>Show Kotlin Bytecode
  >     Decompile
  >
  > Java转换kotlin文件（需要studio3.0）或者安装了kotlin插件。
  >
  > 选择页面的要转的文件
  >
  > 第一种   Ctrl+Shift+Alt+K
  >
  > 第二种    Code - Convert Java File To Kotlin File 
  >  



### 10.9

!解决编译慢的问题了！！（就是梯子太卡了awa,换梯子之后只编译了2s……无语啦



课堂任务

> 理解您的需求，下面是一个完整的示例，包含每一步的具体代码以创建一个Android应用程序，其中一个Activity显示日历，点击日期后将日期数据传递到另一个Activity中。在这个示例中，我们将使用 "Material Calendar View" 库来实现日期选择。
>
> 1. **创建新项目**：
>
>    在Android Studio中创建一个新的Android项目。
>
> 2. **添加依赖库**：
>
>    打开项目级别的build.gradle文件，并确保已添加以下依赖库：
>
>    ```gradle
>    implementation 'com.applandeo:material-calendar-view:1.7.0'
>    ```
>
> 3. **设计第一个Activity的布局**：
>
>    在 `activity_main.xml` 布局文件中，添加一个按钮，用户可以点击它来打开日历选择日期。
>
>    ```xml
>    <?xml version="1.0" encoding="utf-8"?>
>    <LinearLayout
>        xmlns:android="http://schemas.android.com/apk/res/android"
>        xmlns:app="http://schemas.android.com/apk/res-auto"
>        xmlns:tools="http://schemas.android.com/tools"
>        android:layout_width="match_parent"
>        android:layout_height="match_parent"
>        android:orientation="vertical"
>        android:gravity="center"
>        android:padding="16dp"
>        tools:context=".MainActivity">
>
>        <Button
>            android:id="@+id/button_open_calendar"
>            android:layout_width="wrap_content"
>            android:layout_height="wrap_content"
>            android:text="Open Calendar"
>            android:textSize="18sp" />
>
>    </LinearLayout>
>    ```
>
> 4. **设计第二个Activity的布局**：
>
>    在 `activity_second.xml` 布局文件中，添加一个用于显示日期的TextView。
>
>    ```xml
>    <?xml version="1.0" encoding="utf-8"?>
>    <LinearLayout
>        xmlns:android="http://schemas.android.com/apk/res/android"
>        xmlns:app="http://schemas.android.com/apk/res-auto"
>        xmlns:tools="http://schemas.android.com/tools"
>        android:layout_width="match_parent"
>        android:layout_height="match_parent"
>        android:orientation="vertical"
>        android:gravity="center"
>        android:padding="16dp"
>        tools:context=".SecondActivity">
>
>        <TextView
>            android:id="@+id/textView"
>            android:layout_width="wrap_content"
>            android:layout_height="wrap_content"
>            android:text="Selected Date: "
>            android:textSize="18sp" />
>
>    </LinearLayout>
>    ```
>
> 5. **实现日期选择逻辑**：
>
>    在第一个Activity的Java文件中，为按钮添加点击事件，以打开日期选择器。
>
>    ```java
>    import android.content.Intent;
>    import android.os.Bundle;
>    import android.view.View;
>    import androidx.appcompat.app.AppCompatActivity;
>    import com.applandeo.materialcalendarview.CalendarView;
>    import com.applandeo.materialcalendarview.EventDay;
>    import com.applandeo.materialcalendarview.listeners.OnDayClickListener;
>    
>    import java.util.Calendar;
>    import java.util.List;
>    
>    public class MainActivity extends AppCompatActivity {
>    
>        @Override
>        protected void onCreate(Bundle savedInstanceState) {
>            super.onCreate(savedInstanceState);
>            setContentView(R.layout.activity_main);
>    
>            Button buttonOpenCalendar = findViewById(R.id.button_open_calendar);
>    
>            buttonOpenCalendar.setOnClickListener(new View.OnClickListener() {
>                @Override
>                public void onClick(View v) {
>                    // 打开日历选择日期
>                    Intent intent = new Intent(MainActivity.this, CalendarActivity.class);
>                    startActivityForResult(intent, 1);
>                }
>            });
>        }
>    }
>    ```
>
> 6. **创建第三个Activity，用于显示日历**：
>
>    在Android Studio中，创建一个新的Activity，可以按照以下步骤操作：
>
>    - 在项目资源管理器中，右键单击 "app" 模块。
>    - 选择 "New"（新建） > "Activity" > "Empty Activity"（空白Activity）。
>    - 为该Activity指定一个名称，例如 "CalendarActivity"。
>
> 7. **在CalendarActivity中实现日历选择**：
>
>    打开 `CalendarActivity.java` 文件，并添加以下代码：
>
>    ```java
>    import android.content.Intent;
>    import android.os.Bundle;
>    import androidx.annotation.NonNull;
>    import androidx.appcompat.app.AppCompatActivity;
>    import com.applandeo.materialcalendarview.CalendarView;
>    import com.applandeo.materialcalendarview.EventDay;
>    import com.applandeo.materialcalendarview.listeners.OnDayClickListener;
>    import java.text.SimpleDateFormat;
>    import java.util.ArrayList;
>    import java.util.Calendar;
>    import java.util.List;
>    
>    public class CalendarActivity extends AppCompatActivity {
>    
>        private CalendarView calendarView;
>    
>        @Override
>        protected void onCreate(Bundle savedInstanceState) {
>            super.onCreate(savedInstanceState);
>            setContentView(R.layout.activity_calendar);
>    
>            calendarView = findViewById(R.id.calendarView);
>    
>            // 设置日历视图的点击事件监听器
>            calendarView.setOnDayClickListener(new OnDayClickListener() {
>                @Override
>                public void onDayClick(EventDay eventDay) {
>                    Calendar clickedDayCalendar = eventDay.getCalendar();
>                    SimpleDateFormat dateFormat = new SimpleDateFormat("yyyy-MM-dd");
>                    String selectedDate = dateFormat.format(clickedDayCalendar.getTime());
>    
>                    // 将所选日期返回到MainActivity
>                    Intent resultIntent = new Intent();
>                    resultIntent.putExtra("selectedDate", selectedDate);
>                    setResult(RESULT_OK, resultIntent);
>                    finish();
>                }
>            });
>        }
>    }
>    ```
>
> 8. **在 `AndroidManifest.xml` 中声明CalendarActivity**：
>
>    确保在 `AndroidManifest.xml` 中声明 `CalendarActivity`：
>
>    ```xml
>    <activity android:name=".CalendarActivity" />
>    ```
>
> 9. **处理日期选择结果**：
>
>    在第一个Activity中，处理从CalendarActivity返回的所选日期：
>
>    ```java
>    @Override
>    protected void onActivityResult(int requestCode, int resultCode, Intent data) {
>        super.onActivityResult(requestCode, resultCode, data);
>           if (requestCode == 1 && resultCode == RESULT_OK) {
>           if (data != null && data.hasExtra("selectedDate")) {
>               String selectedDate = data.getStringExtra("selectedDate");
>          
>               // 更新UI以显示所选日期
>               TextView textView = findViewById(R.id.textView);
>               textView.setText("Selected Date: " + selectedDate);
>           }
>       }
>    }
>
> 
>
> 这样，您就可以在第一个Activity中选择日期，将其传递到CalendarActivity进行选择，然后返回所选日期并在第一个Activity中显示它。确保您的布局文件和代码与上述示例匹配，并根据需要进行适当的自定义。



### *10.16*

- [x] 将安卓手机与Android Studio连接

#坑 Android Studio 真机调试每次都需要安装

==KEY== : 开发者模式—USB调试----监控ADB安装应用-----关闭即可解决。



gpt_eg1:

>  请注意，之前的回答中已经为大多数代码提供了注释，在这里提供了剩下的代码的基本注释：
>
> ```java
> public class MainActivity extends AppCompatActivity {
>     private DatabaseHelper dbHelper;  // 声明了一个 DatabaseHelper 对象，用于管理数据库的创建和更新
>     private SQLiteDatabase database;  // 声明了一个 SQLiteDatabase 对象，用于执行数据库操作
>     private TextView questionTextView;  // 声明了一个 TextView 对象，用于显示问题
>     private EditText answerEditText;  // 声明了一个 EditText 对象，用于接收答案输入
>     private TextView resultTextView;  // 声明了一个 TextView 对象，用于显示答案结果
> 
>     @Override
>     protected void onCreate(Bundle savedInstanceState) {  // 活动创建时调用的方法
>         super.onCreate(savedInstanceState);
>         setContentView(R.layout.activity_main);  // 设置活动使用的布局文件
> 
>         dbHelper = new DatabaseHelper(this);  // 创建 DatabaseHelper 实例，以便访问数据库
>         database = dbHelper.getReadableDatabase();  // 获取可读数据库对象
> 
>         questionTextView = findViewById(R.id.questionTextView);  // 初始化 questionTextView 对象
>         answerEditText = findViewById(R.id.answerEditText);  // 初始化 answerEditText 对象
>         resultTextView = findViewById(R.id.resultTextView);  // 初始化 resultTextView 对象
> 
>         loadRandomMathProblem();  // 载入随机的数学问题
>     }
> 
>     public void checkAnswer(View view) {  // 点击按钮后执行的方法
>         String userAnswer = answerEditText.getText().toString();  // 获取用户输入的答案
>         String correctAnswer = getCorrectAnswer();  // 获取正确答案
> 
>         if (userAnswer.equals(correctAnswer)) {  // 比较用户答案和正确答案
>             resultTextView.setText("Correct!");  // 若答案正确，显示 "Correct!"
>         } else {
>             resultTextView.setText("Incorrect. Try again.");  // 若答案错误，显示 "Incorrect. Try again."
>         }
> 
>         answerEditText.getText().clear();  // 清空答案输入框的内容
>         loadRandomMathProblem();  // 载入下一个随机的数学问题
>     }
> 
>     private void loadRandomMathProblem() {  // 加载随机的数学问题
>         String[] columns = {DatabaseHelper.COL_QUESTION};  // 指定要检索的列
>         Cursor cursor = database.query(
>             DatabaseHelper.TABLE_NAME, columns, null, null, null, 
>             null, "RANDOM()", "1"  // 指定 SQL 查询的选择条件和排序规则
>         );
> 
>         if (cursor != null && cursor.moveToFirst()) {  // 检查 cursor 是否有效，并将其移到第一行
>             String question = cursor.getString(cursor.getColumnIndex(DatabaseHelper.COL_QUESTION));  // 提取问题列的值
>             questionTextView.setText(question);  // 将问题文本显示在界面上
>         }
>         if (cursor != null) {
>             cursor.close();  // 关闭 cursor
>         }
>     }
> 
>     private String getCorrectAnswer() {  // 获取正确答案
>         String[] columns = {DatabaseHelper.COL_ANSWER};  // 指定要检索的列
>         Cursor cursor = database.query(
>             DatabaseHelper.TABLE_NAME, columns, null, null, null, 
>             null, null, "1"  // 指定 SQL 查询的选择条件和排序规则
>         );
> 
>         if (cursor != null && cursor.moveToFirst()) {
>             return String.valueOf(cursor.getInt(cursor.getColumnIndex(DatabaseHelper.COL_ANSWER)));  // 获取正确答案
>         }
>         if (cursor != null) {
>             cursor.close();
>         }
>         return "";
>     }
> 
>     @Override
>     protected void onDestroy() {  // 活动销毁时调用的方法
>         super.onDestroy();
>         if (database != null) {
>             database.close();  // 关闭数据库连接
>         }
>     }
> }
> ```
>
> 这些注释描述了每个方法的功能和目的，并对每个成员变量的用途进行了解释。
>
> 希望这可以回答您的问题。如果您有其他问题，请随时提问。

#坑 数据库文件未升级

> - KEY1：
>   - ==**直接从设备上删除应用**==是删除数据库文件最便捷的方法。要在模拟器上删除应用，可以切换 到应用浏览器界面，向上拖动CriminalIntent应用的图标，直到屏幕顶部出现Uninstall字样


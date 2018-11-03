---
layout: post
title:  Android-Studio
categories: 
    - Android
    - Android Studio
description: Android
keywords: Android
comments: true
---

> 安卓开发工具Android Studio

```angular2html
<TableLayout xmlns:android="http://schemas.android.com/apk/res/android"

    android:layout_width="fill_parent"

    android:layout_height="fill_parent"

    android:gravity="center_vertical"

    android:stretchColumns="0,3">

    <TableRow>

        <TextView />

        <TextView

            android:text="账   号："

            android:layout_width="wrap_content"

            android:layout_height="wrap_content"


            />

        <EditText

            android:id="@+id/account"

            android:layout_width="170dp"

            android:layout_height="wrap_content"

            android:minWidth="220px"

            android:textSize="24px" />

        <TextView />

    </TableRow>

    <TableRow android:layout_marginTop="20px">

        <TextView />

        <TextView

            android:text="密  码："

            android:layout_width="wrap_content"

            android:layout_height="wrap_content"

            />

        <EditText

            android:id="@+id/pwd"

            android:layout_width="wrap_content"

            android:layout_height="wrap_content"

            android:minWidth="220px"

            android:textSize="24px"

            android:inputType="textPassword"/>

        <TextView />

    </TableRow>

    <TableRow android:layout_marginTop="20px">

        <TextView />

        <Button

            android:id="@+id/login"

            android:layout_width="75dp"

            android:layout_height="wrap_content"

            android:text="登录"

            />

        <Button

            android:id="@+id/quit"

            android:layout_width="91dp"

            android:layout_height="wrap_content"

            android:text="退出" />

        <TextView />

    </TableRow>

</TableLayout>
```


### 点击事件

OnClickListener注册监听，重写onclick方法
```angular2html
import android.view.View.OnClickListener;
 
public class MainActivity extends AppCompatActivity implements OnClickListener {
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
 
        findViewById(R.id.myButton).setOnClickListener(MainActivity.this);
        findViewById(R.id.myButton2).setOnClickListener(MainActivity.this);
    }
    @Override
    public void onClick(View v) {
        switch (v.getId())
        {
            case R.id.myButton:
                Toast.makeText(MainActivity.this,"你点击了myButton" , Toast.LENGTH_SHORT).show();
                break;
            case R.id.myButton2:
                Toast.makeText(MainActivity.this,"你点击了myButton2" , Toast.LENGTH_SHORT).show();
                break;
        }
    }
}
```

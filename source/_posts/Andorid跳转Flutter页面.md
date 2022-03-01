---
title: Andorid跳转Flutter页面
date: 2020-08-17 09:17:02
tags:
  - App应用
category: Java
---

## flutter 页面配置

### 创建 flutter 项目

```
flutter create -t module '项目名称'
```

### 打开 Andorid 项目目录

![](/images/andoridtoFlutter/operate1.png)

## Andorid 页面配置

接下来由于 Andorid studio 的项目本地配置信息与你 flutter 生成的 Andorid 项目配置信息不符就会有接下来的一些问题：
![](/images/andoridtoFlutter/operate2.png)
所以这时候我们需要 build 我的项目，查看项目中存在什么问题
![](/images/andoridtoFlutter/operate3.png)

### 修改配置

产生这种问题的原因是就是因为 flutter 的 Andorid 项目配置与本地配置不兼容
将 gradle 文件里的配置改成本地项目的版本

```
distributionUrl=https\://services.gradle.org/distributions/gradle-5.6.2-all.zip
```

改为

```
distributionUrl=https\://services.gradle.org/distributions/gradle-4.6-all.zip
```

以上是我的本地配置，不一定符合你们的本地配置，想看自己本地配置可以新建一个项目或者查看以前项目的配置

将 APP 中的 gradle 文件的中的配置改成对应版本

```
distributionUrl=https\://services.gradle.org/distributions/gradle-5.6.2-all.zip
```

改为

````

distributionUrl=https\://services.gradle.org/distributions/gradle-4.6-all.zip
``
将 gradle.properties 文件中的<label style="background-color: #fff5f5;color:#ff502c;">android.enableR8=true</label>改为<label style="background-color: #fff5f5;color:#ff502c;">android.enableR8=false</label>

## 设置跳转

### 新建 Andorid 页面

```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
   xmlns:app="http://schemas.android.com/apk/res-auto"
   android:orientation="vertical" android:layout_width="match_parent"
   android:layout_height="match_parent">
   <Button
       android:id="@+id/btn_jump_to_flutter"
       android:layout_width="match_parent"
       android:layout_height="wrap_content"
       android:text="跳转Flutter"/>

</LinearLayout>
````

```java
public class MainActivity extends AppCompatActivity {

    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        Button btnJumpToFlutter = (Button) findViewById(R.id.btn_jump_to_flutter);
        btnJumpToFlutter.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                Intent intent = new Intent(MainActivity.this, MainFlutterActivity.class);
                startActivity(intent);
            }
        });
    }
}
```

### 关联 flutter 页面

```java
public class MainFlutterActivity extends FlutterActivity {

}
```

修改完成后虽然可以进行运行，但会报一下错误
![](/images/andoridtoFlutter/operate4.png)
这是要页面主题设置主题，请修改 APP 中的 AndoridMainifest.xml 文件
![](/images/andoridtoFlutter/operate5.png)
就完成了

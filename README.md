# 实现设置Activity
## 实现设置Activity : 总共四组设置项 
### In-line preferences 
  CheckBoxPreference 
### Dialog-based preferences
  EditTextPreference 
  ListPreference 
### Launch preferences 
  PreferenceScreen: 跳转到另一个PreferenceScreen 
  PreferenceScreen: 启动一个网页Preference 
### attributes CheckBox: 父选项 CheckBox: 子选项，当父选项勾选时呈现 



1. activity_main.xml
```
    <fragment
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:id="@+id/setting_out"
        android:name="com.example.cy5962.test4.PreFragment"/>
 ```

 2. preference.xml
 ```
    <PreferenceCategory android:title="In-line preferences">
        <CheckBoxPreference
            android:key="Checkbox_preference"
            android:title="Checkbox_preference"
            android:summary="This a checkbox">
        </CheckBoxPreference>
    </PreferenceCategory>

    <PreferenceCategory android:title="Dialog-based preferences">
        <EditTextPreference
            android:title="EditTextPreference"
            android:key="EditText"
            android:summary="An example that uses an edit text dialog"
            android:dialogTitle="Enter your favortie animal">
        </EditTextPreference>
        <ListPreference
            android:key="list"
            android:title="List preference"
            android:summary="An example that use a list dialog"
            android:dialogTitle="Choose one">
        </ListPreference>
    </PreferenceCategory>

    <PreferenceCategory android:title="Launch preferences">
        <PreferenceScreen
            android:key="screen"
            android:title="Screen preference"
            android:summary="Shows another screen of preferences">
            <CheckBoxPreference
                android:key="s_checkbox"
                android:summary="Preference that is on the next screen but same hierarchy"
                android:title="Toggle preference">
            </CheckBoxPreference>
        </PreferenceScreen>
        <PreferenceScreen
            android:summary="Launches an Activity from an intent"
            android:title="Intent preference" >
            <intent
                android:action="android.intent.action.VIEW"
                android:data="http://www.google.com">
            </intent>
        </PreferenceScreen>
    </PreferenceCategory>
    <PreferenceCategory android:title="Preference attributes">
        <CheckBoxPreference
            android:key="parent_checkbox"
            android:summary="This is visually parent"
            android:title="Parent checkbox preference">
        </CheckBoxPreference>
        <CheckBoxPreference
            android:key="child_checkbox"
            android:summary="This is visually a child"
            android:title="Child checkbox preference"
            android:dependency="parent_checkbox"/>
    </PreferenceCategory>
</PreferenceScreen>
```

3. PreFragment.java
```
package com.example.cy5962.test4;

import android.os.Bundle;
import android.preference.PreferenceFragment;
import android.support.annotation.Nullable;

public class PreFragment extends PreferenceFragment {
    @Override
    public void onCreate(@Nullable Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        addPreferencesFromResource(R.xml.preference);
    }
}
```

4. MainActivity.java
```
package com.example.cy5962.test4;

import android.app.FragmentManager;
import android.app.FragmentTransaction;
import android.support.v7.app.AppCompatActivity;
import android.os.Bundle;

public class MainActivity extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        FragmentManager fragmentManager=getFragmentManager();
        //开启一个新事物
        FragmentTransaction transaction=fragmentManager.beginTransaction();
        PreFragment preFragment=new PreFragment();
        transaction.add(R.id.setting_out,preFragment);
        transaction.commit();
    }
}
```
![全截图](https://img-blog.csdnimg.cn/20190417134819912.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2JlbHRv,size_16,color_FFFFFF,t_70)

![Edit](https://img-blog.csdnimg.cn/20190417135038824.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2JlbHRv,size_16,color_FFFFFF,t_70)

![跳转1](https://img-blog.csdnimg.cn/20190417135116993.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2JlbHRv,size_16,color_FFFFFF,t_70)

![跳转2](https://img-blog.csdnimg.cn/20190417135147735.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2JlbHRv,size_16,color_FFFFFF,t_70)

![父子组件](https://img-blog.csdnimg.cn/20190417134937112.png)

---
title:      "android 实现顶部的滚动通知"
cover:      "https://image.animekid.cn/images/2019/02/02/a8eee80f86560bfbd193a420b0814267.md.png"
date:       "2019-02-28 15:26:44"
tags:
    - Kotlin
    - Android
---

#### 设置顶部的滚动通知  
其实只需要一个textview即可实现这种功能  
```xml
<TextView
    android:id="@+id/txt"
    android:layout_width="400dp"
    android:layout_height="30dp"
    android:textSize="20sp"
    android:text="我来不及认真地年轻，待明白过来时，只能选择认真地老去。"
    android:paddingLeft="35dp"
    android:paddingRight="15dp"
    android:layout_above="@+id/search"
    android:layout_centerHorizontal="true"
    android:layout_marginBottom="30dp"
    android:background="@drawable/ggt"
    android:ellipsize="marquee"
    android:marqueeRepeatLimit="marquee_forever"
    android:singleLine="true"
    android:focusable="true"
    android:focusableInTouchMode="true"
    android:scrollHorizontally="true" />

```

--- 
* `android:ellipsize="marquee"` 是字体滚动
* `android:marqueeRepeatLimit="marquee_forever"` 是字体永久滚动
* `android:singleLine="true"` 是字体单行显示
* `android:focusableInTouchMode="true"` 和 `android:scrollHorizontally="true"` 是允许手动操纵运动轨迹  

---
如果出现了不能使用的情况，可能是因为嵌套的UI太多，导致TextView获取不到焦点，所以，这时候就需要重新集成一个TextView了。
```kotlin
package cn.animekid.familybirthday.ui

import android.content.Context
import android.util.AttributeSet
import android.widget.TextView

class MarqueeText : TextView {
    constructor(context: Context) : super(context) {}
    constructor(context: Context, attrs: AttributeSet) : super(context, attrs) {}
    constructor(context: Context, attrs: AttributeSet, defStyleAttr: Int) : super(context, attrs, defStyleAttr) {}

    //返回textview是否处在选中的状态，返回true表示一直是获取焦点的
    override fun isFocused(): Boolean {
        return true
    }
}
```
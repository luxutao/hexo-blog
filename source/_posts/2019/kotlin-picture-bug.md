---
title:      "kotlin 调用相册不选择图片直接返回则崩溃的bug"
cover:      "https://image.123m.me/images/2019/02/02/4cf359e3ba8d11608a07a05f8855d2af.png"
date:       "2019-02-26 12:01:13"
tags:
    - Kotlin
    - Android
---

最近使用`kotlin`开发后发现调起相机拍照或相册时如果不选择就直接取消会崩溃!  
错误原因`kotlin`的`onActivityResult`方法中`data: intent`不能为`null`, 而在`Java`中这一项是可以为`null`的。

#### 解决办法
这里在`onActivityResult`最后一个参数添加`Intent`后面添加`?`,意思是允许`data`为空!这样就简单的解决这个bug了!
```kotlin
override fun onActivityResult(requestCode: Int, resultCode: Int, data: Intent?) {
    if (resultCode != RESULT_OK) return
    if (requestCode == Crop.REQUEST_CROP) 
        mPresenter.uploadUserIcon(File(tempImg))
    } else if (requestCode == CAMERA_REQUEST) {
        tempImg = CameraHelper.handleCameraResult(this)
    }
}
```

原答案地址：[android kotlin调起相机拍照取消崩溃的bug!](https://blog.csdn.net/qq_33391220/article/details/83783289 )

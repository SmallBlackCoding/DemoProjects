#ImageCropper
图片裁剪器，为各位追求用户体验的daLao提供更优质的服务
它能够

* 按需求比例裁剪图片，或者按照指定尺寸输出
* 它是一个view不是activity，所以并不需要在AndroidManifest.xml中注册

![image](https://github.com/iielse/DemoProjects/blob/master/P01_ImageCropper/previews/111.gif)

马蛋，模拟器不能多点触摸(![image](https://github.com/iielse/DemoProjects/blob/master/P01_ImageCropper/previews/222.gif))

## 下载（强烈推荐下载体验）

[DemoApp.apk](https://github.com/iielse/DemoProjects/blob/master/P01_ImageCropper/previews/app-debug.apk)

至尊体验;daLao专用;上图Gif不够看？下载apk自行体验; /doge

## 实现步骤

在module的gradle
```
compile 'ch.ielse:imagecropper:1.0.0'
```

首先在xml布局中
```
<FrameLayout
    xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent">

    <!-- some layout here -->

    <ch.ielse.view.imagecropper.ImageCropper
            android:id="@+id/v_image_cropper"
            android:layout_width="match_parent"
            android:layout_height="match_parent"/>

    <!-- 在跟布局的下面盖上的一个ImageCropper,ImageCropper初始化默认是INVISIABLE的 -->
</FrameLayout>
```

蓝后在Activity onCreate里面 一般需要调用这2个API简单的初始化一下

```
vImageCropper = (ImageCropper) findViewById(R.id.v_image_cropper);
// 默认值为false，一般情况下不一定要设置这个API
        vImageCropper.setOutputFixedSize(false);
// 实现裁剪结果回调
vImageCropper.setCallback(new ImageCropper.Callback(){
    @Override
    public void onPictureCropOut(Bitmap bitmap, String tag) {
        // save and display the result bitmap
    }
});
```

这个时候你的所有准备工作已经完成

```
/**
     * 裁剪图片(输出的图片默认只有比例是按照入参outputWidth和outputHeight获得的，尺寸大小并没有按照指定的尺寸大小。<br>
     * 如果要求大小也为入参请调用{@link ImageCropper#setOutputFixedSize(boolean)} 设置值为true) <br>
     * 逻辑见{@link ImageCropper#onClick(View)} output = mOutputWidth * mOutputHeight != 0 ? Bitmap.createScaledBitmap(clip, mOutputWidth, mOutputHeight, true) : clip <br>
     * ps: createScaledBitmap (小图变大图会造成内容的失真) 55555555<br>
     *
     * @param sourceFilePath  原图片路径
     * @param outputWidth     输出宽度
     * @param outputHeight    输出高度
     * @param isCircleOverlay 遮罩蒙板是否为圆形，为圆形的条件时在isCircleOverlay为true的同时，outputWidth等于outputHeight才行
     * @param tag             若同一界面有多处裁剪功能，对此传递一个tag标志避免混淆
     */
    public void crop(String sourceFilePath, int outputWidth, int outputHeight, boolean isCircleOverlay, String tag) { ... }
```
最后只要调用 `vImageCropper.crop()` 方法就可以了

可以具体看源码demo，这个项目是可以运行的，这个项目是可以运行的，这个项目是可以运行的

ps ：
本demo的代码对Android6.0动态权限的申请也做过处理，`PermissionUtils`的代码是有一定参考价值哒。
(参考了 AndPermission 代码实现方式，在此感谢一下原作者)
同时封装了获得图片的逻辑，简化调用，`PictureInquirer`的代码也是有一定参考价值哒。


## 写在最后
为什么要写这个Demo？

*能够给在项目上有这个功能需求而又愿意试水此库的各位daLao节约一些开发时间
*怕长时间不写代码，会慢慢忘记，于是反复练习
*为了更好的视觉体验

ps:如果此裤对你提供了帮助，你的Star是对本宝最大的支持。  谢 /舔

Q群274306954(可以找到我)
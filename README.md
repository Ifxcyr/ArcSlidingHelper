## 几行代码实现Android弧形滑动
### 添加依赖：
build.gradle:
```
allprojects {
    repositories {
        jcenter()
        maven { url "https://github.com/Ifxcyr/ArcSlidingHelper/raw/master" }
    }
}
```
app/build.gradle:
```
implementation 'com.wuyr:arcslidinghelper:1.0.0'
```
### 简单使用示例：
```
        mView = findViewById(R.id.view);
        //创建对象
        mArcSlidingHelper = ArcSlidingHelper.create(mView, new ArcSlidingHelper.OnSlidingListener() {
            @Override
            public void onSliding(float angle) {
                mView.setRotation(mView.getRotation() + angle);
            }
        });
        //开启惯性滚动
        mArcSlidingHelper.enableInertialSliding(true);

        getWindow().getDecorView().setOnTouchListener(new View.OnTouchListener() {
            @Override
            public boolean onTouch(View v, MotionEvent event) {
                //处理滑动事件
                mArcSlidingHelper.handleMovement(event);
                return true;
            }
        });
```
### 效果：
![preview](https://github.com/wuyr/ArcSlidingHelper/raw/master/preview.gif)
### APIs： 
```
//获取对象 (targetView: 接受滑动手势的View (圆弧滑动事件以此View的中心点为圆心))
ArcSlidingHelper.create(targetView, onSlidingListener);

//开启惯性滚动
enableInertialSliding(true);

//onTouchEvent中调用此方法
handleMovement(event);

//如果是自定义的ViewGroup, 需在onInterceptTouchEvent中调用此方法
updateMovement(event);

//如果监听onTouchEvent的是targetView本身, 需设置
setSelfSliding(ture);

//打断动画
abortAnimation();

//惯性滑动的利用率 (0~1) (数值越大，惯性滚动的时间越长)
setScrollAvailabilityRatio(ratio);

//更新圆心x坐标
updatePivotX(pivotX);

//更新圆心y坐标
updatePivotY(pivotY);

//释放资源
release();
```
### Demo: https://github.com/wuyr/ArcSlidingHelper
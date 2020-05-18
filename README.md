### Homework3

下载bulid目录里的app-debug.apk

运行查看app运行效果

### Ex1

#### TODO1: 将 lottie 控件的相关属性补全

```
app:lottie_loop="true"
app:lottie_rawRes="@raw/material_wave_loading" 
```

#### TODO2:

```
animationView.setProgress((float) progress / 100);
```



### Ex2

#### TODO1:    实现另一个 ObjectAnimator，对 target 控件的大小进行缩放，从 1 到 2 循环

```
//x坐标
ObjectAnimator scaleXAnimator = ObjectAnimator.ofFloat(target,"scaleX",1,2);
scaleXAnimator.setRepeatCount(ValueAnimator.INFINITE);
scaleXAnimator.setInterpolator(new LinearInterpolator());
scaleXAnimator.setDuration(1000);
scaleXAnimator.setRepeatMode(ValueAnimator.REVERSE);

//y坐标
ObjectAnimator scaleYAnimator = ObjectAnimator.ofFloat(target,"scaleY",1,2);
scaleYAnimator.setRepeatCount(ValueAnimator.INFINITE);
scaleYAnimator.setInterpolator(new LinearInterpolator());
scaleYAnimator.setDuration(1000);
scaleYAnimator.setRepeatMode(ValueAnimator.REVERSE);
```

#### TODO2:     实现另一个 ObjectAnimator，对 target 控件的透明度进行修改，从 1 到 0.5f 循环

```
ObjectAnimator alphaAnimator = ObjectAnimator.ofFloat(target,"alpha",1,0.5f);
alphaAnimator.setRepeatCount(ValueAnimator.INFINITE);
alphaAnimator.setInterpolator(new LinearInterpolator());
alphaAnimator.setDuration(500);
alphaAnimator.setRepeatMode(ValueAnimator.REVERSE);
```

#### TODO2:     将上面创建的其他 ObjectAnimator 都添加到 AnimatorSet 中

```
animatorSet = new AnimatorSet();
animatorSet.playTogether(animator1,scaleXAnimator,scaleYAnimator,alphaAnimator);
animatorSet.start();
animatorSet = new AnimatorSet();
animatorSet.playTogether(animator1);
animatorSet.start();
```



### Ex3

```
// TODO: ex3-1. 添加 ViewPager 和 Fragment 做可滑动界面
ViewPager pager = findViewById(R.id.view_pager);
TabLayout tabLayout = findViewById(R.id.tab_layout);
pager.setAdapter(new FragmentPagerAdapter(getSupportFragmentManager()) {
    @Override
    public Fragment getItem(int i) {
        return new PlaceholderFragment();
    }

    @Override
    public int getCount() {
        return 2;
    }

    @Override
    public CharSequence getPageTitle(int position){
        if(position == 0){
            return "好友列表";
        }
        else{
            return "我的好友";
        }
    }
});

// TODO: ex3-2, 添加 TabLayout 支持 Tab
tabLayout.setupWithViewPager(pager);
```

#### TODO3:   修改 fragment_placeholder，添加 loading 控件和列表视图控件

```
<com.airbnb.lottie.LottieAnimationView
    android:id="@+id/animation_view"
    android:layout_width="wrap_content"
    android:layout_height="wrap_content"
    android:layout_gravity="center"
    app:lottie_autoPlay="true"
    app:lottie_loop="true"
    app:lottie_rawRes="@raw/material_wave_loading" />

<android.support.v7.widget.RecyclerView
    android:id="@+id/rv_numbers"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:layoutManager="android.support.v7.widget.LinearLayoutManager"
    tools:listitem="@layout/list_item"/>
```

```
<!--TODO ex3-3: 修改 fragment_placeholder，添加 loading 控件和列表视图控件 -->
<com.airbnb.lottie.LottieAnimationView
    android:id="@+id/animation_view"
    android:layout_width="wrap_content"
    android:layout_height="wrap_content"
    android:layout_gravity="center"
    app:lottie_autoPlay="true"
    app:lottie_loop="true"
    app:lottie_rawRes="@raw/material_wave_loading" />

<android.support.v7.widget.RecyclerView
    android:id="@+id/rv_numbers"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:layoutManager="android.support.v7.widget.LinearLayoutManager"
    tools:listitem="@layout/list_item"/>
```

```
// TODO ex3-4：实现动画，将 lottie 控件淡出，列表数据淡入
//淡出
ObjectAnimator alphaAnimator = ObjectAnimator.ofFloat(animationView,"alpha",1,0f);

alphaAnimator.setInterpolator(new LinearInterpolator());
alphaAnimator.setDuration(500);

//淡入
recyclerView = getView().findViewById(R.id.rv_numbers);
recyclerView.setLayoutManager(new LinearLayoutManager(getActivity(), LinearLayoutManager.VERTICAL, false));
mAdapter = new CardAdapter(5);

recyclerView.setAdapter(mAdapter);
ObjectAnimator alphaAnimatorOpen = ObjectAnimator.ofFloat(recyclerView,"alpha",0,1f);

alphaAnimatorOpen.setInterpolator(new LinearInterpolator());
alphaAnimatorOpen.setDuration(500);

animatorSet = new AnimatorSet();
animatorSet.playTogether(alphaAnimator,alphaAnimatorOpen);
animatorSet.start();
```
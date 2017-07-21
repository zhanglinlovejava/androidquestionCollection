# androidquestionCollection
android 开发中遇到的问题总结


1，Android开发中有哪些兼容性问题？都是怎么解决的？

`音频的兼容性问题就复杂的多，分为语音业务也和视频电话业务两大模块。首先是录音源配置，大部分的手机在语音或视频电话时使用
MediaRecorder.AudioSource.MIC 即可，但三星华为某些机型需要在视频电话时将录音设备设置成 
MediaRecorder.AudioSource.VOICE_COMMUNICATION 。
接着是amr编码方式的配置，可以使用系统的Mediarecorder直接录制amr文件，也可以使用Audiorecorder录制pcm后，调so库编码成amr文件，
有一个高速语音的设置项可以供用户选择，但是有些机型只能使用其中的某一种才能正常发语音，所以需要动态配置。
还有一些是声音录不进的问题，一般就是指定的samplerate不支持或者录音权限没开。
然后是语音播放扬声器、听筒模式切换，这类反馈量比较大。主要就是前面介绍的speakerPhone、mode、 streamType的组合要设置正确。
语音播放和语音通话还不能使用同一套策略，需要分别设置。

2，场景
魅族手机ListView的Item中的EditText无法编辑，点击EditText弹出软键盘后，软键盘会立即自动隐藏
机型
魅族3和魅族4
解决方案
将ListView换成RecyclerView

3，场景：HTC M8 从一个Activity 使用QQSDK 登陆, 登陆成功后, 返回Activity结果Activity 被销毁了
机型：HTC M8 等某些带有 虚拟 Menu 键盘的手机
解决方案：后来调查发现是这个Activity是全屏,屏蔽了Menu键盘的黑条. 但是跳转到QQ却把那个Menu的黑条显示了出来, 这导致发生了 screenSize 的变化 从而导致我的Activity销毁了.
知道了这个原因, 在manifest中的 configChanges 添加screenSize 解决了这个问题

4 自定义 imageview 点击的时候显示灰色  
@Override
    public boolean onTouchEvent(MotionEvent event) {

        switch (event.getAction()) {
            case MotionEvent.ACTION_DOWN:
                this.setColorFilter(0x33000000);
                return super.onTouchEvent(event);
            case MotionEvent.ACTION_UP:
            case MotionEvent.ACTION_CANCEL:
                this.setColorFilter(null);
                break;
        }
        return super.onTouchEvent(event);
    }

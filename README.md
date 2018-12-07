# QRProject

> 所需权限

    <uses-permission android:name="android.permission.CAMERA" />
    <uses-permission android:name="android.permission.FLASHLIGHT" />
    <uses-feature android:name="android.hardware.camera" />
    <uses-feature android:name="android.hardware.camera.autofocus" />
    <uses-permission android:name="android.permission.VIBRATE" />
    <uses-permission android:name="android.permission.WAKE_LOCK" />
    <uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE" />
    <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
   
   
> 扫描二维码代码

         Intent intent = new Intent(MainActivity.this, CaptureActivity.class);
                                /*ZxingConfig是配置类
                                 *可以设置是否显示底部布局，闪光灯，相册，
                                 * 是否播放提示音  震动
                                 * 设置扫描框颜色等
                                 * 也可以不传这个参数
                                 * */
        ZxingConfig config = new ZxingConfig();
//                                config.setPlayBeep(false);//是否播放扫描声音 默认为true
//                                config.setShake(false);//是否震动  默认为true
//                                config.setDecodeBarCode(false);//是否扫描条形码 默认为true
        config.setReactColor(R.color.colorPrimaryDark);//设置扫描框四个角的颜色 默认为白色
//                                config.setFrameLineColor(R.color.colorPrimaryDark);//设置扫描框边框颜色 默认无色
        config.setScanLineColor(R.color.colorAccent);//设置扫描线的颜色 默认白色
//                                config.setFullScreenScan(false);//是否全屏扫描  默认为true  设为false则只会在扫描框中扫描
        intent.putExtra(Constant.INTENT_ZXING_CONFIG, config);
        startActivityForResult(intent, 101);
        
   
       
         @Override
    protected void onActivityResult(int requestCode, int resultCode, Intent data) {
        super.onActivityResult(requestCode, resultCode, data);
        // 扫描二维码/条码回传
        if (requestCode == 101 && resultCode == RESULT_OK) {
            if (data != null) {
                String content = data.getStringExtra(Constant.CODED_CONTENT);
                Log.e("扫描结果为：", content);
            }
        }
    } 
    
> 生成二维码
    
     String contentEtString = "测试二维码";

        Bitmap bitmap = null;
        try {
                    /*
                    * contentEtString：字符串内容
                    * w：图片的宽
                    * h：图片的高
                    * logo：不需要logo的话直接传null
                    * */

            Bitmap logo = BitmapFactory.decodeResource(getResources(), R.mipmap.ic_launcher);
            bitmap = CodeCreator.createQRCode(contentEtString, 400, 400, null);
            imgN.setImageBitmap(bitmap);
        }  catch (WriterException e) {
            Toast.makeText(this,"生成二维码出错->" + e.getMessage(),Toast.LENGTH_LONG).show();
            e.printStackTrace();
        }
    
    

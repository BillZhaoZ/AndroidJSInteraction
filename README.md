# AndroidJS
Android 和JavaScript交互，互调方法(包括无参调用和有参数调用)；

 1. 启用javascript
    contentWebView.getSettings().setJavaScriptEnabled(true);
   
 2. 从assets目录下面的加载html
     contentWebView.loadUrl("file:///android_asset/JsTestWeb.html");
     contentWebView.addJavascriptInterface(MainActivity.this, "android");
 
 安卓调用JS
 
 3. 无参调用Js点击
 
    findViewById(R.id.button).setOnClickListener(new View.OnClickListener() {
                @Override
                public void onClick(View v) {
                    // 无参数调用
                    contentWebView.loadUrl("javascript:javaCallJs()");
                }
            });
            
 4. 有参调用Js点击
    findViewById(R.id.button2)
        .setOnClickListener(new View.OnClickListener() {
             @Override
              public void onClick(View v) {
                // 传递参数调用
                contentWebView.loadUrl("javascript:javaCallJsWith(" + "'http://blog.csdn.net/luoshengyang/article/details/6618363/'" + ")");
              }
    });  
 
 JS调用Android方法
 
 5. 无参
    
    <input type="button" value="点击调用java代码" onclick="window.android.startFunction()"/>

     //由于安全原因 需要加 @JavascriptInterface
        @JavascriptInterface
        public void startFunction() {

            runOnUiThread(new Runnable() {
                @Override
                public void run() {
                    Toast.makeText(MainActivity.this, "show", 3000).show();
                }
            });
        }

 6. 无参调用
    
    <input type="button" value="点击调用java代码,并传递参数"
       onclick="window.android.startFunction('http://blog.csdn.net/luoshengyang/article/details/6618363')"/>
       
        @JavascriptInterface
           public void startFunction(final String text) {
               runOnUiThread(new Runnable() {
       
                   @Override
                   public void run() {
                       new AlertDialog.Builder(MainActivity.this).setMessage(text).show();
                   }
               });
           }
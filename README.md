# Khodiyar-JP-Parlour
Kirana store 

KhodiyarApp.zip
├── app/
│   ├── src/
│   │   ├── main/
│   │   │   ├── java/com/khodiyar/app/
│   │   │   │   └── MainActivity.java
│   │   │   ├── assets/
│   │   │   │   └── index.html
│   │   │   ├── res/
│   │   │   │   ├── layout/
│   │   │   │   │   └── activity_main.xml
│   │   │   │   ├── values/
│   │   │   │   │   ├── strings.xml
│   │   │   │   │   ├── colors.xml
│   │   │   │   │   └── themes.xml
│   │   │   │   └── mipmap/
│   │   │   │       ├── ic_launcher.png
│   │   │   │       └── ic_launcher_round.png
│   │   │   └── AndroidManifest.xml
│   │   └── test/ (empty)
│   ├── build.gradle (app level)
│   └── proguard-rules.pro
├── gradle/
│   └── wrapper/
│       ├── gradle-wrapper.jar
│       └── gradle-wrapper.properties
├── build.gradle (project level)
├── settings.gradle
└── gradle.properties
```

---

📄 All Files in One Place

1. MainActivity.java

```java
package com.khodiyar.app;

import android.os.Bundle;
import android.webkit.WebView;
import android.webkit.WebSettings;
import android.webkit.WebViewClient;
import android.view.KeyEvent;
import android.net.ConnectivityManager;
import android.net.NetworkInfo;
import android.content.Context;
import android.content.Intent;
import android.net.Uri;
import android.widget.Toast;
import androidx.appcompat.app.AppCompatActivity;

public class MainActivity extends AppCompatActivity {

    private WebView webView;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        webView = findViewById(R.id.webview);

        if (!isNetworkAvailable()) {
            Toast.makeText(this, "No Internet Connection", Toast.LENGTH_LONG).show();
        }

        WebSettings webSettings = webView.getSettings();
        webSettings.setJavaScriptEnabled(true);
        webSettings.setDomStorageEnabled(true);
        webSettings.setLoadWithOverviewMode(true);
        webSettings.setUseWideViewPort(true);
        webSettings.setBuiltInZoomControls(false);
        webSettings.setDisplayZoomControls(false);
        webSettings.setSupportZoom(false);
        webSettings.setAllowFileAccess(true);
        webSettings.setAllowContentAccess(true);
        webSettings.setCacheMode(WebSettings.LOAD_DEFAULT);

        webView.setWebViewClient(new WebViewClient() {
            @Override
            public boolean shouldOverrideUrlLoading(WebView view, String url) {
                if (url.startsWith("https://wa.me") || url.startsWith("tel:")) {
                    Intent intent = new Intent(Intent.ACTION_VIEW, Uri.parse(url));
                    startActivity(intent);
                    return true;
                }
                return false;
            }
        });

        webView.loadUrl("file:///android_asset/index.html");
    }

    @Override
    public boolean onKeyDown(int keyCode, KeyEvent event) {
        if (keyCode == KeyEvent.KEYCODE_BACK && webView.canGoBack()) {
            webView.goBack();
            return true;
        }
        return super.onKeyDown(keyCode, event);
    }

    private boolean isNetworkAvailable() {
        ConnectivityManager connectivityManager = (ConnectivityManager) 
                getSystemService(Context.CONNECTIVITY_SERVICE);
        NetworkInfo activeNetworkInfo = connectivityManager.getActiveNetworkInfo();
        return activeNetworkInfo != null && activeNetworkInfo.isConnected();
    }
}
```

---

2. activity_main.xml

```xml
<?xml version="1.0" encoding="utf-8"?>
<RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:background="#5a2e0f">

    <ProgressBar
        android:id="@+id/progressBar"
        style="?android:attr/progressBarStyleHorizontal"
        android:layout_width="match_parent"
        android:layout_height="3dp"
        android:layout_alignParentTop="true"
        android:progressTint="#f5b042"
        android:visibility="gone" />

    <WebView
        android:id="@+id/webview"
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        android:overScrollMode="never" />

</RelativeLayout>
```

---

3. index.html

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>Khodiyar JP Parlour</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Segoe UI', Roboto, Arial, sans-serif;
        }
        
        body {
            background-color: #f5efe6;
        }
        
        .header {
            background: #5a2e0f;
            color: white;
            padding: 25px 20px;
            text-align: center;
            border-bottom-left-radius: 30px;
            border-bottom-right-radius: 30px;
            box-shadow: 0 4px 15px rgba(0,0,0,0.3);
        }
        
        .header h1 {
            font-size: 28px;
            letter-spacing: 1px;
        }
        
        .header p {
            font-size: 16px;
            opacity: 0.9;
            margin-top: 5px;
        }
        
        .card {
            background: white;
            margin: 15px 15px;
            padding: 20px;
            border-radius: 20px;
            box-shadow: 0 3px 10px rgba(0,0,0,0.1);
        }
        
        .card h3 {
            color: #5a2e0f;
            font-size: 22px;
            margin-bottom: 15px;
            border-left: 5px solid #f5b042;
            padding-left: 12px;
        }
        
        .product-list {
            display: grid;
            grid-template-columns: repeat(2, 1fr);
            gap: 12px;
            margin-top: 10px;
        }
        
        .product-item {
            background: #f9f2e9;
            padding: 12px 8px;
            border-radius: 12px;
            text-align: center;
            font-size: 16px;
            font-weight: 500;
            color: #333;
            border: 1px solid #e0d3c4;
        }
        
        .btn {
            background: #5a2e0f;
            color: white;
            padding: 15px 25px;
            border: none;
            border-radius: 50px;
            font-size: 18px;
            font-weight: 600;
            width: 100%;
            cursor: pointer;
            box-shadow: 0 4px 10px rgba(90,46,15,0.3);
            transition: 0.3s;
        }
        
        .btn:hover {
            background: #7a3e12;
        }
        
        .btn-whatsapp {
            background: #25D366;
            box-shadow: 0 4px 10px rgba(37,211,102,0.3);
        }
        
        .address {
            background: #e8d9cc;
            padding: 15px;
            border-radius: 12px;
            margin-top: 10px;
            font-size: 16px;
            line-height: 1.6;
        }
        
        .footer {
            text-align: center;
            padding: 20px;
            color: #7a5a3e;
            font-size: 14px;
        }
        
        .upi-card {
            background: linear-gradient(145deg, #1e3a8a, #152a5e);
            color: white;
        }
        
        .upi-id {
            background: rgba(255,255,255,0.2);
            padding: 15px;
            border-radius: 12px;
            text-align: center;
            font-size: 18px;
            margin: 15px 0;
            word-break: break-all;
            font-weight: 500;
        }
        
        .copy-btn {
            background: rgba(255,255,255,0.2);
            border: 1px solid white;
            color: white;
            padding: 12px;
            border-radius: 30px;
            width: 100%;
            font-size: 16px;
            cursor: pointer;
        }
    </style>
</head>
<body>

    <div class="header">
        <h1>🪔 KHODIYAR JP</h1>
        <p>Fresh Kirana & Premium Chocolates</p>
    </div>

    <div class="card">
        <h3>📦 Our Products</h3>
        <div class="product-list">
            <div class="product-item">🍚 Rice</div>
            <div class="product-item">🌾 Wheat Flour</div>
            <div class="product-item">🧂 Sugar</div>
            <div class="product-item">🫘 Toor Dal</div>
            <div class="product-item">🟢 Moong Dal</div>
            <div class="product-item">🫒 Oil</div>
            <div class="product-item">🍵 Tea</div>
            <div class="product-item">🥛 Milk</div>
            <div class="product-item">🍪 Biscuits</div>
            <div class="product-item">🍫 Chocolates</div>
            <div class="product-item">🥔 Chips</div>
            <div class="product-item">🥤 Cold Drinks</div>
            <div class="product-item">🧼 Soap</div>
            <div class="product-item">🧴 Shampoo</div>
            <div class="product-item">🧂 Salt</div>
            <div class="product-item">🌶️ Spices</div>
        </div>
    </div>

    <div class="card upi-card">
        <h3 style="color: white; border-left-color: #f5b042;">💰 UPI Payment</h3>
        <div style="display: flex; align-items: center; gap: 10px; margin: 15px 0;">
            <span style="background: #00baf2; padding: 5px 15px; border-radius: 20px;">Paytm</span>
            <span>UPI</span>
        </div>
        <div style="font-size: 20px; font-weight: 600;">Jayeshkumar Popatsinh</div>
        <div style="font-size: 24px; margin: 10px 0;">📱 6351641986</div>
        <div class="upi-id">paytmqr1p1ugeko5m@paytm</div>
        <button class="copy-btn" onclick="copyUpi()">📋 कॉपी UPI ID</button>
    </div>

    <div class="card">
        <h3>📲 Order on WhatsApp</h3>
        <p style="margin: 15px 0; font-size: 16px;">Click below to place your order directly on WhatsApp</p>
        <a href="https://wa.me/916351641986" style="text-decoration: none;">
            <button class="btn btn-whatsapp">💬 WhatsApp Order</button>
        </a>
    </div>

    <div class="card">
        <h3>📍 Address</h3>
        <div class="address">
            <p>🏠 Rajpur, Gambhoi</p>
            <p>🗺️ Himatnagar, Gujarat</p>
            <p>📌 PIN: 383030</p>
        </div>
        <a href="tel:916351641986" style="text-decoration: none;">
            <button class="btn" style="margin-top: 15px;">📞 Call Now</button>
        </a>
    </div>

    <div class="footer">
        <p>© 2026 Khodiyar JP Parlour</p>
        <p>All rights reserved</p>
    </div>

    <script>
        function copyUpi() {
            const upiId = "paytmqr1p1ugeko5m@paytm";
            navigator.clipboard.writeText(upiId).then(() => {
                alert("✅ UPI ID copied: " + upiId);
            }).catch(() => {
                alert("❌ Failed to copy");
            });
        }
    </script>

</body>
</html>
```

---

4. AndroidManifest.xml

```xml
<?xml version="1.0" encoding="utf-8"?>
<manifest xmlns:android="http://schemas.android.com/apk/res/android"
    package="com.khodiyar.app">

    <uses-permission android:name="android.permission.INTERNET" />
    <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />

    <application
        android:allowBackup="true"
        android:icon="@mipmap/ic_launcher"
        android:label="@string/app_name"
        android:roundIcon="@mipmap/ic_launcher_round"
        android:supportsRtl="true"
        android:theme="@style/Theme.Khodiyar"
        android:usesCleartextTraffic="true">
        
        <activity
            android:name=".MainActivity"
            android:configChanges="orientation|screenSize|keyboardHidden"
            android:exported="true"
            android:screenOrientation="portrait">
            <intent-filter>
                <action android:name="android.intent.action.MAIN" />
                <category android:name="android.intent.category.LAUNCHER" />
            </intent-filter>
        </activity>
    </application>

</manifest>
```

---

5. strings.xml

```xml
<resources>
    <string name="app_name">Khodiyar JP Parlour</string>
</resources>
```

---

6. colors.xml

```xml
<?xml version="1.0" encoding="utf-8"?>
<resources>
    <color name="primary">#5a2e0f</color>
    <color name="primary_dark">#3e1f0a</color>
    <color name="accent">#f5b042</color>
    <color name="white">#ffffff</color>
</resources>
```

---

7. themes.xml

```xml
<resources xmlns:tools="http://schemas.android.com/tools">
    <style name="Theme.Khodiyar" parent="Theme.AppCompat.Light.NoActionBar">
        <item name="colorPrimary">@color/primary</item>
        <item name="colorPrimaryDark">@color/primary_dark</item>
        <item name="colorAccent">@color/accent</item>
        <item name="android:windowBackground">@color/white</item>
        <item name="android:statusBarColor">@color/primary_dark</item>
    </style>
</resources>
```

---

8. app/build.gradle

```gradle
plugins {
    id 'com.android.application'
}

android {
    namespace 'com.khodiyar.app'
    compileSdk 34

    defaultConfig {
        applicationId "com.khodiyar.app"
        minSdk 21
        targetSdk 34
        versionCode 1
        versionName "1.0"
    }

    buildTypes {
        release {
            minifyEnabled false
            proguardFiles getDefaultProguardFile('proguard-android-optimize.txt'), 'proguard-rules.pro'
        }
    }
}

dependencies {
    implementation 'androidx.appcompat:appcompat:1.6.1'
    implementation 'com.google.android.material:material:1.11.0'
}
```

---

9. project/build.gradle

```gradle
plugins {
    id 'com.android.application' version '8.2.0' apply false
    id 'com.android.library' version '8.2.0' apply false
}
```

---

10. settings.gradle

```gradle
pluginManagement {
    repositories {
        google()
        mavenCentral()
        gradlePluginPortal()
    }
}
dependencyResolutionManagement {
    repositoriesMode.set(RepositoriesMode.FAIL_ON_PROJECT_REPOS)
    repositories {
        google()
        mavenCentral()
    }
}

rootProject.name = "Khodiyar JP Parlour"
include ':app'
```

---

11. gradle-wrapper.properties

```
distributionBase=GRADLE_USER_HOME
distributionPath=wrapper/dists
distributionUrl=https\://services.gradle.org/distributions/gradle-8.2-bin.zip
zipStoreBase=GRADLE_USER_HOME
zipStorePath=wrapper/dists
```

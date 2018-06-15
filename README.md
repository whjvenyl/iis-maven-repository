# Hosting Maven Repository on IIS
Upload Android AAR file to a local **Maven repository** and host the Maven repository on **IIS**.

## How to Use
### Maven repository
Create an empty folder and share it local network.

![shared folder](http://www.codepool.biz/wp-content/uploads/2018/06/shared-folder.PNG)

Edit the security and add **Everyone**.

![permission for shared folder](http://www.codepool.biz/wp-content/uploads/2018/06/iis-shared-everyone.PNG)

Import **library** to **Android Studio**.
Open library\dcs\maven-publish.gradle, and replace  ```repository(url: 'file:\\\\DESKTOP-3PCHU10\\site\\')``` with your path.

Build and upload your AAR file to the target folder.

Host the repository on IIS with **web.config**.

Run [Ngrok](https://ngrok.com/download) to get a random URL:

```
ngrok http 80 
```

![ngrok](http://www.codepool.biz/wp-content/uploads/2018/06/iis-ngrok.PNG)


### Test
Import **MavenTest** to **Android Studio**.

Add the Maven repository to **MavenTest\build.gradle**:

```
allprojects {
    repositories {
        google()
        jcenter()
        maven{
            url 'https://727eb58a.ngrok.io'
        }
    }
}

```

Open **app\build.gradle** to add the dependency **com.dynamsoft:dcs:1.0**:

```
dependencies {
    implementation 'com.dynamsoft:dcs:1.0'
}

```

Build and run the app.

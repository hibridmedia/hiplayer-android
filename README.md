

**HibridPlayer**

Documentation





**Optional (Setup a new project)**

In Android Studio, create a new project of type **Empty Activity.**

If your project is already created, you can skip this step.

Our player works with both Kotlin and Java. Yet, you will need to note which language you

are using for later reference.

For the Android Minimum SDK, choose API 21. Earlier APIs can also be supported if needed.

When done, click Finish to create the project.





**Import the .AAR library in the project needed as following**

\1. Within your project, create a new module

(usually File -> New -> New Module) and

select “Import JAR/AAR Package”

\2. Click Next





**Select the AAR**

\1. Select the HibridPlayer.aar file

\2. Click on **Import** / **Finish** and wait till the

gradle build ends





**After Importing**

●

●

Within your project view (in Android

Studio), you should be able to see the

module **HibridPlayer**

This means that the code was imported

successfully





**Get the name of the library**

Open the build.gradle file inside the imported module

Search for the line that looks like:

artifacts.add("default", file(**'HibridPlayer**.aar'))

Note the name of the file (HibridPlayer) in this case.





**Add the dependencies to the app/gradle under the dependencies tag as shown in the**

**screenshot**

Open the build.gradle file under the app folder and add the below dependencies

dependencies {

implementation project("**:HibridPlayer**")

implementation 'com.google.android.exoplayer:exoplayer:2.12.1'

implementation 'com.google.android.gms:play-services-analytics:17.0.0'

implementation 'com.google.ads.interactivemedia.v3:interactivemedia:3.21.4'

implementation 'com.google.android.exoplayer:extension-ima:2.12.1'

implementation "org.jetbrains.kotlin:kotlin-stdlib-jdk7:1.4.10"

}

Change the entry **HibridPlayer** to whatever the file was named (from previous step)

Click on **Sync Now** to sync the project gradle





**Include the hibrid player in the activity layout**

\1. Add the below snippet within the project

activity layout to include the HibridPlayer

layout.

<include

layout="@layout/hibrid\_player"

android:id="@+id/includeLayout"

/>





**To Disable the activity to restart on orientation**

Add the below snippet into the application

manifest file inside the <activity> tag for proper

player orientation handling.

Need to add the below in the app manifest as in

the screenshot in the activity level

android:configChanges="keyboardHidden|orient

ation|screenSize"





**Extend HibridApplication**

**If you are using an application: (Screenshot 1)**

\1. In your application file, import HibridApplication

import app.hibrid.hibridplayer.Utils.HibridApplication

\1. Set your class to extend HibridApplication

If using an application

**If you are not using an application:**

Open the app manifest and edit the application name attribute to

the following:

android:name="app.hibrid.hibridplayer.Utils.HibridApplication"

If not using an application





**Add the HibridPlayer Player to the activity using Java (if using Kotlin, check next**

**slide)**

HibridApplication app = (HibridApplication) getApplication();

HibridPlayerSettings settings = new HibridPlayerSettings(

withIma(boolean),

withDai(boolean),

"imaURL",

"assetKey",

"apiKey",

autoplay(boolean),

"baseUrl",

"channelKey");

HibridPlayer player = new HibridPlayer(this,settings,findViewById(R.id.includeLayout),app);





**Add the HibridPlayer Player to the activity using Kotlin**

val myApplication = application as HibridApplication

val settings = HibridPlayerSettings(

channelKey = "key",

autoplay = true,

daiAssetKey = "assetkey",

daiApiKey = "apikey",

imaUrl = "imaURl",

withIma = true,

withDai = true,

baseUrl = "baseUrl"

)

HibridPlayer(

context = this,

hibridSettings = settings,

includeLayout = includeLayout,

application = myApplication

)





**Extend the HibridActivity instead of AppCompatActivity**

Set your activity to extend HibridActivity instead of

AppCompatActivity to get the player into your

activity.

The HibridActivity will handle to

pause/resume/destroy the player upon the activity

life cycle plus will have listeners for the volume and

orientation change.


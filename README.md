

<h1>HibridPlayer</h1>
<br>
<h2>Documentation</h2>
<br>

<h3>Optional (Setup a new project)</h3>

In Android Studio, create a new project of type **Empty Activity.**

If your project is already created, you can skip this step.

Our player works with both Kotlin and Java. Yet, you will need to note which language you are using for later reference.

For the Android Minimum SDK, choose API 21. Earlier APIs can also be supported if needed. When done, click Finish to create the project.

<br>


[comment]: <> (![alt text]&#40;https://github.com/hibridmedia/hiplayer-android/edit/main/readmeimages/1.png&#41;)



**Import the .AAR library in the project needed as following**

* Within your project, create a new directory and copy to it the  HibridPlayer.aar file”

<br>


<h3>Add the dependencies to the app/gradle under the dependencies tag as shown in the screenshot</h3>

 Open the build.gradle file under the app folder and add the below dependencies

dependencies {

	implementation files('../libs/HibridPlayer.aar')

	implementation 'com.google.android.exoplayer:exoplayer:2.18.1'

	implementation 'com.google.android.gms:play-services-analytics:18.0.2'

	implementation 'com.google.ads.interactivemedia.v3:interactivemedia:3.28.2'

	implementation 'com.google.android.exoplayer:extension-ima:2.18.1'

	implementation "org.jetbrains.kotlin:kotlin-stdlib-jdk7:1.6.0"

}

Change the entry **HibridPlayer** to whatever the file was named (from previous step)

Click on **Sync Now** to sync the project gradle


<br>
<br>


<h3>Include the hibrid player in the activity layout</h3>

Add the below snippet within the projectactivity layout to include the HibridPlayer layout.

    <app.hibrid.hibridplayer.view.HibridPlayerView
        android:id="@+id/id"
        android:layout_width="0dp"
        android:layout_height="0dp"
        app:autoPlay="true|false"
        app:channelKey="<CHannelKeyName>"
        app:lisence="<API-KEY>"
         />

<br><br>

<h3>To Disable the activity to restart on orientation</h3>

Add the below snippet into the application manifest file inside the <activity> tag for prope player orientation handling.Need to add the below in the app manifest as in the screenshot in the activity level

	android:configChanges="keyboardHidden|orientation|screenSize"

<h3>Extend HibridApplication</h3>

**If you are using an application: 

- In your application file, import HibridApplication

	import app.hibrid.hibridplayer.Utils.HibridApplication

-  Set your class to extend HibridApplication

**If you are not using an application: Open the app manifest and edit the application name attribute to the following:**

	android:name="app.hibrid.hibridplayer.Utils.HibridApplication"

<br><br>

<br>

<h3>Extend the HibridActivity instead of AppCompatActivity or HibridFragment instead of Fragment()</h3>

Set your activity to extend **HibridActivity** instead of AppCompatActivity to get the player into your activity.
Set your activity to extend **HibridFragment** instead of Fragment to get the player into your fragment.
The HibridActivity/HibridFragment will handle to pause/resume/destroy the player upon the activity life cycle plus will have listeners for the volume and orientation change.

> Hibrid Player 

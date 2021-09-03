

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


![alt text](https://github.com/hibridmedia/hiplayer-android/edit/main/readmeimages/1.png)



**Import the .AAR library in the project needed as following**

* Within your project, create a new module (usually File -> New -> New Module) and select “Import JAR/AAR Package”

* Click Next

<br>

<h3>Select the AAR</h3>

* Select the HibridPlayer.aar file

* Click on **Import** / **Finish** and wait till thegradle build ends

<br>

<h3>After Importing</h3>


Within your project view (in Android Studio), you should be able to see the module **HibridPlayer**

This means that the code was imported successfully

<br>

<h3>Get the name of the library</h3>

Open the build.gradle file inside the imported module Search for the line that looks like:

artifacts.add("default", file(**'HibridPlayer**.aar'))

Note the name of the file (HibridPlayer) in this case.

<br>

<h3>Add the dependencies to the app/gradle under the dependencies tag as shown in the screenshot</h3>

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


<br>
<br>


<h3>Include the hibrid player in the activity layout</h3>

Add the below snippet within the projectactivity layout to include the HibridPlayer layout.

	<include layout="@layout/hibrid_player"
	android:id="@+id/includeLayout"
	/>


<br><br>

<h3>To Disable the activity to restart on orientation</h3>

Add the below snippet into the application manifest file inside the <activity> tag for prope player orientation handling.Need to add the below in the app manifest as in the screenshot in the activity level

	android:configChanges="keyboardHidden|orientation|screenSize"


<h3>Extend HibridApplication</h3>

**If you are using an application: (Screenshot 1)**

- In your application file, import HibridApplication

	import app.hibrid.hibridplayer.Utils.HibridApplication

-  Set your class to extend HibridApplication

**If you are not using an application: Open the app manifest and edit the application name attribute to the following:**

	android:name="app.hibrid.hibridplayer.Utils.HibridApplication"



<br><br>
	
<h3>Add the HibridPlayer Player to the activity using Java (if using Kotlin, check next slide)</h3>

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



<br>

	<h3>Add the HibridPlayer Player to the activity using Kotlin</h3>

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


<br>


<h3>Extend the HibridActivity instead of AppCompatActivity</h3>

Set your activity to extend **HibridActivity** instead of AppCompatActivity to get the player into your activity.

The HibridActivity will handle to pause/resume/destroy the player upon the activity life cycle plus will have listeners for the volume and orientation change.

> Hibrid Player 


MoEngage Documentation for Android.
==================================

Adding Jar file to the Android project
--------------------------------------

Add the given MoEngage-Android-SDK.jar file to the project, by copying
the jar file to the libs folder. If there is no libs folder please
create a libs folder. Make sure that you have the latest android support
jar file (android-support-v4.jar) accessable to the project.

Push Registration
-----------------

create a Google API project :

1. Open the `Google Developers Console`_.
2. If you havenÕt created an API project yet, click Create Project.
3. Supply a project name and click Create.
4. Once the project has been created, a page appears that displays your
   project ID and project number. For example, Project Number:
   670330094152.
5. Copy down your project number. You will use it later on as the GCM
   sender ID.

Enabling the GCM Service

1. In the sidebar on the left, select APIs & auth.
2. In the displayed list of APIs, turn the Google Cloud Messaging for
   Android toggle to ON.

Obtaining an API Key

1. In the sidebar on the left, select APIs & auth > Credentials.
2. Under Public API access, click Create new key.
3. In the Create a new key dialog, click Server key.
4. In the resulting configuration dialog, leave the box empty and Click
   Create.
5. In the refreshed page, copy the API key and send it to us.

Change the manifest file
------------------------

To enable push notifications, add the following lines to your manifest
file by replacing PACKAGE\_NAME with your package name, you have to
replace the package name 3 times.

::

    <permission android:name="PACKAGE_NAME.permission.C2D_MESSAGE" android:protectionLevel="signature" />
    <uses-permission android:name="PACKAGE_NAME.permission.C2D_MESSAGE" /> 
    <uses-permission android:name="com.google.android.c2dm.permission.RECEIVE" />
    <uses-permission android:name="android.permission.GET_ACCOUNTS" />
    <uses-permission android:name="android.permission.WAKE_LOCK"/>

    <receiver android:name="com.moe.pushlibrary.PushGcmBroadcastReceiver"
            android:permission="com.google.android.c2dm.permission.SEND" >
            <intent-filter>
                <action android:name="com.google.android.c2dm.intent.RECEIVE" />
                <action android:name="com.google.android.c2dm.intent.REGISTRATION" />
                <category android:name="PACKAGE_NAME" />
            </intent-filter>
    </receiver>
    <service android:name="com.moe.pushlibrary.PushGCMIntentService" />
    <receiver android:name="com.moe.pushlibrary.PushGcmRegister" />
    <receiver android:name="com.moe.pushlibrary.SendReport" />

To add Install Attribution (User Acquisition Source) tracking, add the
following lines

::

    <receiver android:name="com.moe.pushlibrary.InstallReceiver">
        <intent-filter>
            <action android:name="com.android.vending.INSTALL_REFERRER"/>
            </intent-filter>
    </receiver>

Gcm ids are refreshed after every update, to handle that please put the
following code, note that the PACKAGE\_NAME has to be replaced with your
app pakage name.

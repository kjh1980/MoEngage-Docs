
Android Integration guide
=========================

Installing the MoEngage library - Eclipse
-----------------------------------------

Step 1 - Get the latest MoEngage library release
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

You must have received the latest MoEngage SDK from the team. If you have received the SDK, please proceed to the next steps.

Step 2 - Import the SDK into your project's workspace
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Add the given MoEngage-Android-SDK.jar file to the project, by copying the jar file to the libs folder. If there is no libs folder please
create a libs folder.

Make sure that you have the latest android support jar file (android-support-v4.jar) accessable to the project.

Step 3 - Add permissions to your AndroidManifest.xml

In order for the library to work, you need to ensure that you're requesting the following permissions in your AndroidManifest.xml:

::

    <!--
    This permission is required to allow the application to send
    user events and attributes to MoEngage.
    -->
    <uses-permission
      android:name="android.permission.INTERNET" />
    
    <!--
      This permission is optional but recommended so we can be smart
      about when to send data.
     -->
    <uses-permission
      android:name="android.permission.ACCESS_NETWORK_STATE" />

At this point, you're ready to use the MoEngage SDK inside Eclipse!

Setting up Push Notifications through GCM
----------------------------------------

Step 1 - Create a Google API project
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

1. Open the `Google Developers Console`_.
2. If you havenÕt created an API project yet, click Create Project.
3. Supply a project name and click Create.
4. Once the project has been created, a page appears that displays your
   project ID and project number. For example, Project Number:
   670330094152.
5. Copy down your project number. You will use it later on as the GCM
   sender ID.
   
.. _Google Developers Console: https://cloud.google.com/console

Step 2 - Enabling the GCM Service
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

1. In the sidebar on the left, select APIs & auth.
2. In the displayed list of APIs, turn the Google Cloud Messaging for
   Android toggle to ON.

Step 3 - Obtaining an API Key
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

1. In the sidebar on the left, select APIs & auth > Credentials.
2. Under Public API access, click Create new key.
3. In the Create a new key dialog, click Server key.
4. In the resulting configuration dialog, leave the box empty and Click
   Create.
5. In the refreshed page, copy the API key and send it to us.

Handling Push Notifications
---------------------------

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

Gcm ids are refreshed after every update, to handle that please put the
following code, note that the PACKAGE\_NAME has to be replaced with your
app package name.

::

    <receiver android:name="com.moe.pushlibrary.PushUpdateReceiver">
    <intent-filter>
            <action android:name="android.intent.action.PACKAGE_REPLACED" />
            <data android:path="PACKAGE_NAME"
                android:scheme="package" />
        </intent-filter>
    </receiver>

Initializing the SDK and Push Notifications
-------------------------------------------

Put the following code in the first activity onCreate() method

::

    MoEHelper mHelper = new MoEHelper(this);
    mHelper.initialize("GCM Sender ID", "MoEngage APP ID");

GCM Sender ID - the ID of the project created as part of Push Registration
MoEngage APP ID - This is an application specific id, which MoEngage team must have shared with you.

Put the following code after the above initialization code to register for push

::

    mHelper.Register(drawableResourceId);
    drawableResourceId - for eg. R.drawable.icon



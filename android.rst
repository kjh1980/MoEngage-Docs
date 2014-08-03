
Android Integration guide
=========================

Installing the MoEngage library - Eclipse
-----------------------------------------

Step 1 - Get the latest MoEngage library release
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

You must have received the latest MoEngage SDK from the team. If you have received the SDK, please proceed to the next steps.

Step 2 - Import the SDK into your project's workspace
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Add the given MoEngage-Android-SDK.jar file to the project, by copying the jar file to the libs folder. If there is no libs folder please
create a libs folder.

*Make sure that you have the latest android support jar file (android-support-v4.jar) accessable to the project.*

Step 3 - Add permissions to your AndroidManifest.xml
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

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

This covers a quick-start guide for setting up push for your Android app that covers setting up your Google API project,
locating the your project number, uploading your Google API Project key to MoEngage portal.

Step 1 - Enabling Google Cloud Messaging (GCM) in your Google API Console
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

To enable Google Cloud Messaging (GCM) for Android, there are a few preliminary steps that must be taken.
You will first need to turn on the Google Cloud Messaging Services from `Google's API Console page`_.
If you do you not have a Google API project yet, the following pop up will appear prompting you to create a project.

.. image:: images/1.png

Click on the "Create Project..." to create a new project. Once you have created a new project (or if you already have an existing project),
you will be taken to the console's dashboard.

Once the project has been created, a page appears that displays your project ID and project number. The project number will be your
twelve digit GCM Sender ID, which you will need to use in your code later to register your application for push notifications.

From the Google API Console page, select "Services" from the left-hand navigation. Find "Google Cloud Messaging for Android" in the list of services,
and turn it on by clicking the switch in the "Status" column.

.. image:: images/2.png

Create an Google API key. From the Google API Console page, select "Public API Access" from the left navigation and click "Create new Server key...". You should see the following pop up.

.. image:: images/3.png

Click the create button. The next page will contain a "Simple API Access" header, and below the header a "Key for server apps" box.
Your Google API key will appear in this box, after the heading "API Key:".

.. image:: images/4.png

.. _Google's API Console page: https://cloud.google.com/console

Step 2 - Uploading your GCM API Key through MoEngage portal
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

In order for MoEngage to send Google Cloud Messaging notifications on your behalf, you will need to enter the
Google API key generated from the last step through MoEngage portal. To upload it, log in to your MoEngage account provided by the team
and click the Settings button (with the gear icon) on the top-right corner of the screen as shown below:

.. image:: images/5.png

In the Settings page, click on the "App settings" tab. Then paste in your Google API key into the text field that appears for GCM key.
Click the "Save" button underneath the text fields to confirm.

.. image:: images/6.png




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

GCM Sender ID - the twelve digit sender ID of your Google API project.
MoEngage APP ID - This is an application specific id, which MoEngage team must have shared with you. You can also find it in the 'App Settings' tab of the 'Settings' page of your MoEngage account.

Put the following code after the above initialization code to register for push

::

    mHelper.Register(drawableResourceId);
    drawableResourceId - for eg. R.drawable.icon


Send a push notification for testing
------------------------------------

Once you have set up your permissions and set up GCMReciever as a receiver of Google Cloud Messaging notifications in your AndroidManifest.xml file and
added the initialization code mentioned above, you're ready to send a notification!

Install and run your application on an Android device (not the emulator, it can't receive notifications).
Make sure to run the app until the calls to the initialization code mentioned above has been run. For apps built
according to our recommendations, these calls are in the onCreate method of your main application activity, so it is enough to simply open the app. Press the back button to close your app.

Now log in to your MoEngage account and select `Create Campaign`_ from the left-hand navigation, and click on 'General Push Campaign'.

.. _Create Campaign: http://app.moengage.com/newpushcampaign

If this is the first time you are testing MoEngage SDK with your app, you can just set a test message, leave the screen selection part, set the scheduling to run 'as soon as possible' and create the campaign as shown below:

.. image:: images/7.png

.. image:: images/8.png

.. image:: images/9.png

Once the campaign is created, the message should show up on your device.

.. image:: images/10.png

*Note: If MoEngage SDK has been integrated earlier with your app and has been released to your users, please don't create a campaign targeting all users. You can create a campaign targeting only your device by setting the filters based on user attributes.*







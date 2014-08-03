
Windows Phone Integration guide
===============================

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


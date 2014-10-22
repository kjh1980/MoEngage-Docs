
iOS Integration guide
===============================

Importing the MoEngage library 
-----------------------------------------

Step 1 - Get the latest MoEngage library release
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

You must have received the latest MoEngage SDK from the team. If you have received the SDK, please proceed to the next steps. If not, please contact MoEngage team for help.

Step 2 - Adding library and header files to the project 
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Add the given library file (.a extension) to your project. Please check the following page for instructions.
https://developer.apple.com/library/ios/technotes/iOSStaticLibraries/Articles/configuration.html

Add the given header files (.h extensions) , by dragging and dropping the files in to your project.

After these 2 steps you are all set to use the MoEngage Library now.

App Delegate Changes
----------------------
In your AppDelegate.m add the following code in the respective methods..

ApplicationID - a unique id will be provided to you from MoEngage. You can also find it in the 'App Settings' tab of the 'Settings' page of your MoEngage account.

::

	- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions 
	{
    		[[MoEngage sharedInstance] initializeWithApiKey:@"ApplicationID" inApplication:application withLaunchOptions:launchOptions];
    		return YES;
	}

	- (void)applicationDidEnterBackground:(UIApplication *)application {
    		[[MoEngage sharedInstance] stop:application];
	}

	- (void)applicationDidBecomeActive:(UIApplication *)application {
    		[[MoEngage sharedInstance]applicationBecameActiveinApplication:application];
	}

	- (void)applicationWillTerminate:(UIApplication *)application {
		[[MoEngage sharedInstance]applicationTerminated:application];
	}

	- (void) application:(UIApplication *)application didReceiveRemoteNotification:(NSDictionary *)userInfo 
	{
    		[[MoEngage sharedInstance]didReceieveNotificationinApplication:application withInfo:userInfo];
	}

	- (void)application:(UIApplication*)application didRegisterForRemoteNotificationsWithDeviceToken:(NSData*)deviceToken
	{
    		[[MoEngage sharedInstance]registerForPush:deviceToken];
	}


Tracking your first event
-------------------------

You can track an event using trackEvent with the event name and it's characteristics (attributes).

Every event has 2 attributes, action name and key, value pairs as NSMutableDictionary which stores additional information about the action. Add all the additional information which you think would be useful for segmentation while creating campaigns.
For eg. the following code tracks a purchase event of a product. We are including attributes like product, category which describe the event we are tracking.

::


    NSMutableDictionary* mut_dict = [NSMutableDictionary dictionaryWithDictionary:@{@"product":@"Moto E",@"category":@"Mobiles"}];
    [[MoEngage sharedInstance]trackEvent:@"Made Purchase" andPayload:mut_dict];

If you don't have any attributes, just pass nil as second argument. for eg.

::

    [[MoEngage sharedInstance]trackEvent:@"Made Purchase" andPayload:nil];
    


To pass location as key value pairs, Use the following approach

for eg. event name is "loaction_search", where we have to pass "loc" as additional information with values as latitude and longitude of the location.

::
    NSMutableDictionary *mut_dict = [[NSMutableDictionary alloc]init];
    [MoEngage setLocationwithLat:79.3249 lng:32.328 withName:@"loc" inDictionary:mut_dict];
    [[MoEngage sharedInstance]trackEvent:@"location_search" andPayload:mut_dict];

*Please make sure that you are tracking event attributes without changing their data types. For instance, in the above purchase event, amount and quantity are tracked in the numeric form. Our system detects the data type automatically unless you explicitly specify it as a string.*

*You should track all the events relevant to your business, so that your product managers and marketers can segment your app users and create targeted campaigns.*



Testing event tracking after integration
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

To test event tracking, first you need to login to the MoEngage portal with the credentials provided for your app.

After adding event tracking in the app as shown in the guide above, you can visit `For Developers`_ link through the MoEngage portal to check whether the events are being tracked, as you use.

.. _For Developers: http://app.moengage.com/latestActivity

.. image:: images/11.png

As users use the application, events data is stored locally and sent as a batch at app close or termination to avoid any performance impact. So, you should close or terminate the app to see the events in the portal.



Setting user attributes
-------------------------

Use the following lines to set User attributes like Name, Email, Mobile, Gender, etc.

For eg. to set unique id for the user

::

    [[MoEngage sharedInstance]setUserAttribute:uniqueId forKey:USER_ATTRIBUTE_UNIQUE_ID];
    
uniqueId - unique id for the user specific to your system, so that there is a unique identifier mapping between your platform and MoEngage.

You can also set the default user attributes like mobile number, gender, user name, brithday. Birthday has to be in the format - "mm/dd/yyyy". The constants for these default attributes in MoEHelperConstants are mentioned below:

::

    USER_ATTRIBUTE_UNIQUE_ID
    USER_ATTRIBUTE_USER_EMAIL
    USER_ATTRIBUTE_USER_MOBILE
    USER_ATTRIBUTE_USER_NAME   # incase you have full name 
    USER_ATTRIBUTE_USER_GENDER
    USER_ATTRIBUTE_USER_FIRST_NAME # incase you have first and last name separately
    USER_ATTRIBUTE_USER_LAST_NAME
    USER_ATTRIBUTE_USER_BDAY
    GENDER_MALE = "male";
    GENDER_FEMALE = "female";

for eg. to set email attribute for a user

::

    [[MoEngage sharedInstance]setUserAttribute:email forKey:USER_ATTRIBUTE_USER_EMAIL];
    
email - email of the user

To set user location, use the following syntax

::

    [[MoEngage sharedInstance] setUserLocationwithLatitude:lat withLongitude:lng];

lat - latitude of the location
lng - longitude of the location

Setting custom user attributes
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The above examples demonstrate how to set predefined attributes and their values. To set custom attributes use the following syntax.

::

    [[MoEngage sharedInstance]setUserAttribute:value forKey:key];

key - the name you want to give to the attribute
value - the value you would like to assign to it


Setting user attributes for existing registered users
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

This applies if your app has been live and has users using before integrating MoEngage. We recommend you to set the attributes for existing registered users who
have been using your app when they use after updating to the app with MoEngage SDK.

You can do this by writing the user attributes setting code (mentioned earlier) in the first screen existing users see after updating the app.

This helps your product/marketing team to target based on the attributes of all users who use the updated app.

Push Notifications
-----------------------------------------

If you already have production and development key file and certificate files, Proceed to Uploading Key file to MoEngage section.


.. image:: images/apns1.png



Uploading Key file to MoEngage
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

1. Select the environment , sandbox or production
2. Upload the pem file which contains both certificate and key information.
3. Enter the password for the key.

.. image:: images/apns20.png

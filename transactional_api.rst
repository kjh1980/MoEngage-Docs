
Transactional API Integration guide
===============================

Transactional API can be used to send push to your users individually, like targeting based on the activity they did in the past or targeting based on the unique parameters the user has like a unique user Id or email or mobile number. If you would like to target multiple people, you can use the campaigns feature provided to you in the dashboard.

How to make the API call.
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

API call is a POST method, and the end url is mentioned below. 

::

    http://runcampaigns.moengage.com/v1/notifyUser

Headers for the call

::

    'Content-Type':'application/json'

Parameters necessary for the API call should be passed as JSON object string as part of request body.

Required parameters

::

    appId (*) - Unique Id that MoEngage has shared with you.
    target (*) - value can be either "action" or "user".
    screenName (*) - the screen you want to take the user to after he clicks on push notification. This is a JSON object with the keys as the platforms you would like to target, along with values as the full activity name or xaml file name.
    ttl (*) - time to live value in seconds
    title (*) - title of the push
    message (*) - message for the push

Optioinal parameters

::

    data - JSON object that is used to extra key value pairs for the screen that opens when user clicks on the push notification.

API call targeting a user based on the attributes
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Attributes can be either a uniqueId that your app assigns to the user or his email address.


    userId - unique id of the user, use this parameter if you want to target user based on the unique Id along with target as "user"
    userEmail - email of the user, use this parameter if you want to target user based on the email address along with target as "user"

A sample JSON object for sending it as part of request body would looke like

::

    {
    	"appId": "your app id",
    	"screenName": {"android":"com.example.moengagetest.MainActivity","windows":"Page.xaml"}
    	"ttl": 86400,
    	"message": "Hello",
    	"title": "Hi",
    	"target": "user",
    	"userId": "1234"
    }

From the above parameters, we are targeting a user with unique Id as 1234. Screen names should be available for each platform, if you do not mention the screen name for a particular platform, we will not push to the user.


API call targeting a user based on the past activity or action 
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

You will need to target the user based on the action and also based on the available attributes for that particular action.

    eventName - event or action that the user has done in the past
    attrName - attribute name associated with the event
    attrValue - attribute value for the attribute name

A sample JSON object for sending it as part of request body would looke like
::

    {
    	"appId": "QVF7UXCJO9M74NCFMVUIVFGQ",
    	"screenName": {"android":"com.example.moengagetest.MainActivity","windows":"Page.xaml"}
    	"ttl": 86400,
    	"message": "Hello",
    	"title": "Hi",
    	"target": "action",
    	"eventName": "purchased",
    	"attrName": "purchase Id",
    	"attrValue": "7854"
    }

From the above parameters, we are targeting a user who has made a purchase with purchase Id as 7854. Screen names should be available for each platform, if you do not mention the screen name for a particular platform, we will not push to the user.

Response for a successful API call
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Response will be a json object, on the sucessfull call you will receive response as {"result":"Push Sent"}

Response for Invalid API call
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

::

    "data should be provided in JSON format" - request body is not in JSON format
    "appId not found" - appId parameter not found in reqeust body
    "target not found" - target parameter not found in request body
    "target has to be either action or user" - target value is neither "user" or "action"
    "user atrributes not found" - none of the expected user attributes found like userId, userEmail
    "screenName not found" - screenName parameter not found in request body
    "ttl not found" - ttl parameter not found in request body
    "title not found" - title parameter not found in request body
    "message not found" - message parameter not found in request body
    "no user found" - couldn't find any users with the mentioned parameters

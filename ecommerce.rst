
Tracking Best Practices for E-commerce companies
================================================

From our experience working with E-commerce companies, we would like to provide best practices on tracking the events relevant to e-commerce companies, so that they can make the best use of MoEngage.

We would focus primarily on the events tracking, please make sure to go through the integration guide of any mobile platform we have. We would mention the code snippets for Android, those will be similar for iOS and Windows Phone as well.

Below are the examples of most important events to be tracked in E-commerce.

Viewing a Product Category
^^^^^^^^^^^^^^^^^^^^^^^^^^^

Category views are the most important components of a E-commerce app. You would want to track all the category views as events/actions, so that you can understand the user's interests, which would help you in better insights and targeting.

To do that, you’ll want to track an event called Viewed Product Category using a 'trackEvent' call of MoEngage SDK. You might want to track additional relevant attributes like 'results', if it's relevant for you.

::

    JSONObject newJson = new JSONObject();
    try {
      newJson.put("category", "Android Smartphones");
      newJson.put("results", 20);
    } catch (JSONException e) {
      // json exception
    }
    MoEHelper.getInstance(mCurrentContext).trackEvent("Viewed Product Category", newJson);

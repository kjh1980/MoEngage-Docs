
Tracking Best Practices for E-commerce companies
================================================

From our experience working with E-commerce companies, we would like to provide best practices on tracking the events relevant to e-commerce companies, so that they can make the best use of MoEngage.

We would focus primarily on the events tracking, please make sure to go through the integration guide of any mobile platform we have. We would mention the code snippets for Android, those will be similar for iOS and Windows Phone as well.

We recommend you to use unique recognizable event names, instead of non-descript names like 'Event 12'. We also recommend you to provide the event attributes persisting the data-types. For examples, 'price' for a 'Viewed Product' event should be numeric

Below are the examples of most important events to be tracked in E-commerce:

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

Viewing a Product
^^^^^^^^^^^^^^^^^

The second most important event to record for an Ecommerce app is 'Viewed Product'. To track that you’ll use a 'trackEvent' call like below, with additional relevant event attributes which will help your product/marketing team in segmentation:

::

    JSONObject newJson = new JSONObject();
    try {
      newJson.put("name", "Samsung Galaxy S4");
      newJson.put("price", 700);
      newJson.put("category", "Mobile Phones");
      newJson.put("subcategory", "Android Smart Phones");
      newJson.put("ID", "1720340234");
      newJson.put("sku", "234324-21");
      
    } catch (JSONException e) {
      // json exception
    }
    MoEHelper.getInstance(mCurrentContext).trackEvent("Viewed Product", newJson);

Adding and Removing from Cart
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

These events represents the interest of customers in buying a product: 'Added to Cart' and 'Removed from Cart'. One for when products are added to the customer’s shopping cart, and one for when they are removed.

The properties to record for each of these are the same as the ones for the 'Viewed Product' event above with additional relevant attributes like 'quantity' (of course you can always add more properties of your own too!).

Here’s what the tracking code would look like:

::

    JSONObject newJson = new JSONObject();
    try {
      newJson.put("name", "Samsung Galaxy S4");
      newJson.put("price", 700);
      newJson.put("category", "Mobile Phones");
      newJson.put("subcategory", "Android Smart Phones");
      newJson.put("ID", "1720340234");
      newJson.put("sku", "234324-21");
      newJson.put("quantity", 2);
    } catch (JSONException e) {
      // json exception
    }
    MoEHelper.getInstance(mCurrentContext).trackEvent("Added to Cart", newJson);
    
::

    JSONObject newJson = new JSONObject();
    try {
      newJson.put("name", "Samsung Galaxy S4");
      newJson.put("price", 700);
      newJson.put("category", "Mobile Phones");
      newJson.put("subcategory", "Android Smart Phones");
      newJson.put("ID", "1720340234");
      newJson.put("sku", "234324-21");
      newJson.put("quantity", 2);
    } catch (JSONException e) {
      // json exception
    }
    MoEHelper.getInstance(mCurrentContext).trackEvent("Removed from Cart", newJson);


Completing an Order
^^^^^^^^^^^^^^^^^^^

The final step is to track a 'Completed Order' event when people complete your checkout process. It’s the most important event to record, since you’ll use it for conversion goals, segmentation, analytics and many more.

We would recommend to include all items in the cart as event properties, with the same attributes from the previous calls, like shown in the below:

::

    JSONObject newJson = new JSONObject();
    try {
      newJson.put("orderId", "5720340234");
      newJson.put("totalvalue", 920);
      newJson.put("revenue", 900);
      newJson.put("shipping", 0);
      newJson.put("tax", 20);
      newJson.put("discount", 15);
      newJson.put("coupon", "APP15");
      newJson.put("currency", "USD");
      newJson.put("products", [productJsonObject1, productJsonObject2]);
      
    } catch (JSONException e) {
      // json exception
    }
    MoEHelper.getInstance(mCurrentContext).trackEvent("Order Completed", newJson);

Other Common Events
^^^^^^^^^^^^^^^^^^^

We covered the most common e-commerce events, but there are plenty of other things you might want to track. We would always recommend you to track the most important events relevant for your product/marketing team to segment/analyze.

Here are some common e-commerce events and properties you might want to include with each event:

::

    'Favorited/Liked/Wishlisted Product'	With properties like id, sku, category, subcategory, price, name…
    'Searched Products'	With properties like query, results…
    'Shared Product'	With properties like id, sku, category, subcategory, price, name, as well as the network they shared on, for example: Facebook, Twitter or Email.
    'Reviewed Product'	With properties like id, sku, category, subcategory, price, name, and the product rating given.
    'Filtered Products'	With properties like category, subcategory, price, size…
    'Viewed Product Reviews'	With properties like id, sku, category, subcategory, price, name, and the averageRatings and reviewCount.
    'Viewed Sale Page'	With properties like campaign and coupon. Using the page method.
    'Started Order'	With properties like orderId and an array of products
    'Updated Order'	With properties like orderId and an array of products
    'Viewed Checkout'	With properties like an array of products
    'Completed Checkout Step'	With properties like orderId and an array of products
    'Refunded Order'	With properties like orderId and an array of products
    'Viewed Promotion'	With properties like a promotion id, sku, category, price, name…



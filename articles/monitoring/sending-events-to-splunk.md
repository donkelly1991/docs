---
description: How to send events from Auth0 to Spunk.
topics:
  - monitoring
  - splunk
contentType:
  - how-to
useCase:
  - analyze-auth0-analytics
  - analyze-logs
  - analyze-external-analytics
  - integrate-analytics
---
# Sending Events from Auth0 to Splunk

[Splunk](http://splunk.com) provides a platform to easily get insights into all the information generated by your IT infrastructure.

This example shows how you can very easily connect Auth0 to Splunk and stream `signup` and `login` events with user contextual information.

![](/media/articles/tutorials/splunk-dataflow.png)

## Record a SignUp or Login Event in Splunk

This [Auth0 rule](/rules) uses the [Splunk REST API](http://dev.splunk.com/view/rest-api-overview/SP-CAAADP8) to record `signup` and `login` events from users to your apps. This is tracked with the `signedUp` property. If the property is present, then we assume this is a `login` event. Otherwise we assume that this event is a new `signup`.

You can send any number of properties. This sample sends contextual information like the user IP address (can be used for location), the application, the username, and so on.

Splunk's API supports basic & token based auth. For simplicity, we use basic auth, with credentials in the rule. You can store these credentials securely in Auth0 using standard settings on the dashboard.

When enabled, this rule will start sending events that will show up on Splunk's dashboard:

![](/media/articles/scenarios/splunk/splunk-dashbaord.png)

::: panel Securely Storing Credentials
This example has your Splunk credentials hard-coded into the rule, but if you prefer, you can store them instead in the `configuration` object (see the [Settings](${manage_url}/#/rules) under the list of your rules). This allows you to use those credentials in multiple rules if you require, and also prevents you from having to store them directly in the code.
:::

```js
function(user, context, callback) {
  user.app_metadata = user.app_metadata || {};
  var splunkBaseUrl = 'YOUR SPLUNK SERVER, like: https://your server:8089';

  //Add any interesting info to the event
  var event = {
    message: user.app_metadata.signedUp ? 'Login' : 'SignUp',
    application: context.clientName,
    clientIP: context.request.ip,
    protocol: context.protocol,
    userName: user.name,
    userId: user.user_id
  };

  request.post( {
    url: splunkBaseUrl + '/services/receivers/simple',
    auth: {
        'user': 'YOUR SPLUNK USER',
        'pass': 'YOUR SPLUNK PASSWORD',
      },
    json: event,
    qs: {
      'source': 'auth0',
      'sourcetype': 'auth0_activity'
    }
  }, function(e,r,b) {
    if (e) return callback(e);
    if (r.statusCode !== 200) return callback(new Error('Invalid operation'));
    user.app_metadata.signedUp = true;
    auth0.users.updateAppMetadata(user.user_id, user.app_metadata)
    .then(function(){
      callback(null, user, context);
    })
    .catch(function(err){
      callback(err);
    });
  });
}
```

::: note
Notice that if all calls are successful, we signal the user as signed up. So next time we record `login`.
:::

Check out our [repository of Auth0 Rules](https://github.com/auth0/rules) for more great examples:

* Rules for access control
* Integration with other services: [Firebase](http://firebase.com), [Rapleaf](http://rapleaf.com), [Parse](http://parse.com)
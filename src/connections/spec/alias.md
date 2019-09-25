---
title: 'Spec: Alias'
sidebar: Alias
---


The `alias` method is used to merge two user identities, effectively connecting two sets of user data as one. This is an advanced method, but it is required to manage user identities successfully in some of our destinations.

Since this is our most advanced method we have added sections to each docs page for destinations that use it:

- [KISSmetrics](/docs/integrations/kissmetrics#alias)
- [Mixpanel](/docs/integrations/mixpanel#alias)
- [Vero](/docs/integrations/vero#alias)

Here's the payload of a basic `alias` call that will associate this user's existing `id` (email address) with a new one (a database ID), with most [common fields](/docs/spec/common/) removed:

```js
{
  "type": "alias",
  "previousId": "jen@email.com",
  "userId": "507f191e81"
}
```

If you're instrumenting a website, then the Anonymous ID is generated in the browser so you'll want to call `alias` from the client-side. If you're using a server-side session ID as the Anonymous ID, then you'll want to alias from the server-side.

Here's the corresponding Javascript event that would generate the above payload. If you're using Segment's Javascript library, we'll automatically pass in the user's anonymousId as previousId for you:

```js
analytics.alias("507f191e81");
```

Beyond the common fields, the `alias` call takes the following fields:

<table>
  <tr>
    <th>**Field**</th>
    <th>**Type**</th>
    <th>**Description**</th>
  </tr>
  {% include content/spec-field-previous-id.md %}
  {% include content/spec-field-user-id.md %}
</table>


## Examples
Here's a complete example of an `alias` call:

```js
{
  "anonymousId": "507f191e810c19729de860ea",
  "channel": "browser",
  "context": {
    "ip": "8.8.8.8",
    "userAgent": "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_9_5) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/40.0.2214.115 Safari/537.36"
  },
  "integrations": {
    "All": true,
    "Mixpanel": false,
    "Salesforce": false
  },
  "messageId": "022bb90c-bbac-11e4-8dfc-aa07a5b093db",
  "previousId": "39239-239239-239239-23923",
  "receivedAt": "2015-02-23T22:28:55.387Z",
  "sentAt": "2015-02-23T22:28:55.111Z",
  "timestamp": "2015-02-23T22:28:55.111Z",
  "type": "alias",
  "userId": "507f191e81",
  "version": "1.1"
}
```

## Previous ID

The `previousId` is the existing ID you've referred to the user by. It might be an Anonymous ID assigned to that user or a User ID you previously identified them with using our [`identify`](/docs/spec/identify/) call.

## User ID

The `userId` is a string that will be the user's new identity, or an existing identity that you wish to merge with the `previousId`. See the [User ID docs](/docs/spec/identify#user-id) for more detail.
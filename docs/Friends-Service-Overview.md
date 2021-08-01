# Friends Service Overview

The Friends service maintains and suggests "friend" relationships between users. It is not the authoritative source of "users" - it identifies them using id strings provided by callers. It is not conceptually concerned with any properties of users for maintaining frienship, but may make use of such properties to make friendship _suggestions_. Similarly, it may observe events such as post creation or liking, only from the perspective of some connection between users that can be used to make friendship suggestions.

It is divided into the following three APIs:

## My API

The My API provides friend-related operations for the _calling_ user, including:

* get my friends
* get my pending friendship requests
* add a new friendship request
* delete a pending request
* get my incoming requests
* accept an incoming request
* reject an incoming request
* get friend suggestions for me

This API needs to identify the calling user using a security scheme, for example by bearer token. If the bearer token is valid, the API will extract the calling user's id from it and not validate it further. It will also not validate target user ids included in friendship requests.

## Bulk API

The bulk API is intended to be used from other services which are interested in friendships. It implements the following operations:

* get friends of user(s)

This API needs to identify the calling _application_, for example by a static api key.

## Events API

The events API represents events in the overall application that the Friends service is interested in. In the final implementation, event information may be passed around using some form of messaging. For now, the events API may be called directly by the services that source these events.

Operations:

* User(s) added
* User(s) deleted
* Post(s) added
* Post(s) liked

This API also needs to identify the calling _application_, for example by an api key.

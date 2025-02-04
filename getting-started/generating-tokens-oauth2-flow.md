---
icon: unlock-keyhole
description: The Kick OAuth Flow.
---

# Generating Tokens / OAuth2 Flow

* Authorization
* Token
* Token Refresh



## Token Types

There are 2 types of tokens that are available for the Kick Dev API: App Access Token and User Access Token. Each token has a unique OAuth flow to generate the token and are generally used in different scenarios.

### App Access Token

The App Access Token are tokens generated through the \<insert oauth flow here> flow. They are server to server API tokens and are the most basic  from of token to access the API. App Access Tokens can access publically accessible

{% swagger src="https://api.kick.com/swagger/v1/doc.json" path="/oauth/authorize" method="get" %}
[https://api.easygo-drop-kick.com/swagger/v1/doc.json](https://api.kick.com/swagger/v1/doc.json)
{% endswagger %}

{% swagger src="https://api.kick.com/swagger/v1/doc.json" path="/oauth/token" method="post" %}
[https://api.easygo-drop-kick.com/swagger/v1/doc.json](https://api.kick.com/swagger/v1/doc.json)
{% endswagger %}

{% swagger src="https://api.kick.com/swagger/v1/doc.json" path="/oauth/revoke" method="post" %}
[https://api.easygo-drop-kick.com/swagger/v1/doc.json](https://api.kick.com/swagger/v1/doc.json)
{% endswagger %}

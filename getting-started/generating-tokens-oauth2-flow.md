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

App Access Tokens are generated through the Client Credentials flow. These server-to-server API tokens are the most basic form of token for accessing the API. They can access publicly available data and are ideal for use when user login is not required.

### User Access Token

User Access Tokens are generated through the Authorization Grant Flow. These token give an application access to the users information based on the scopes the App has requested. This give more privileged information and access to an App and will often allow an App to act on the users behalf.&#x20;


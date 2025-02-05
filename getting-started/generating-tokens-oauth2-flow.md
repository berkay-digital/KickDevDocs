---
icon: unlock-keyhole
description: The Kick OAuth Flow.
---

# OAuth 2.1

## Token Types

There are 2 types of tokens that are available for the Kick Dev API: App Access Token and User Access Token. Each token has a unique OAuth flow to generate the token and are generally used in different scenarios.

### App Access Token (Not yet implemented)

App Access Tokens are generated through the Client Credentials flow. These server-to-server API tokens are the most basic form of token for accessing the API. They can access publicly available data and are ideal for use when user login is not required.

### User Access Token

User Access Tokens are generated through the Authorization Grant Flow. These token give an application access to the users information based on the scopes the App has requested. This give more privileged information and access to an App and will often allow an App to act on the users behalf.

## Kick OAuth Server

The Kick OAuth server is hosted on id.kick.com.

Information from creating an App will be required in these endpoints. Checkout the Kick Apps Setup page to get the information for your App.

{% hint style="info" %}
The host URL for our OAuth server is different from our API server.&#x20;

The Host URL is: _https://id.kick.com_
{% endhint %}



## Authorization Endpoint

<mark style="color:green;">`GET`</mark> `/oauth/token`

Directs the user to the authorization server where they can log in and approve the application's access request.

**Query Parameters**

<table><thead><tr><th width="276">Name</th><th width="128">Type</th><th>Description</th></tr></thead><tbody><tr><td><code>client_id</code></td><td>string</td><td>Your application's client id</td></tr><tr><td><code>response_type</code></td><td>string</td><td><code>code</code></td></tr><tr><td><code>redirect_url</code></td><td>uri</td><td>The URI to redirect users to after authorization</td></tr><tr><td><code>state</code></td><td>string</td><td>A random string to maintain state between the request and callback</td></tr><tr><td><code>scope</code></td><td>string</td><td>Scopes for request</td></tr><tr><td><code>code_challenge</code></td><td>string </td><td>OAuth code challenge</td></tr><tr><td><code>code_challenge_method</code></td><td>string</td><td><code>S256</code></td></tr></tbody></table>

**Response**

{% tabs %}
{% tab title="200" %}
```json
https://yourapp.com/callback?code=<code>&state=random-state
```
{% endtab %}

{% tab title="400" %}
```json
{
  "error": "Invalid request"
}
```
{% endtab %}
{% endtabs %}

#### Example Request

{% code overflow="wrap" %}
```uri
GET
https://id.kick.com/oauth/authorize?
    response_type=code&
    client_id=<your_client_id>&
    redirect_uri=<https://yourapp.com/callback>&
    scope=<scopes>&
    code_challenge=<code_challenge>&
    code_challenge_method=S256&
    state=<random_value>
```
{% endcode %}

#### Example Response

```uri
https://yourapp.com/callback?code=<code>&state=random-state
```



## Token Endpoint

<mark style="color:green;">`POST`</mark> `/oauth/token`

Exchanges the code for a valid access token and a refresh token that can be used to make authorised requests to Kick’s API.

**Body**

<table><thead><tr><th width="244">Name</th><th>Type</th><th>Description</th></tr></thead><tbody><tr><td><code>code</code></td><td>string</td><td>Code received during the Authorization Flow</td></tr><tr><td><code>client_id</code></td><td>string</td><td>Your application's client id</td></tr><tr><td><code>client_secret</code></td><td>string</td><td>You application's client secret</td></tr><tr><td><code>redirect_uri</code></td><td>string </td><td>The URI to redirect users to after authorization</td></tr><tr><td><code>grant_type</code></td><td>string</td><td><code>authorization_code</code></td></tr><tr><td><code>code_verifier</code></td><td>string</td><td>To verify PKCE challenge code created</td></tr></tbody></table>

**Response**

{% tabs %}
{% tab title="200" %}
```json
{
  "access_token": "",
  "token_type": "",
  "refresh_token": "",
  "expiry": ""
}
```
{% endtab %}

{% tab title="400" %}
```json
{
  "error": "Invalid request"
}
```
{% endtab %}
{% endtabs %}

#### Example Request

<pre><code>POST
https://id.kick.com/oauth/token

Request Form Body:
{
    grant_type=authorization_code
    client_id=&#x3C;Client_id>
    client_secret=&#x3C;Client_secret>
    redirect_uri=&#x3C;Redirect_uri>
<strong>    code_verifier=&#x3C;code_verifier>
</strong>    code=&#x3C;CODE>
}
</code></pre>

#### Example Response

```
{
  "access_token": "",
  "token_type": "",
  "refresh_token": "",
  "expiry": ""
}
```



## Refresh Token Endpoint

<mark style="color:green;">`POST`</mark> `/oauth/token`

Pass in refresh token and refresh both access and refresh codes.

**Body**

<table><thead><tr><th width="244">Name</th><th>Type</th><th>Description</th></tr></thead><tbody><tr><td><code>refresh_token</code></td><td>string</td><td>Code received during the Authorization Flow</td></tr><tr><td><code>client_id</code></td><td>string</td><td>Your application's client id</td></tr><tr><td><code>client_secret</code></td><td>string</td><td>You application's client secret</td></tr><tr><td><code>grant_type</code></td><td>string</td><td><code>refresh_token</code></td></tr></tbody></table>

**Response**

{% tabs %}
{% tab title="200" %}
```json
{
  "access_token": "",
  "token_type": "",
  "refresh_token": "",
  "expiry": ""
}
```
{% endtab %}

{% tab title="400" %}
```json
{
  "error": "Invalid request"
}
```
{% endtab %}
{% endtabs %}

#### Example Request

```
POST
https://id.kick.com/oauth/token

Request Form Body:
{
    grant_type=refresh_token
    client_id=<client_id>
    client_secret=<client_secret>r>
    refresh_token=<refresh_token>
}
```

#### Example Response

```
{
  "access_token": "",
  "token_type": "",
  "refresh_token": "",
  "expiry": ""
}
```

## Revoke Token Endpoint

<mark style="color:green;">`POST`</mark> `/oauth/revoke`

Pass in a token to revoke access to that token.

**Query**

<table><thead><tr><th width="244">Name</th><th>Type</th><th>Description</th></tr></thead><tbody><tr><td><code>token</code></td><td>string</td><td>The token to be revoked</td></tr><tr><td><code>token_hint_type</code></td><td>string</td><td><code>access_token or refresh_token</code></td></tr></tbody></table>

**Response**

{% tabs %}
{% tab title="200" %}
OK
{% endtab %}

{% tab title="400" %}
```json
{
  "error": "Invalid request"
}
```
{% endtab %}
{% endtabs %}

#### Example Request

```
POST 
https://kick.com/oauth/revoke?token=<your_token>&token_hint_type=<token_type>
```

#### Example Response

```
OK
```


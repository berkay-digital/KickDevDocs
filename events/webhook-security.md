---
icon: lock
---

# Webhooks

Both App and User access tokens can access this at the moment.

## Headers

<table><thead><tr><th width="302">Header</th><th width="200">Type</th><th>Short Description</th></tr></thead><tbody><tr><td>Kick-Event-Message-Id</td><td>ULID</td><td>Unique message id, idempotent key.</td></tr><tr><td>Kick-Event-Signature</td><td>Base64 Encode String</td><td>Signature to verify the sender</td></tr><tr><td>Kick-Event-Message-Timestamp</td><td>RFC3339 Date-time</td><td>Timestamp of when the message was sent</td></tr><tr><td>Kick-Event-Type</td><td>string</td><td>Eg. channel:write</td></tr><tr><td>Kick-Event-Version</td><td>string</td><td>Eg. 1</td></tr></tbody></table>

## Webhook Sender Validation

_Please Note! This currently isn't working as intended and is in the process of being fixed._

Kick-Event-Message-Signature header is used to validate if a request has come from the Kick servers. This is to prevent anyone that found an apps webhook endpoint from sending fake events.

### Kick Public Key

This is the Kick public key. Any request that is sent from our servers will be have a signature signed by our Private Key, which can be decrypted using this Public Key.

```
// Some code
-----BEGIN PUBLIC KEY-----
MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAq/+l1WnlRrGSolDMA+A8
6rAhMbQGmQ2SapVcGM3zq8ANXjnhDWocMqfWcTd95btDydITa10kDvHzw9WQOqp2
MZI7ZyrfzJuz5nhTPCiJwTwnEtWft7nV14BYRDHvlfqPUaZ+1KR4OCaO/wWIk/rQ
L/TjY0M70gse8rlBkbo2a8rKhu69RQTRsoaf4DVhDPEeSeI5jVrRDGAMGL3cGuyY
6CLKGdjVEM78g3JfYOvDU/RvfqD7L89TZ3iN94jrmWdGz34JNlEI5hqK8dd7C5EF
BEbZ5jgB8s8ReQV8H+MkuffjdAj3ajDDX3DOJMIut1lBrUVD1AaSrGCKHooWoL2e
twIDAQAB
-----END PUBLIC KEY-----
```

### Signature Creation

The signature is created through the concatenation of the following values into a single string:

* Kick-Event-Message-Id
* Kick-Event-Message-Timestamp
* The raw body of the request

Once concatenated, the body will be signed with the Kick Private Key.

### Examples

Here are some examples of verifying the signature in different languages.

#### Golang

```go
// Some code
func Verify(publicKey *rsa.PublicKey, body []byte, signature []byte) error {
   decoded := make([]byte, base64.StdEncoding.DecodedLen(len(signature)))

   n, err := base64.StdEncoding.Decode(decoded, signature)
   if err != nil {
       return err
   }


   signature = decoded[:n]
   hashed := sha256.Sum256(body)


   return rsa.VerifyPKCS1v15(publicKey, crypto.SHA256, hashed[:], signature)
}

```

## Retrying Sending of Events

Kick will attempt to send a webhook 3 times over a period of time until a 200 response is made by the server.

## Disabling of webhooks

After a certain thresholds of errors received from an apps webhook endpoint, Kick may automatically unsubscribe the app from receiving webhooks.

The app would then need to resubscribe to webhooks.

{% swagger src="https://api.kick.com/swagger/v1/doc.json" path="/oauth/revoke" method="post" %}
[https://api.kick.com/swagger/v1/doc.json](https://api.kick.com/swagger/v1/doc.json)
{% endswagger %}

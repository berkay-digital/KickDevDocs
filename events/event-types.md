---
icon: font-case
---

# Webhook Payloads

## Chat Message

```json
// Some code
Header: Kick-Event-Type: “chat.message.sent”

{
  "message_id": "unique_message_id_123",
  "broadcaster": {
    "user_id": 123456789,
    "username": "broadcaster_name",
    "is_verified": true,
    "profile_picture": "https://example.com/broadcaster_avatar.jpg",
    "channel_id": 987654321,
    "channel_slug": "broadcaster_channel"
  },
  "sender": {
    "user_id": 987654321,
    "username": "sender_name",
    "is_verified": false,
    "profile_picture": "https://example.com/sender_avatar.jpg",
    "channel_id": 987654321,
    "channel_slug": "sender_channel"
  },
  "content": "This is a test message with emotes!",
  "emotes": [
    {
      "emote_id": "12345",
      "positions": [
        { "s": 0, "e": 7 }
      ]
    },
    {
      "emote_id": "67890",
      "positions": [
        { "s": 20, "e": 25 }
      ]
    }
  ]
}
```

## Channel Follow

```json
// Some code
Header: Kick-Event-Type: “channel.followed”

{
  "broadcaster": {
    "user_id": 123456789,
    "username": "broadcaster_name",
    "is_verified": true,
    "profile_picture": "https://example.com/broadcaster_avatar.jpg",
    "channel_id": 987654321,
    "channel_slug": "broadcaster_channel"
  },
  "follower": {
    "user_id": 987654321,
    "username": "follower_name",
    "is_verified": false,
    "profile_picture": "https://example.com/sender_avatar.jpg",
    "channel_id": 987654321,
    "channel_slug": "follower_channel"
  }
}
```

## Channel Subscription Renewal

```json
// Some code
Header: Kick-Event-Type: “channel.subscription.renewal”

{
  "broadcaster": {
    "user_id": 123456789,
    "username": "broadcaster_name",
    "is_verified": true,
    "profile_picture": "https://example.com/broadcaster_avatar.jpg",
    "channel_id": 987654321,
    "channel_slug": "broadcaster_channel"
  },
  "subscriber": {
    "user_id": 987654321,
    "username": "subscriber_name",
    "is_verified": false,
    "profile_picture": "https://example.com/sender_avatar.jpg",
    "channel_id": 987654321,
    "channel_slug": "subscriber_channel"
  },
  "duration": 3.
  "created_at": "2025-01-14T16:08:06Z"
}
```

## Channel Subscription Gifts

```json
// Some code
Header: Kick-Event-Type: “channel.subscription.gifts”

{
  "broadcaster": {
    "user_id": 123456789,
    "username": "broadcaster_name",
    "is_verified": true,
    "profile_picture": "https://example.com/broadcaster_avatar.jpg",
    "channel_id": 987654321,
    "channel_slug": "broadcaster_channel"
  },
  "gifter": {
    "user_id": 987654321,
    "username": "gifter_name",
    "is_verified": false,
    "profile_picture": "https://example.com/sender_avatar.jpg",
    "channel_id": 987654321,
    "channel_slug": "gifter_channel"
  },
  "giftees": 
  [
    {
      "user_id": 561654654,
      "username": "giftee_name",
      "is_verified": true,
      "profile_picture": "https://example.com/broadcaster_avatar.jpg",
      "channel_id": 546546545,
      "channel_slug": "giftee_channel"
    }
  ],
  "created_at": "2025-01-14T16:08:06Z"
}
```

## Channel Subscription Created

```json
// Some code
Header: Kick-Event-Type: “channel.subscription.new”

{
  "broadcaster": {
    "user_id": 123456789,
    "username": "broadcaster_name",
    "is_verified": true,
    "profile_picture": "https://example.com/broadcaster_avatar.jpg",
    "channel_id": 987654321,
    "channel_slug": "broadcaster_channel"
  },
  "subscriber": {
    "user_id": 987654321,
    "username": "subscriber_name",
    "is_verified": false,
    "profile_picture": "https://example.com/sender_avatar.jpg",
    "channel_id": 987654321,
    "channel_slug": "subscriber_channel"
  },
  "duration": 1.
  "created_at": "2025-01-14T16:08:06Z"
}
```



{% swagger src="https://api.kick.com/swagger/v1/doc.json" path="/oauth/revoke" method="post" %}
[https://api.kick.com/swagger/v1/doc.json](https://api.kick.com/swagger/v1/doc.json)
{% endswagger %}

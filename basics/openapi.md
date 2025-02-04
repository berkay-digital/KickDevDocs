---
icon: network-wired
---

# OpenAPI

You can sync GitBook pages with an OpenAPI or Swagger file or a URL to include auto-generated API methods in your documentation.

### OpenAPI block

GitBook's OpenAPI block is powered by [Scalar](https://scalar.com/), so you can test your APIs directly from your docs.

{% swagger src="https://api.kick.com/swagger/v1/doc.json" path="/categories" method="get" %}
[https://api.kick.com/swagger/v1/doc.json](https://api.kick.com/swagger/v1/doc.json)
{% endswagger %}



{% swagger src="https://api.kick.com/swagger/v1/doc.json" path="/categories/:category_id" method="get" %}
[https://api.kick.com/swagger/v1/doc.json](https://api.kick.com/swagger/v1/doc.json)
{% endswagger %}

{% swagger src="https://api.kick.com/swagger/v1/doc.json" path="/channels" method="get" %}
[https://api.kick.com/swagger/v1/doc.json](https://api.kick.com/swagger/v1/doc.json)
{% endswagger %}

{% swagger src="https://api.kick.com/swagger/v1/doc.json" path="/channels" method="patch" %}
[https://api.kick.com/swagger/v1/doc.json](https://api.kick.com/swagger/v1/doc.json)
{% endswagger %}

{% swagger src="https://api.kick.com/swagger/v1/doc.json" path="/events/subscriptions" method="get" %}
[https://api.kick.com/swagger/v1/doc.json](https://api.kick.com/swagger/v1/doc.json)
{% endswagger %}

{% swagger src="https://api.kick.com/swagger/v1/doc.json" path="/events/subscriptions" method="post" %}
[https://api.kick.com/swagger/v1/doc.json](https://api.kick.com/swagger/v1/doc.json)
{% endswagger %}

{% swagger src="https://api.kick.com/swagger/v1/doc.json" path="/events/subscriptions" method="delete" %}
[https://api.kick.com/swagger/v1/doc.json](https://api.kick.com/swagger/v1/doc.json)
{% endswagger %}

{% swagger src="https://api.kick.com/swagger/v1/doc.json" path="/users" method="get" %}
[https://api.kick.com/swagger/v1/doc.json](https://api.kick.com/swagger/v1/doc.json)
{% endswagger %}

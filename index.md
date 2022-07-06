---
layout: null
---
{% for post in site.posts %}
    {{ post.title | xml_escape }}
    {{ post.content | xml_escape }}
    {{ post.date | date_to_rfc822 }}
    {{ post.url | prepend: site.baseurl | prepend: site.url }}
{% endfor %}
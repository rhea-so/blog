## Contents

<section id="contents" markdown="0">
{% for post in site.posts %}
    <a href="{{ post.url | prepend: site.baseurl | prepend: site.url }}">{{ post.title | xml_escape }} ({{ post.date | date_to_rfc822 }})</a><br/>
{% endfor %}
</section>
---
layout: page
title: The Aging Coder!
tagline: Random Musing of Technology
---
{% include JB/setup %}

<ul >
    {% for post in site.posts limit 4 %}
    <li><span>{{ post.date | date_to_string }}</span> &raquo; <a href="{{ BASE_PATH }}{{ post.url }}"><strong>{{ post.title }}</strong></a></li>
        {{ post.content | strip_html | truncatewords:75}}<br>
            <a href="{{ post.url }}">Read more...</a><br><br>
    {% endfor %}
</ul>




---
layout: page
title: Blog Arquivos
permalink: /archive/
banner_image: books.jpg
---

<div>
  {% for post in site.posts %}
    {% capture currentyear %}{{post.date | date: "%Y"}}{% endcapture %}
    {% if currentyear != year %}
        {% unless forloop.first %}
          </ul>
        {% endunless %}
        <h5>{{ currentyear }}</h5>
        <ul>
        {% capture year %}{{currentyear}}{% endcapture %} 
    {% endif %}
    <li><a href="{{ post.url | prepend: site.baseurl }}">{{ post.title }}</a></li>
  {% endfor %}

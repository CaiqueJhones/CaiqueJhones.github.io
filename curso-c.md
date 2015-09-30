---
layout: page
title: Introdução à linguagem de programação C
permalink: /cursos/c/
banner_image: c-program-language.jpg
---
<div>

<h2>Aulas:</h2>

{% for category in site.categories %}
    {% if category[0] == 'c' %}
    <ol>
    {% for posts in category %} 
      {% for post in posts reversed %}
        {% if post.title != null %}
        <li><a href="{{ post.url }}">{{ post.title }}</a></li>
	{% endif %}
      {% endfor %}
    {% endfor %}
    </ol>
    {{ break }}
    {% endif %}
{% endfor %}
</div>

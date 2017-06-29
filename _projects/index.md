---
layout: post
title: Projects
permalink: /projects/
---
#**Projects**
{% for project in site.data.projects %}
## **[{{ project.name }}]({{ project.url }})**
  <p>
    <strong>Status:</strong> {{ project.status }}<br>
    <strong>Focus:</strong> {{ project.focus }}<br>
    {{ project.short-description }} <br>
    <a class="post-link" href="{{ project.url }}"><img src="{{ project.image-path }}" style="width: {{ project.image-width }}; height: {{ project.image-height }}"/></a><br>
    <a class="post-link" href="{{ project.url }}">More info...</a>
  </p>
{% endfor %}

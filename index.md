---
layout: default
title: All Notes
direction: "auto"
---

<h1 id="all-notes">All Notes</h1>

<ul>
  {% assign _seen_urls = "" %}
  
  {% if site.notes and site.notes.size > 0 %}
    {% assign list = site.notes | sort: 'title' %}
    {% for note in list %}
      {% if note.title and note.published != false %}
        {% assign note_url = note.url | relative_url %}
        {% unless _seen_urls contains note_url %}
          
        {% assign item_dir = note.direction | default: 'ltr' %}

        <li dir="{{ item_dir }}" class="note-item">
          <a href="{{ note_url }}">{{ note.title }}</a>
        </li>

          {% assign _seen_urls = _seen_urls | append: note_url | append: "," %}
        {% endunless %}
      {% endif %}
    {% endfor %}

{% else %}
{% for item in site.pages %}
{% if item.title and item.url != "/" and item.layout != nil and item.published != false and item.path != "README.md" %}
{% assign item_url = item.url | relative_url %}
{% unless _seen_urls contains item_url %}

          {% assign item_dir = item.direction | default: 'ltr' %}

          <li dir="{{ item_dir }}" class="note-item">
            <a href="{{ item_url }}">{{ item.title }}</a>
          </li>

          {% assign _seen_urls = _seen_urls | append: item_url | append: "," %}
        {% endunless %}
      {% endif %}
    {% endfor %}

{% endif %}

</ul>
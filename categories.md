---
layout: page
title: 分类
permalink: /categories/
---

<div class="categories-list">
  {% assign sorted_categories = site.categories | sort %}
  {% for category in sorted_categories %}
    <h2 class="category-heading" id="{{ category[0] | slugify }}">{{ category[0] }}</h2>
    <ul class="category-list">
      {% assign sorted_posts = category[1] | sort: "date" | reverse %}
      {% for post in sorted_posts %}
        <li>
          <time class="post-item-date" datetime="{{ post.date | date_to_xmlschema }}">{{ post.date | date: "%Y-%m-%d" }}</time>
          <a href="{{ post.url | relative_url }}">{{ post.title }}</a>
        </li>
      {% endfor %}
    </ul>
  {% endfor %}
</div>

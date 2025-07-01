---
layout: default
title: News
permalink: /news/
---
<section class="news-listing">
  <h1>{{ page.title }}</h1>

  <ul class="news-list">
    {% assign news_posts = site.posts | where_exp: "post", "post.layout == 'news'" %}
    {% for post in news_posts %}
      <li class="news-item">
        <p class="news-meta">
          <time datetime="{{ post.date | date_to_xmlschema }}">
            {{ post.date | date: "%B %-d, %Y" }}
          </time>
          {% if post.author %}
            • <em>{{ post.author }}</em>
          {% endif %}
        </p>
        <h2><a href="{{ post.url | relative_url }}">{{ post.title }}</a></h2>
        {% if post.excerpt %}
          <p>{{ post.excerpt | strip_html | truncate: 200 }}</p>
        {% endif %}
      </li>
    {% endfor %}
  </ul>
</section>

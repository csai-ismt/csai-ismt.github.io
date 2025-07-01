---
layout: page
title: News
permalink: /news/
paginate: 5
---

<div id="news">
  <!-- Responsive Header -->
  <section id="header-content">
    <h1>{{ page.title }}</h1>
  </section>
  <section class="bg"></section>

  <div class="row">
    <!-- Aside Navigation -->
    <aside id="aside" class="col-md-4">
      {% include blogaside.html %}
    </aside>

    <!-- News List -->
    <section id="posts" class="col-md-8">
      {% assign news_posts = paginator.posts | where_exp: "post", "post.layout == 'news'" %}
      {% for post in news_posts %}
      <div class="post">
        <a href="{{ post.url | relative_url }}">
          <div class="post-wrap">
            <div class="text-wrap">
              <h3 class="title">{{ post.title }}</h3>
              <p class="excerpt">
                {% if post.excerpt and post.excerpt.size > 50 %}
                  {{ post.excerpt | strip_html | strip_newlines | truncatewords: 25, '...' }}
                {% elsif post.subtitle %}
                  {{ post.subtitle }}
                {% endif %}
              </p>
              <div>
                <span class="meta">
                  {{ post.date | date: "%B %-d, %Y" }}
                  {% if post.author %}
                    • {{ post.author }}
                  {% endif %}
                </span>
                {% if post.tags %}
                <ul class="tag-wrap">
                  {% for tag in post.tags %}
                    <a href="{{ site.baseurl }}/tags#{{ tag | cgi_escape }}">
                      <li class="tag-sm">{{ tag }}</li>
                    </a>
                  {% endfor %}
                </ul>
                {% endif %}
              </div>
            </div>

            {% if post.image %}
            <div class="img-wrap">
              <img src="{{ post.image }}" alt="{{ post.title }}">
            </div>
            {% endif %}
          </div>
        </a>
      </div>
      {% endfor %}

      <!-- Pagination -->
      {% if paginator.total_pages > 1 %}
      <div id="pagination">
        <ul>
          {% assign start = ((paginator.page - 1) | divided_by: 5) | times: 5 | plus: 1 %}
          {% assign end = start | plus: 4 %}
          {% if end > paginator.total_pages %}
          {% assign end = paginator.total_pages %}
          {% endif %}

          {% if paginator.page > 1 %}
          <a href="{{ paginator.previous_page_path }}">
            <li class="btn-rounded prev"><i class="fas fa-angle-double-left"></i></li>
          </a>
          {% endif %}

          {% for p in (start..end) %}
          <a href="{% if p == 1 %}/news/{% else %}/news/page{{ p }}/{% endif %}"
             class="{% if p == paginator.page %}selected{% endif %}">
            <li class="btn-rounded">{{ p }}</li>
          </a>
          {% endfor %}

          {% if paginator.page < paginator.total_pages %}
          <a href="{{ paginator.next_page_path }}">
            <li class="btn-rounded next"><i class="fas fa-angle-double-right"></i></li>
          </a>
          {% endif %}
        </ul>
      </div>
      {% endif %}
    </section>
  </div>
</div>

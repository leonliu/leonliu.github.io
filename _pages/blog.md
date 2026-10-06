---
title: "Writing"
layout: archive
permalink: /blog/
classes: wide
author_profile: false
---

Thoughts, notes, and things I’ve learned—technical and otherwise. Browse by topic, or start with the latest posts.

<nav class="topic-links" aria-label="Writing topics">
  <a href="{{ '/categories/ai-chatbots/' | relative_url }}">AI &amp; chatbots</a>
  <a href="{{ '/categories/robotics/' | relative_url }}">Robotics</a>
  <a href="{{ '/categories/blockchain/' | relative_url }}">Blockchain</a>
</nav>

<div class="post-list archive-list">
  {% for post in site.posts %}
    <article class="post-card">
      <p class="post-card__meta">{{ post.date | date: "%b %-d, %Y" }}{% if post.categories.size > 0 %}<span aria-hidden="true"> · </span>{{ post.categories | join: ", " }}{% endif %}</p>
      <h2><a href="{{ post.url | relative_url }}">{{ post.title }}</a></h2>
      <p>{{ post.excerpt | strip_html | truncate: 220 }}</p>
    </article>
  {% endfor %}
</div>

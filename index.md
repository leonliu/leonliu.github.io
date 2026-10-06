---
title: ""
layout: splash
permalink: /
classes: wide home-page
author_profile: false
---

<section class="home-intro">
  <p class="eyebrow">Indie developer · Auckland, New Zealand</p>
  <h1>Hi, I’m Leon.</h1>
  <p class="home-lede">I build software, write about what I’m learning, and follow whatever else catches my curiosity.</p>
  <div class="home-actions">
    <a class="btn btn--primary" href="{{ '/blog/' | relative_url }}">Browse the writing</a>
    <a class="text-link" href="{{ '/products/' | relative_url }}">Explore my products <span aria-hidden="true">→</span></a>
  </div>
</section>

<section class="home-section" aria-labelledby="recent-writing">
  <div class="section-heading">
    <div>
      <p class="eyebrow">From the notebook</p>
      <h2 id="recent-writing">Recent writing</h2>
    </div>
    <a class="text-link" href="{{ '/blog/' | relative_url }}">All writing <span aria-hidden="true">→</span></a>
  </div>
  <div class="post-list">
    {% for post in site.posts limit:3 %}
      <article class="post-card">
        <p class="post-card__meta">{{ post.date | date: "%b %-d, %Y" }}{% if post.categories.size > 0 %}<span aria-hidden="true"> · </span>{{ post.categories | join: ", " }}{% endif %}</p>
        <h3><a href="{{ post.url | relative_url }}">{{ post.title }}</a></h3>
        <p>{{ post.excerpt | strip_html | truncate: 180 }}</p>
      </article>
    {% endfor %}
  </div>
</section>

<section class="home-section" aria-labelledby="browse-topics">
  <div class="section-heading">
    <div>
      <p class="eyebrow">Follow a thread</p>
      <h2 id="browse-topics">Browse by topic</h2>
    </div>
  </div>
  <div class="topic-grid">
    <a class="topic-card" href="{{ '/categories/ai-chatbots/' | relative_url }}"><span class="topic-card__mark">01</span><span><strong>AI &amp; chatbots</strong><small>Conversational systems and machine learning</small></span><span class="topic-card__arrow" aria-hidden="true">↗</span></a>
    <a class="topic-card" href="{{ '/categories/robotics/' | relative_url }}"><span class="topic-card__mark">02</span><span><strong>Robotics</strong><small>Mechanisms, motion, and control</small></span><span class="topic-card__arrow" aria-hidden="true">↗</span></a>
    <a class="topic-card" href="{{ '/categories/blockchain/' | relative_url }}"><span class="topic-card__mark">03</span><span><strong>Blockchain</strong><small>Distributed systems and digital money</small></span><span class="topic-card__arrow" aria-hidden="true">↗</span></a>
  </div>
</section>

<section class="home-section home-products" aria-labelledby="products-heading">
  <div>
    <p class="eyebrow">Made independently</p>
    <h2 id="products-heading">Products &amp; support</h2>
    <p>Small software projects, along with the notes and help that make them easier to use.</p>
  </div>
  <a class="btn btn--inverse" href="{{ '/products/' | relative_url }}">See products</a>
</section>

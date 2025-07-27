---
layout: page
title: Jaenact
permalink: /
---

<style>
  .post-cards {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
    gap: 1.5rem;
    margin-top: 1rem;
  }

  .post-card {
    border: 1px solid #ddd;
    border-radius: 8px;
    padding: 1.2rem;
    background-color: #fff;
    transition: box-shadow 0.2s ease;
  }

  .post-card:hover {
    box-shadow: 0 4px 12px rgba(0,0,0,0.1);
  }

  .post-title {
    font-size: 1.1rem;
    font-weight: 600;
    margin-bottom: 0.2rem;
  }

  .post-meta {
    font-size: 0.85rem;
    color: #777;
    margin-bottom: 0.5rem;
  }

  .post-desc {
    font-size: 0.95rem;
    margin-top: 0.3rem;
    color: #444;
  }

  .section-title {
    font-size: 1.4rem;
    font-weight: 600;
    margin-top: 2.5rem;
    border-bottom: 1px solid #ccc;
    padding-bottom: 0.3rem;
  }

  .category-label {
    font-size: 0.8rem;
    color: #888;
    font-style: italic;
  }
</style>

<section>
  <h2 class="section-title">About</h2>
  <p>
    This is <strong>Jaenact</strong>'s technical blog, focused on security, development, and real-world experimentation.<br>
    I publish research notes, project logs, and curated thoughts on systems, automation, and vulnerability.
  </p>
</section>

<section>
  <h2 class="section-title">GitHub Activity</h2>
  <div style="display: flex; flex-wrap: wrap; gap: 2rem;">
    <!-- GitHub Stats 카드 (왼쪽) -->
    <div style="flex: 1; min-width: 300px;">
      <img src="https://github-readme-stats.vercel.app/api?username=Jaenact&show_icons=true&theme=default&hide=prs&count_private=true" alt="GitHub Stats" style="max-width: 100%;">
    </div>

    <!-- 최근 커밋 목록 (오른쪽) -->
    <div style="flex: 1.2; min-width: 300px;">
      <ul class="post-list">
        {% for item in site.data.commits %}
          <li>
            <a href="{{ item.url }}" target="_blank">{{ item.message | truncate: 60 }}</a>
            <span class="post-meta">{{ item.date }}</span>
          </li>
        {% endfor %}
      </ul>
    </div>
  </div>
</section>


<section>
  <h2 class="section-title">Featured Posts</h2>
  <div class="post-cards">
    {% assign pinned = site.posts | where: "pin", true %}
    {% for post in pinned %}
    <div class="post-card">
      <div class="post-title">
        <a href="{{ post.url }}">{{ post.title }}</a>
      </div>
      <div class="post-meta">
        {{ post.date | date: "%Y.%m.%d" }}
        {% if post.categories %}
          · <span class="category-label">{{ post.categories | join: " / " }}</span>
        {% endif %}
      </div>
      {% if post.description %}
        <div class="post-desc">{{ post.description }}</div>
      {% endif %}
    </div>
    {% endfor %}
  </div>
</section>

<section>
  <h2 class="section-title">Recent Posts</h2>
  <div class="post-cards">
    {% assign recent = site.posts | sort: "date" | reverse %}
    {% for post in recent limit:5 %}
      {% unless post.pin %}
      <div class="post-card">
        <div class="post-title">
          <a href="{{ post.url }}">{{ post.title }}</a>
        </div>
        <div class="post-meta">
          {{ post.date | date: "%Y.%m.%d" }}
          {% if post.categories %}
            · <span class="category-label">{{ post.categories | join: " / " }}</span>
          {% endif %}
        </div>
        {% if post.description %}
          <div class="post-desc">{{ post.description }}</div>
        {% endif %}
      </div>
      {% endunless %}
    {% endfor %}
  </div>
</section>

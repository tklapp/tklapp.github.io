---
layout: page
permalink: /gems/
title: gems
description: live recordings worth the detour — an ongoing dig through concerts, sessions, and bootlegs.
nav: true
nav_order: 2
---

<style>
  .gem-list {
    list-style: none;
    margin: 2rem 0 0;
    padding: 0;
  }

  .gem {
    padding: 1.25rem 0;
    border-top: 1px solid var(--global-divider-color);
  }

  .gem:last-child {
    border-bottom: 1px solid var(--global-divider-color);
  }

  .gem-title {
    font-size: 1.05rem;
    font-weight: 600;
    line-height: 1.35;
  }

  .gem-title a {
    color: var(--global-text-color);
    text-decoration: none;
  }

  .gem-title a:hover {
    color: var(--global-theme-color);
  }

  .gem-artist {
    color: var(--global-theme-color);
  }

  .gem-meta {
    margin-top: 0.15rem;
    font-size: 0.85rem;
    color: var(--global-text-color-light);
  }

  .gem-note {
    margin-top: 0.5rem;
    font-size: 0.95rem;
  }

  .gem-note p {
    margin-bottom: 0;
  }
</style>

{% if site.data.gems and site.data.gems.size > 0 %}
  <ul class="gem-list">
    {% for gem in site.data.gems %}
      <li class="gem">
        <div class="gem-title">
          {% if gem.url %}<a href="{{ gem.url }}" target="_blank" rel="noopener noreferrer">{{ gem.title }}</a>{% else %}{{ gem.title }}{% endif %}
          {% if gem.artist %}<span class="gem-artist">— {{ gem.artist }}</span>{% endif %}
        </div>
        {% if gem.where or gem.year %}
          <div class="gem-meta">
            {{ gem.where }}{% if gem.where and gem.year %},{% endif %}
            {{ gem.year }}
          </div>
        {% endif %}
        {% if gem.note %}<div class="gem-note">{{ gem.note | markdownify }}</div>{% endif %}
      </li>
    {% endfor %}
  </ul>
{% else %}
  <p>Nothing here yet — the dig is ongoing.</p>
{% endif %}

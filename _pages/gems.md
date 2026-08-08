---
layout: page
permalink: /gems/
title: gems
description: live recordings worth the detour — an ongoing dig through concerts, sessions, and bootlegs.
nav: true
nav_order: 3
---

<style>
  .gem-list {
    list-style: none;
    margin: 2rem 0 0;
    padding: 0;
  }

  .gem {
    display: flex;
    gap: 1rem;
    align-items: flex-start;
    padding: 1.25rem 0;
    border-top: 1px solid var(--global-divider-color);
  }

  .gem:last-child {
    border-bottom: 1px solid var(--global-divider-color);
  }

  /* min-width/max-width are load-bearing: a flex item defaults to
     min-width:auto, which is the image's intrinsic 480px, so flex-basis alone
     gets ignored and the thumb renders full size. */
  .gem-thumb {
    flex: 0 0 160px;
    min-width: 0;
    max-width: 160px;
    display: block;
    line-height: 0;
  }

  /* hqdefault is 4:3 and holds the whole frame; mqdefault is a hard 16:9
     center-crop that decapitates anything shot in 4:3. `contain` means a
     natively widescreen video letterboxes instead of being cut. */
  .gem-thumb img {
    width: 160px;
    height: 120px;
    object-fit: contain;
    border-radius: 4px;
    display: block;
  }

  /* Keeps the text from overflowing the flex row on long titles. */
  .gem-body {
    min-width: 0;
    flex: 1;
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

  @media (max-width: 575px) {
    .gem-thumb {
      flex-basis: 108px;
      max-width: 108px;
    }

    .gem-thumb img {
      width: 108px;
      height: 81px;
    }
  }
</style>

{% if site.data.gems and site.data.gems.size > 0 %}

  <ul class="gem-list">
    {% for gem in site.data.gems %}
      {% comment %}
        Pull the YouTube id straight out of the link so entries in _data/gems.yml
        stay a single `url:` line. Handles both watch?v= and youtu.be/ forms;
        anything else just renders without a thumbnail.
      {% endcomment %}
      {% assign yt_id = "" %}
      {% if gem.url contains "youtu.be/" %}
        {% assign yt_id = gem.url | split: "youtu.be/" | last | split: "?" | first | split: "&" | first %}
      {% elsif gem.url contains "v=" %}
        {% assign yt_id = gem.url | split: "v=" | last | split: "&" | first %}
      {% endif %}

      <li class="gem">
        {% if yt_id != "" %}
          <a class="gem-thumb" href="{{ gem.url }}" target="_blank" rel="noopener noreferrer" tabindex="-1" aria-hidden="true">
            <img src="https://img.youtube.com/vi/{{ yt_id }}/hqdefault.jpg" alt="" loading="lazy" width="480" height="360">
          </a>
        {% endif %}

        <div class="gem-body">
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
        </div>
      </li>
    {% endfor %}

  </ul>
{% else %}
  <p>Nothing here yet — the dig is ongoing.</p>
{% endif %}

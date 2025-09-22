---
layout: home-page
title: Research
permalink: /research/
subtitle: Publications by type — Conference / Journal / Poster / Workshop
---

{% assign blocks = site.data.publications | sort: 'year' | reverse %}
{% assign types = "Conference|Journal|Poster|Workshop" | split: "|" %}

<!-- 상단 빠른 이동(원하면 지워도 됨) -->
<p class="pub-meta small">
  <a href="#conference">Conference</a> ·
  <a href="#journal">Journal</a> ·
  <a href="#poster">Poster</a> ·
  <a href="#workshop">Workshop</a>
</p>

{% for T in types %}
<div id="{{ T | downcase }}" class="section-label">{{ T }}</div>
{% assign any = false %}

  {% for b in blocks %}
    {% assign y = b.year %}
    {% for p in b.items %}
      {% if p.type == T %}
        {% assign any = true %}
<div class="pub-card compact">
  <div class="pub-title">{{ p.authors }}. <strong>{{ p.title }}</strong></div>
  <div class="pub-meta small">
    {% if p.venue %}<em>{{ p.venue }}</em>{% endif %}
    {% if y %} · {{ y }}{% endif %}
    {% if p.ar %} · AR: {{ p.ar }}{% endif %}
    {% if p.award %} · 🏅 {{ p.award }}{% endif %}
    {% if p.status %} · {{ p.status }}{% endif %}
  </div>
  <div class="pub-links">
    {% if p.pdf %}<a href="{{ p.pdf }}">PDF</a>{% endif %}
    {% if p.doi %}<a href="https://doi.org/{{ p.doi }}">DOI</a>{% endif %}
    {% if p.video %}<a href="{{ p.video }}">Video</a>{% endif %}
    {% if p.demo %}<a href="{{ p.demo }}">Demo</a>{% endif %}
    {% if p.poster %}<a href="{{ p.poster }}">Poster</a>{% endif %}
    {% if p.teaser %}<a href="{{ p.teaser }}">Teaser</a>{% endif %}
    {% if p.bib %}<a href="{{ p.bib }}">BibTeX</a>{% endif %}
  </div>
</div>
      {% endif %}
    {% endfor %}
  {% endfor %}

{% unless any %}
<p class="pub-meta small">No {{ T | downcase }} items yet.</p>
{% endunless %}

{% endfor %}

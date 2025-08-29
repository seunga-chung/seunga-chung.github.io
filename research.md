---
layout: home-page
title: Research
permalink: /research/
profile_picture:
  src: /assets/img/profile.jpg
  alt: SeungA Chung profile photo
subtitle: Publications by type — Journal / Conference / Workshop / Poster
---

{% assign blocks = site.data.publications | sort: 'year' | reverse %}
{% assign types = "Journal|Conference|Workshop|Poster" | split: "|" %}

{% for T in types %}
## {{ T }}
{% assign any = false %}
  {% for b in blocks %}
    {% assign y = b.year %}
    {% for p in b.items %}
      {% if p.type == T %}
        {% assign any = true %}
<div class="pub-card">
  <div class="pub-title">{{ p.authors }}. <strong>{{ p.title }}</strong></div>
  <div class="pub-meta">
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
  <div>
    <span class="badge">{{ p.type }}</span>
  </div>
</div>
      {% endif %}
    {% endfor %}
  {% endfor %}
{% unless any %}<p class="pub-meta">No {{ T | downcase }} items yet.</p>{% endunless %}

{% endfor %}

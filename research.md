---
layout: page
title: Research
permalink: /research/
---

# Research

<!-- 상단 빠른 이동 -->
<p>
  <a href="#journal">Journal</a> ·
  <a href="#conference">Conference</a> ·
  <a href="#workshop">Workshop</a> ·
  <a href="#poster">Poster</a>
</p>

<style>
  .pub { margin: 0 0 1.1rem 0; }
  .pub-title { font-weight: 600; }
  .pub-meta { color: #666; }
  .pub .links a { margin-right: .6rem; }
  h2 { margin-top: 2rem; }
  .badge { display:inline-block; padding:.1rem .45rem; border:1px solid #e1e1e1; border-radius:.4rem; font-size:.8rem; }
</style>

{% comment %}
1) 전체 데이터 모음
2) 타입별로 필터 + 연도 최신순 정렬
{% endcomment %}
{% assign all = site.data.publications %}

{% assign journals = all | where: "type", "Journal"    | sort: "year" | reverse %}
{% assign confs    = all | where: "type", "Conference" | sort: "year" | reverse %}
{% assign works    = all | where: "type", "Workshop"   | sort: "year" | reverse %}
{% assign posters  = all | where: "type", "Poster"     | sort: "year" | reverse %}

<!-- ========== Journal ========== -->
<h2 id="journal">Journal</h2>
{% if journals and journals.size > 0 %}
  {% for p in journals %}
  <div class="pub">
    <div class="pub-title">{{ p.authors }}. <strong>{{ p.title }}</strong></div>
    <div class="pub-meta">
      {% if p.venue %}<em>{{ p.venue }}</em>{% endif %}
      {% if p.year %} · {{ p.year }}{% endif %}
      {% if p.ar %} · AR: {{ p.ar }}{% endif %}
      {% if p.award %} · 🏅 {{ p.award }}{% endif %}
      {% if p.status %} · {{ p.status }}{% endif %}
    </div>
    <div class="links">
      {% if p.pdf %}<a href="{{ p.pdf }}">PDF</a>{% endif %}
      {% if p.doi %}<a href="https://doi.org/{{ p.doi }}">DOI</a>{% endif %}
      {% if p.video %}<a href="{{ p.video }}">Video</a>{% endif %}
      {% if p.demo %}<a href="{{ p.demo }}">Demo</a>{% endif %}
      {% if p.poster %}<a href="{{ p.poster }}">Poster</a>{% endif %}
      {% if p.teaser %}<a href="{{ p.teaser }}">Teaser</a>{% endif %}
      {% if p.bib %}<a href="{{ p.bib }}">BibTeX</a>{% endif %}
    </div>
    <div>
      <span class="badge">Journal</span>
      {% if p.venue_short %}<span class="badge">{{ p.venue_short }}</span>{% endif %}
    </div>
  </div>
  {% endfor %}
{% else %}
  <p class="pub-meta">No journal publications yet.</p>
{% endif %}

<!-- ========== Conference ========== -->
<h2 id="conference">Conference</h2>
{% if confs and confs.size > 0 %}
  {% for p in confs %}
  <div class="pub">
    <div class="pub-title">{{ p.authors }}. <strong>{{ p.title }}</strong></div>
    <div class="pub-meta">
      {% if p.venue %}<em>{{ p.venue }}</em>{% endif %}
      {% if p.year %} · {{ p.year }}{% endif %}
      {% if p.ar %} · AR: {{ p.ar }}{% endif %}
      {% if p.award %} · 🏅 {{ p.award }}{% endif %}
      {% if p.status %} · {{ p.status }}{% endif %}
    </div>
    <div class="links">
      {% if p.pdf %}<a href="{{ p.pdf }}">PDF</a>{% endif %}
      {% if p.video %}<a href="{{ p.video }}">Video</a>{% endif %}
      {% if p.demo %}<a href="{{ p.demo }}">Demo</a>{% endif %}
      {% if p.poster %}<a href="{{ p.poster }}">Poster</a>{% endif %}
      {% if p.teaser %}<a href="{{ p.teaser }}">Teaser</a>{% endif %}
      {% if p.bib %}<a href="{{ p.bib }}">BibTeX</a>{% endif %}
    </div>
    <div>
      <span class="badge">Conference</span>
      {% if p.venue_short %}<span class="badge">{{ p.venue_short }}</span>{% endif %}
    </div>
  </div>
  {% endfor %}
{% else %}
  <p class="pub-meta">No conference papers yet.</p>
{% endif %}

<!-- ========== Workshop ========== -->
<h2 id="workshop">Workshop</h2>
{% if works and works.size > 0 %}
  {% for p in works %}
  <div class="pub">
    <div class="pub-title">{{ p.authors }}. <strong>{{ p.title }}</strong></div>
    <div class="pub-meta">
      {% if p.venue %}<em>{{ p.venue }}</em>{% endif %}
      {% if p.year %} · {{ p.year }}{% endif %}
      {% if p.status %} · {{ p.status }}{% endif %}
    </div>
    <div class="links">
      {% if p.pdf %}<a href="{{ p.pdf }}">PDF</a>{% endif %}
      {% if p.video %}<a href="{{ p.video }}">Video</a>{% endif %}
      {% if p.bib %}<a href="{{ p.bib }}">BibTeX</a>{% endif %}
    </div>
    <div>
      <span class="badge">Workshop</span>
      {% if p.venue_short %}<span class="badge">{{ p.venue_short }}</span>{% endif %}
    </div>
  </div>
  {% endfor %}
{% else %}
  <p class="pub-meta">No workshop papers yet.</p>
{% endif %}

<!-- ========== Poster ========== -->
<h2 id="poster">Poster</h2>
{% if posters and posters.size > 0 %}
  {% for p in posters %}
  <div class="pub">
    <div class="pub-title">{{ p.authors }}. <strong>{{ p.title }}</strong></div>
    <div class="pub-meta">
      {% if p.venue %}<em>{{ p.venue }}</em>{% endif %}
      {% if p.year %} · {{ p.year }}{% endif %}
      {% if p.status %} · {{ p.status }}{% endif %}
    </div>
    <div class="links">
      {% if p.pdf %}<a href="{{ p.pdf }}">PDF</a>{% endif %}
      {% if p.teaser %}<a href="{{ p.teaser }}">Teaser</a>{% endif %}
      {% if p.bib %}<a href="{{ p.bib }}">BibTeX</a>{% endif %}
    </div>
    <div>
      <span class="badge">Poster</span>
      {% if p.venue_short %}<span class="badge">{{ p.venue_short }}</span>{% endif %}
    </div>
  </div>
  {% endfor %}
{% else %}
  <p class="pub-meta">No posters yet.</p>
{% endif %}

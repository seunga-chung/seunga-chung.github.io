---
layout: home-page
title: Research
permalink: /research/
profile_picture:
  src: /assets/img/profile.jpg
  alt: SeungA Chung profile photo
subtitle: Publications by type — Journal / Conference / Workshop / Poster
---

<style>
  /* 이미 assets/css/site.css에 비슷한 스타일이 있으면 이 블록은 생략 가능 */
  .pub-card{ border:1px solid var(--line,#e5e7eb); border-radius:14px; padding:14px; margin:0 0 12px; background:var(--bg,#fff); }
  .pub-title{ font-weight:600; }
  .pub-meta{ color:var(--muted,#60708a); font-size:.95rem; }
  .pub-links a{ margin-right:.6rem; }
  .badge{ display:inline-block; padding:.12rem .45rem; border:1px solid var(--line,#e5e7eb); border-radius:999px; font-size:.8rem; color:var(--muted,#60708a); background:var(--bg,#fff); }
  h2{ margin-top:2rem; }
</style>

{% comment %}
데이터 원본을 유연하게 가져오기:
1) 기본: site.data.publications (권장 파일명)
2) 대안: site.data.publication / site.data.pubs (혹시 파일명을 다르게 저장했을 때를 대비)
또, 데이터 구조가
 A) '평탄(flat) 리스트'   예: - {type:..., year:..., ...}
 B) '연도 블록 구조'      예: - year: 2024, items: [ {type:..., ...}, ... ]
둘 다 지원.
{% endcomment %}

{% assign D = site.data.publications | default: site.data.publication | default: site.data.pubs %}

{% if D == nil %}
<p class="pub-meta">⚠️ 데이터를 찾을 수 없어요. <code>_data/publications.yml</code> 파일을 확인해 주세요.</p>
{% endif %}

{% assign is_blocks = false %}
{% if D and D[0] and D[0].items %}
  {% assign is_blocks = true %}
{% endif %}

{% comment %}섹션 그리기 유틸: 타입/연도 정렬 + 카드 출력{% endcomment %}
{% capture render_item %}
<div class="pub-card">
  <div class="pub-title">{{ p.authors }}. <strong>{{ p.title }}</strong></div>
  <div class="pub-meta">
    {% if p.venue %}<em>{{ p.venue }}</em>{% endif %}
    {% if yy %} · {{ yy }}{% endif %}
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
    <span class="badge">{{ p.type }}</span>{% if p.venue_short %} <span class="badge">{{ p.venue_short }}</span>{% endif %}
  </div>
</div>
{% endcapture %}

{% assign types = "Journal|Conference|Workshop|Poster" | split: "|" %}

{% for T in types %}
<h2 id="{{ T | downcase }}">{{ T }}</h2>

  {% if is_blocks %}
    {%- assign any = false -%}
    {%- comment -%} 연도 블록 구조에서 해당 타입을 찾아 최신연도→과거연도 순으로 출력 {%- endcomment -%}
    {%- assign blocks_sorted = D | sort: "year" | reverse -%}
    {%- for b in blocks_sorted -%}
      {%- assign year = b.year -%}
      {%- for p in b.items -%}
        {%- if p.type == T -%}
          {%- assign any = true -%}
          {%- assign yy = p.year | default: year -%}
          {{ render_item }}
        {%- endif -%}
      {%- endfor -%}
    {%- endfor -%}
    {%- if any == false -%}<p class="pub-meta">No {{ T | downcase }} items yet.</p>{%- endif -%}

  {% else %}
    {%- comment -%} 평탄 리스트 구조에서 where + 최신연도 정렬 {%- endcomment -%}
    {%- assign items = D | where: "type", T | sort: "year" | reverse -%}
    {%- if items and items.size > 0 -%}
      {%- for p in items -%}
        {%- assign yy = p.year -%}
        {{ render_item }}
      {%- endfor -%}
    {%- else -%}
      <p class="pub-meta">No {{ T | downcase }} items yet.</p>
    {%- endif -%}
  {% endif %}

{% endfor %}

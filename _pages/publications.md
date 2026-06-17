---
layout: archive
title: "Publications"
permalink: /publications/
author_profile: true
---

{% assign all_pubs    = site.data.publications %}
{% assign journals    = all_pubs | where: "type", "journal" %}
{% assign q1_pubs     = journals  | where: "quartile", "Q1" %}
{% assign q2_pubs     = journals  | where: "quartile", "Q2" %}
{% assign conferences = all_pubs  | where: "type", "conference" %}
{% assign posters     = all_pubs  | where: "type", "poster" %}
{% assign books       = all_pubs  | where: "type", "book" %}
{% assign years       = all_pubs  | map: "year" | uniq | sort | reverse %}
{% assign metrics = site.data.metrics %}

{% assign code_count = 0 %}
{% for pub in all_pubs %}{% if pub.code %}{% assign code_count = code_count | plus: 1 %}{% endif %}{% endfor %}

<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Playfair+Display:wght@600;700&family=IBM+Plex+Sans:wght@300;400;500&family=IBM+Plex+Mono:wght@400&display=swap" rel="stylesheet">

<style>
/* ── Reset & base ─────────────────────────────────────────── */
.pub-page * { box-sizing: border-box; }

.pub-page {
  font-family: 'IBM Plex Sans', sans-serif;
  font-weight: 300;
  color: #141416;
  max-width: 860px;
}

/* ── Metrics bar ──────────────────────────────────────────── */
.metrics-bar {
  display: grid;
  grid-template-columns: repeat(5, 1fr);
  gap: 0;
  border: 1px solid #e2ddd8;
  border-radius: 4px;
  margin: 2rem 0 2.8rem;
  overflow: hidden;
}

.metric-item {
  padding: 1.4rem 1rem;
  text-align: center;
  border-right: 1px solid #e2ddd8;
  transition: background 0.18s;
}
.metric-item:last-child { border-right: none; }
.metric-item:hover { background: #faf7f3; }

.metric-number {
  display: block;
  font-family: 'Playfair Display', serif;
  font-size: 2.1rem;
  font-weight: 700;
  color: #0d2b5e;
  line-height: 1;
  letter-spacing: -0.03em;
}

.metric-label {
  display: block;
  font-size: 0.68rem;
  font-weight: 500;
  letter-spacing: 0.09em;
  text-transform: uppercase;
  color: #8a8789;
  margin-top: 0.45rem;
}

/* ── Controls ─────────────────────────────────────────────── */
.pub-controls {
  display: flex;
  flex-direction: column;
  gap: 1rem;
  margin-bottom: 2rem;
}

.control-row {
  display: flex;
  align-items: center;
  gap: 0.6rem;
  flex-wrap: wrap;
}

.control-label {
  font-size: 0.68rem;
  font-weight: 500;
  letter-spacing: 0.1em;
  text-transform: uppercase;
  color: #8a8789;
  min-width: 56px;
}

.filter-pill {
  padding: 0.3rem 0.85rem;
  font-family: 'IBM Plex Sans', sans-serif;
  font-size: 0.78rem;
  font-weight: 400;
  border: 1px solid #d8d3cc;
  border-radius: 2px;
  background: transparent;
  color: #444;
  cursor: pointer;
  transition: all 0.15s;
  line-height: 1.5;
}
.filter-pill:hover {
  border-color: #0d2b5e;
  color: #0d2b5e;
}
.filter-pill.active {
  background: #0d2b5e;
  border-color: #0d2b5e;
  color: #fff;
}

.search-wrapper {
  position: relative;
  flex: 1;
  max-width: 340px;
}
.search-wrapper svg {
  position: absolute;
  left: 0.7rem;
  top: 50%;
  transform: translateY(-50%);
  color: #aaa;
  pointer-events: none;
}
.search-input {
  width: 100%;
  padding: 0.38rem 0.8rem 0.38rem 2.2rem;
  font-family: 'IBM Plex Sans', sans-serif;
  font-size: 0.82rem;
  font-weight: 300;
  border: 1px solid #d8d3cc;
  border-radius: 2px;
  background: #fff;
  color: #141416;
  outline: none;
  transition: border-color 0.15s;
}
.search-input::placeholder { color: #bbb; }
.search-input:focus { border-color: #0d2b5e; }

/* ── Divider + count ──────────────────────────────────────── */
.pub-divider {
  display: flex;
  align-items: center;
  gap: 1rem;
  margin-bottom: 1.6rem;
}
.pub-divider-line { flex: 1; height: 1px; background: #e2ddd8; }
.pub-count-label {
  font-size: 0.72rem;
  font-weight: 500;
  letter-spacing: 0.08em;
  text-transform: uppercase;
  color: #aaa;
  white-space: nowrap;
}

/* ── Publication cards ────────────────────────────────────── */
.pub-list { display: flex; flex-direction: column; gap: 0; }

.pub-card {
  padding: 1.25rem 0;
  border-bottom: 1px solid #eceae6;
  display: grid;
  grid-template-columns: auto 1fr;
  gap: 0 1.2rem;
  transition: opacity 0.2s;
}
.pub-card.hidden { display: none; }
.pub-card:hover .pub-title-link { color: #d4852a; }

.pub-year-col {
  font-family: 'IBM Plex Mono', monospace;
  font-size: 0.72rem;
  color: #bbb;
  padding-top: 0.22rem;
  min-width: 38px;
  text-align: right;
  letter-spacing: 0.03em;
}

.pub-main {}

.pub-meta-top {
  display: flex;
  align-items: center;
  gap: 0.5rem;
  margin-bottom: 0.35rem;
  flex-wrap: wrap;
}

/* Type badges */
.badge-type {
  font-size: 0.62rem;
  font-weight: 500;
  letter-spacing: 0.1em;
  text-transform: uppercase;
  padding: 0.18rem 0.55rem;
  border-radius: 2px;
}
.badge-journal    { background: #e8f0fb; color: #1a3a70; }
.badge-conference { background: #fdf0e8; color: #7a3d14; }
.badge-poster     { background: #eef7ee; color: #2a5a2a; }
.badge-book       { background: #f0ecff; color: #3d1f80; }

/* Quartile badge */
.badge-q {
  font-size: 0.62rem;
  font-weight: 500;
  letter-spacing: 0.06em;
  padding: 0.18rem 0.55rem;
  border-radius: 2px;
  border: 1px solid;
}
.badge-q1 { background: #fffbf0; color: #b07d12; border-color: #e8cc78; }
.badge-q2 { background: #f9f9f9; color: #777;    border-color: #ddd; }

/* Note badge (Spotlight, etc.) */
.badge-note {
  font-size: 0.62rem;
  font-weight: 500;
  letter-spacing: 0.06em;
  padding: 0.18rem 0.55rem;
  border-radius: 2px;
  background: #fff3f0;
  color: #b03a2e;
  border: 1px solid #f5c0b8;
}

.pub-title {
  font-family: 'IBM Plex Sans', sans-serif;
  font-size: 0.93rem;
  font-weight: 400;
  line-height: 1.5;
  margin: 0 0 0.28rem;
}
.pub-title-link {
  color: #141416;
  text-decoration: none;
  transition: color 0.15s;
}
.pub-title-link:hover { color: #d4852a; }
.pub-title-nolink { color: #141416; }

.pub-authors {
  font-size: 0.78rem;
  color: #666;
  margin-bottom: 0.28rem;
  line-height: 1.4;
}

.pub-venue {
  font-size: 0.78rem;
  color: #555;
  font-style: italic;
  margin-bottom: 0.35rem;
}

.pub-if {
  font-size: 0.72rem;
  color: #999;
}

.pub-links {
  display: flex;
  align-items: center;
  gap: 0.8rem;
  margin-top: 0.5rem;
  flex-wrap: wrap;
}
.pub-link {
  font-size: 0.72rem;
  font-weight: 500;
  letter-spacing: 0.06em;
  text-transform: uppercase;
  color: #0d2b5e;
  text-decoration: none;
  display: flex;
  align-items: center;
  gap: 0.3rem;
  opacity: 0.8;
  transition: opacity 0.15s;
}
.pub-link:hover { opacity: 1; text-decoration: underline; text-underline-offset: 2px; }
.pub-link svg { flex-shrink: 0; }

/* ── No results ───────────────────────────────────────────── */
.pub-empty {
  display: none;
  text-align: center;
  padding: 3rem 0;
  color: #aaa;
  font-size: 0.88rem;
  letter-spacing: 0.04em;
}

/* ── Responsive ───────────────────────────────────────────── */
@media (max-width: 640px) {
  .metrics-bar { grid-template-columns: repeat(3, 1fr); }
  .metric-item:nth-child(3) { border-right: none; }
  .metric-item:nth-child(4),
  .metric-item:nth-child(5) { border-top: 1px solid #e2ddd8; }
  .pub-card { grid-template-columns: 1fr; }
  .pub-year-col { text-align: left; padding-bottom: 0.3rem; }
}
</style>

<div class="pub-page">

<!-- ── Metrics ─────────────────────────────────────────────── -->
<div class="metrics-bar">
  <div class="metric-item">
    <span class="metric-number">{{ all_pubs | size }}</span>
    <span class="metric-label">Total</span>
  </div>
  <div class="metric-item">
    <span class="metric-number">{{ journals | size }}</span>
    <span class="metric-label">Journals</span>
  </div>
  <div class="metric-item">
    <span class="metric-number">{{ q1_pubs | size }}</span>
    <span class="metric-label">Q1 Journals</span>
  </div>
  <div class="metric-item">
    <span class="metric-number">{{ metrics.citations }}</span>
    <span class="metric-label">Citations</span>
  </div>  
<div class="metric-item">
    <span class="metric-number">{{ metrics.h_index }}</span>
    <span class="metric-label">H-index</span>
  </div>
</div>

<!-- ── Controls ───────────────────────────────────────────── -->
<div class="pub-controls">

  <div class="control-row">
    <span class="control-label">Search</span>
    <div class="search-wrapper">
      <svg width="14" height="14" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
        <circle cx="11" cy="11" r="8"/><path d="m21 21-4.35-4.35"/>
      </svg>
      <input type="text" class="search-input" id="pub-search" placeholder="Title, author, journal…">
    </div>
  </div>

  <div class="control-row">
    <span class="control-label">Year</span>
    <button class="filter-pill active" data-filter="year" data-value="all">All</button>
    {% for y in years %}
    <button class="filter-pill" data-filter="year" data-value="{{ y }}">{{ y }}</button>
    {% endfor %}
  </div>

  <div class="control-row">
    <span class="control-label">Type</span>
    <button class="filter-pill active" data-filter="type" data-value="all">All</button>
    <button class="filter-pill" data-filter="type" data-value="journal">Journal</button>
    <button class="filter-pill" data-filter="type" data-value="conference">Conference</button>
    <button class="filter-pill" data-filter="type" data-value="poster">Poster / Abstract</button>
    <button class="filter-pill" data-filter="type" data-value="book">Book Chapter</button>
  </div>

  <div class="control-row">
    <span class="control-label">Rank</span>
    <button class="filter-pill active" data-filter="q" data-value="all">All</button>
    <button class="filter-pill" data-filter="q" data-value="Q1">Q1</button>
    <button class="filter-pill" data-filter="q" data-value="Q2">Q2</button>
  </div>

</div>

<!-- ── Count divider ──────────────────────────────────────── -->
<div class="pub-divider">
  <div class="pub-divider-line"></div>
  <span class="pub-count-label" id="pub-count-label">{{ all_pubs | size }} publications</span>
  <div class="pub-divider-line"></div>
</div>

<!-- ── Publication list ───────────────────────────────────── -->
<div class="pub-list" id="pub-list">
{% for pub in all_pubs %}
  {% assign search_blob = pub.title | downcase | append: ' ' | append: pub.authors | downcase | append: ' ' | append: pub.journal | downcase | append: ' ' | append: pub.venue | downcase | append: ' ' | append: pub.note | downcase %}
  <div class="pub-card"
       data-year="{{ pub.year }}"
       data-type="{{ pub.type }}"
       data-q="{{ pub.quartile }}"
       data-search="{{ search_blob | strip_html | escape }}">

    <div class="pub-year-col">{{ pub.year }}</div>

    <div class="pub-main">
      <div class="pub-meta-top">
        <span class="badge-type badge-{{ pub.type }}">
          {% if pub.type == "journal" %}Journal
          {% elsif pub.type == "conference" %}Conference
          {% elsif pub.type == "poster" %}Poster
          {% elsif pub.type == "book" %}Book Chapter
          {% else %}{{ pub.type }}{% endif %}
        </span>
        {% if pub.quartile %}
        <span class="badge-q badge-{{ pub.quartile | downcase }}">{{ pub.quartile }}</span>
        {% endif %}
        {% if pub.note %}
        <span class="badge-note">{{ pub.note }}</span>
        {% endif %}
      </div>

      <p class="pub-title">
        {% if pub.doi %}
        <a class="pub-title-link" href="{{ pub.doi }}" target="_blank" rel="noopener">{{ pub.title }}</a>
        {% else %}
        <span class="pub-title-nolink">{{ pub.title }}</span>
        {% endif %}
      </p>

      <p class="pub-authors">{{ pub.authors }}</p>

      <p class="pub-venue">
        {% if pub.journal %}{{ pub.journal }}{% endif %}
        {% if pub.journal and pub.venue %} · {% endif %}
        {% if pub.venue %}{{ pub.venue }}{% endif %}
      </p>

      {% if pub.impact_factor %}
      <p class="pub-if">{{ pub.metrics_detail }}</p>
      {% endif %}

      <div class="pub-links">
        {% if pub.doi %}
        <a class="pub-link" href="{{ pub.doi }}" target="_blank" rel="noopener">
          <svg width="11" height="11" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.2"><path d="M10 13a5 5 0 0 0 7.54.54l3-3a5 5 0 0 0-7.07-7.07l-1.72 1.71"/><path d="M14 11a5 5 0 0 0-7.54-.54l-3 3a5 5 0 0 0 7.07 7.07l1.71-1.71"/></svg>
          DOI
        </a>
        {% endif %}
        {% if pub.pdf %}
        <a class="pub-link" href="{{ pub.pdf }}" target="_blank" rel="noopener">
          <svg width="11" height="11" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.2"><path d="M14 2H6a2 2 0 0 0-2 2v16a2 2 0 0 0 2 2h12a2 2 0 0 0 2-2V8z"/><polyline points="14 2 14 8 20 8"/></svg>
          PDF
        </a>
        {% endif %}
        {% if pub.code %}
        <a class="pub-link" href="{{ pub.code }}" target="_blank" rel="noopener">
          <svg width="11" height="11" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.2"><polyline points="16 18 22 12 16 6"/><polyline points="8 6 2 12 8 18"/></svg>
          Code
        </a>
        {% endif %}
        {% if pub.scholar %}
        <a class="pub-link" href="{{ pub.scholar }}" target="_blank" rel="noopener">
          <svg width="11" height="11" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.2"><path d="M4 19.5A2.5 2.5 0 0 1 6.5 17H20"/><path d="M6.5 2H20v20H6.5A2.5 2.5 0 0 1 4 19.5v-15A2.5 2.5 0 0 1 6.5 2z"/></svg>
          Scholar
        </a>
        {% endif %}
      </div>
    </div>

  </div>
{% endfor %}
</div>

<p class="pub-empty" id="pub-empty">No publications match the current filters.</p>

</div><!-- /.pub-page -->

<script>
(function () {
  var cards       = Array.from(document.querySelectorAll('.pub-card'));
  var searchInput = document.getElementById('pub-search');
  var countLabel  = document.getElementById('pub-count-label');
  var emptyMsg    = document.getElementById('pub-empty');
  var active      = { year: 'all', type: 'all', q: 'all' };

  /* ── Filter logic ──────────────────────────────────────── */
  function applyFilters() {
    var term = searchInput.value.toLowerCase().trim();
    var visible = 0;

    cards.forEach(function (card) {
      var year   = card.dataset.year;
      var type   = card.dataset.type;
      var q      = card.dataset.q || '';
      var blob   = card.dataset.search || '';

      var ok =
        (active.year === 'all' || year  === active.year) &&
        (active.type === 'all' || type  === active.type) &&
        (active.q    === 'all' || q     === active.q)    &&
        (!term               || blob.indexOf(term) !== -1);

      card.classList.toggle('hidden', !ok);
      if (ok) visible++;
    });

    var total = cards.length;
    countLabel.textContent = visible === total
      ? total + ' publication' + (total !== 1 ? 's' : '')
      : visible + ' of ' + total + ' publication' + (total !== 1 ? 's' : '');

    emptyMsg.style.display = visible === 0 ? 'block' : 'none';
  }

  /* ── Pill buttons ──────────────────────────────────────── */
  document.querySelectorAll('.filter-pill').forEach(function (btn) {
    btn.addEventListener('click', function () {
      var dim = btn.dataset.filter;   /* year | type | q */
      var val = btn.dataset.value;

      /* deactivate siblings in same dimension */
      document.querySelectorAll('.filter-pill[data-filter="' + dim + '"]')
        .forEach(function (b) { b.classList.remove('active'); });

      btn.classList.add('active');
      active[dim] = val;
      applyFilters();
    });
  });

  /* ── Search input ──────────────────────────────────────── */
  searchInput.addEventListener('input', applyFilters);

  /* ── Init ──────────────────────────────────────────────── */
  applyFilters();
})();
</script>
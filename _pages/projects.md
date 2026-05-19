---
layout: archive
title: "Projects"
permalink: /projects/
author_profile: true
---

{% assign all_projects = site.data.projects %}
{% assign eu_projects  = all_projects | where: "funding_type", "european" %}
{% assign nat_projects = all_projects | where: "funding_type", "national" %}
{% assign reg_projects = all_projects | where: "funding_type", "regional" %}
{% assign prv_projects = all_projects | where: "funding_type", "private" %}
{% assign pi_projects  = all_projects | where: "role", "PI" %}
{% assign active_proj  = all_projects | where: "active", true %}

<style>
.proj-page * { box-sizing: border-box; }

.proj-page {
  font-family: 'IBM Plex Sans', sans-serif;
  font-weight: 300;
  color: #141416;
  max-width: 860px;
}

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

.proj-controls {
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
  min-width: 70px;
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
.filter-pill:hover { border-color: #0d2b5e; color: #0d2b5e; }
.filter-pill.active { background: #0d2b5e; border-color: #0d2b5e; color: #fff; }

.search-wrapper {
  position: relative;
  flex: 1;
  max-width: 360px;
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
}
.search-input:focus { border-color: #0d2b5e; }

.proj-divider {
  display: flex;
  align-items: center;
  gap: 1rem;
  margin-bottom: 1.6rem;
}
.proj-divider-line { flex: 1; height: 1px; background: #e2ddd8; }
.proj-count-label {
  font-size: 0.72rem;
  font-weight: 500;
  letter-spacing: 0.08em;
  text-transform: uppercase;
  color: #aaa;
  white-space: nowrap;
}

.proj-list { display: flex; flex-direction: column; }

.proj-card {
  padding: 1.1rem 0;
  border-bottom: 1px solid #eceae6;
  display: grid;
  grid-template-columns: 90px 90px 1fr;
  gap: 0 1.2rem;
}
.proj-card.hidden { display: none; }

.proj-date {
  font-family: 'IBM Plex Mono', monospace;
  font-size: 0.72rem;
  color: #bbb;
  padding-top: 0.22rem;
  text-align: right;
  letter-spacing: 0.03em;
  white-space: nowrap;
}

.proj-acronym {
  font-family: 'IBM Plex Mono', monospace;
  font-size: 0.72rem;
  color: #bbb;
  padding-top: 0.22rem;
  text-align: right;
  letter-spacing: 0.04em;
}

.proj-title {
  font-size: 0.93rem;
  font-weight: 400;
  line-height: 1.45;
  margin: 0 0 0.2rem;
}
.proj-title a {
  color: #141416;
  text-decoration: none;
}
.proj-title a:hover { color: #d4852a; }

.proj-sub {
  font-size: 0.78rem;
  color: #666;
  line-height: 1.5;
  margin: 0.15rem 0;
}

.badge-row {
  display: flex;
  flex-wrap: wrap;
  gap: 0.4rem;
  margin-top: 0.45rem;
}
.badge {
  font-size: 0.62rem;
  font-weight: 500;
  letter-spacing: 0.08em;
  text-transform: uppercase;
  padding: 0.18rem 0.55rem;
  border-radius: 2px;
}
.badge-eu         { background: #e8f0fb; color: #1a3a70; }
.badge-national   { background: #fdf0e8; color: #7a3d14; }
.badge-regional   { background: #eef7ee; color: #2a5a2a; }
.badge-private    { background: #f5f0ff; color: #3d1f80; }
.badge-pi         { background: #0d2b5e; color: #fff; }
.badge-co-pi      { background: #dde9fb; color: #1a3a70; }
.badge-researcher { background: #f5f5f5; color: #777; }
.badge-active     { background: #eef7ee; color: #2a5a2a; }
.badge-area       { background: #e8f0fb; color: #1a3a70; }

.proj-empty {
  display: none;
  text-align: center;
  padding: 3rem 0;
  color: #aaa;
  font-size: 0.88rem;
}

@media (max-width: 640px) {
  .metrics-bar { grid-template-columns: repeat(3, 1fr); }
  .metric-item:nth-child(3) { border-right: none; }
  .metric-item:nth-child(4),
  .metric-item:nth-child(5) { border-top: 1px solid #e2ddd8; }
  .proj-card { grid-template-columns: 1fr; }
  .proj-acronym { text-align: left; padding-bottom: 0.25rem; }
}
</style>

<div class="proj-page">

<div class="metrics-bar">
  <div class="metric-item">
    <span class="metric-number">{{ all_projects | size }}</span>
    <span class="metric-label">Total</span>
  </div>
  <div class="metric-item">
    <span class="metric-number">{{ eu_projects | size }}</span>
    <span class="metric-label">European</span>
  </div>
  <div class="metric-item">
    <span class="metric-number">{{ pi_projects | size }}</span>
    <span class="metric-label">PI</span>
  </div>
  <div class="metric-item">
    <span class="metric-number">{{ active_proj | size }}</span>
    <span class="metric-label">Active</span>
  </div>
  <div class="metric-item">
    <span class="metric-number">{{ nat_projects | size }}</span>
    <span class="metric-label">National</span>
  </div>
</div>

<div class="proj-controls">
  <div class="control-row">
    <span class="control-label">Search</span>
    <div class="search-wrapper">
      <svg width="14" height="14" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
        <circle cx="11" cy="11" r="8"/><path d="m21 21-4.35-4.35"/>
      </svg>
      <input type="text" class="search-input" id="proj-search" placeholder="Name, acronym, area...">
    </div>
  </div>

  <div class="control-row">
    <span class="control-label">Funding</span>
    <button class="filter-pill active" data-filter="funding" data-value="all">All</button>
    <button class="filter-pill" data-filter="funding" data-value="european">European</button>
    <button class="filter-pill" data-filter="funding" data-value="national">National</button>
    <button class="filter-pill" data-filter="funding" data-value="regional">Regional</button>
    <button class="filter-pill" data-filter="funding" data-value="private">Private</button>
  </div>

  <div class="control-row">
    <span class="control-label">Role</span>
    <button class="filter-pill active" data-filter="role" data-value="all">All</button>
    <button class="filter-pill" data-filter="role" data-value="PI">PI</button>
    <button class="filter-pill" data-filter="role" data-value="researcher">Researcher</button>
  </div>

  <div class="control-row">
    <span class="control-label">Status</span>
    <button class="filter-pill active" data-filter="active" data-value="all">All</button>
    <button class="filter-pill" data-filter="active" data-value="true">Active</button>
    <button class="filter-pill" data-filter="active" data-value="false">Finished</button>
  </div>
</div>

<div class="proj-divider">
  <div class="proj-divider-line"></div>
  <span class="proj-count-label" id="proj-count-label">{{ all_projects | size }} projects</span>
  <div class="proj-divider-line"></div>
</div>

<div class="proj-list" id="proj-list">
{% assign active_projects = all_projects | where: "active", true | sort: "year_end" %}
{% assign finished_projects = all_projects | where: "active", false | sort: "year_end" | reverse %}

{% for proj in active_projects %}
  {% assign area_text = proj.area | join: ' ' %}
  {% assign date_text = proj.year_start | append: "–" | append: "Present" %}
  {% assign search_blob = proj.name | append: ' ' | append: proj.acronym | append: ' ' | append: proj.description | append: ' ' | append: area_text | append: ' ' | append: date_text %}
  <div class="proj-card"
       data-funding="{{ proj.funding_type }}"
       data-role="{{ proj.role | default: 'researcher' }}"
       data-active="{{ proj.active }}"
       data-search="{{ search_blob | downcase | strip_html | escape }}">
    <div class="proj-acronym">{{ proj.acronym }}</div>
    <div class="proj-date">{{ date_text }}</div>
    <div>
      <p class="proj-title">
        {% if proj.url %}
          <a href="{{ proj.url }}" target="_blank" rel="noopener">{{ proj.name }}</a>
        {% elsif proj.doi %}
          <a href="{{ proj.doi }}" target="_blank" rel="noopener">{{ proj.name }}</a>
        {% else %}
          {{ proj.name }}
        {% endif %}
      </p>

      {% if proj.description %}
      <p class="proj-sub">{{ proj.description }}</p>
      {% endif %}

      <div class="badge-row">
        {% if proj.funding_type == "european" %}
          <span class="badge badge-eu">European</span>
        {% elsif proj.funding_type == "national" %}
          <span class="badge badge-national">National</span>
        {% elsif proj.funding_type == "regional" %}
          <span class="badge badge-regional">Regional</span>
        {% else %}
          <span class="badge badge-private">Private</span>
        {% endif %}

        {% if proj.role == "PI" %}
          <span class="badge badge-pi">PI</span>
        {% elsif proj.role == "co-PI" %}
          <span class="badge badge-co-pi">Co-PI</span>
        {% else %}
          <span class="badge badge-researcher">Researcher</span>
        {% endif %}

        {% if proj.active %}
          <span class="badge badge-active">Active</span>
        {% endif %}

        {% for a in proj.area %}
          <span class="badge badge-area">{{ a }}</span>
        {% endfor %}
      </div>
    </div>
  </div>
{% endfor %}

{% for proj in finished_projects %}
  {% assign area_text = proj.area | join: ' ' %}
  {% assign date_text = proj.year_start | append: "–" | append: proj.year_end %}
  {% assign search_blob = proj.name | append: ' ' | append: proj.acronym | append: ' ' | append: proj.description | append: ' ' | append: area_text | append: ' ' | append: date_text %}
  <div class="proj-card"
       data-funding="{{ proj.funding_type }}"
       data-role="{{ proj.role | default: 'researcher' }}"
       data-active="{{ proj.active }}"
       data-search="{{ search_blob | downcase | strip_html | escape }}">
    <div class="proj-acronym">{{ proj.acronym }}</div>
    <div class="proj-date">{{ date_text }}</div>
    <div>
      <p class="proj-title">
        {% if proj.url %}
          <a href="{{ proj.url }}" target="_blank" rel="noopener">{{ proj.name }}</a>
        {% elsif proj.doi %}
          <a href="{{ proj.doi }}" target="_blank" rel="noopener">{{ proj.name }}</a>
        {% else %}
          {{ proj.name }}
        {% endif %}
      </p>

      {% if proj.description %}
      <p class="proj-sub">{{ proj.description }}</p>
      {% endif %}

      <div class="badge-row">
        {% if proj.funding_type == "european" %}
          <span class="badge badge-eu">European</span>
        {% elsif proj.funding_type == "national" %}
          <span class="badge badge-national">National</span>
        {% elsif proj.funding_type == "regional" %}
          <span class="badge badge-regional">Regional</span>
        {% else %}
          <span class="badge badge-private">Private</span>
        {% endif %}

        {% if proj.role == "PI" %}
          <span class="badge badge-pi">PI</span>
        {% elsif proj.role == "co-PI" %}
          <span class="badge badge-co-pi">Co-PI</span>
        {% else %}
          <span class="badge badge-researcher">Researcher</span>
        {% endif %}

        {% for a in proj.area %}
          <span class="badge badge-area">{{ a }}</span>
        {% endfor %}
      </div>
    </div>
  </div>
{% endfor %}
</div>

<p class="proj-empty" id="proj-empty">No projects match the current filters.</p>
</div>

<script>
(function () {
  var cards = Array.from(document.querySelectorAll('.proj-card'));
  var searchInput = document.getElementById('proj-search');
  var countLabel = document.getElementById('proj-count-label');
  var emptyMsg = document.getElementById('proj-empty');
  var active = { funding: 'all', role: 'all', active: 'all' };

  function applyFilters() {
    var term = searchInput.value.toLowerCase().trim();
    var visible = 0;

    cards.forEach(function (card) {
      var funding = card.dataset.funding || '';
      var role = card.dataset.role || 'researcher';
      var isActive = card.dataset.active || 'false';
      var blob = card.dataset.search || '';

      var ok =
        (active.funding === 'all' || funding === active.funding) &&
        (active.role === 'all' || role === active.role) &&
        (active.active === 'all' || isActive === active.active) &&
        (!term || blob.indexOf(term) !== -1);

      card.classList.toggle('hidden', !ok);
      if (ok) visible++;
    });

    var total = cards.length;
    countLabel.textContent = visible === total
      ? total + ' project' + (total !== 1 ? 's' : '')
      : visible + ' of ' + total + ' project' + (total !== 1 ? 's' : '');

    emptyMsg.style.display = visible === 0 ? 'block' : 'none';
  }

  document.querySelectorAll('.filter-pill').forEach(function (btn) {
    btn.addEventListener('click', function () {
      var dim = btn.dataset.filter;
      var val = btn.dataset.value;

      document.querySelectorAll('.filter-pill[data-filter="' + dim + '"]')
        .forEach(function (b) { b.classList.remove('active'); });

      btn.classList.add('active');
      active[dim] = val;
      applyFilters();
    });
  });

  searchInput.addEventListener('input', applyFilters);
  applyFilters();
})();
</script>
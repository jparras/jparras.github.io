---
layout: archive
title: "Teaching"
permalink: /teaching/
author_profile: true
---

{% assign all_courses     = site.data.teaching %}
{% assign active_courses  = all_courses | where: "active", true %}
{% assign past_courses    = all_courses | where: "active", false %}
{% assign grad_courses    = all_courses | where: "level", "graduate" %}
{% assign all_theses      = site.data.theses %}
{% assign phd_theses      = all_theses  | where: "type", "phd" %}
{% assign master_theses   = all_theses  | where: "type", "master" %}
{% assign bachelor_theses = all_theses  | where: "type", "bachelor" %}

<style>
.teach-page * { box-sizing: border-box; }
.teach-page {
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

/* ── Section headers ── */
.teach-section { margin: 2.2rem 0 1rem; }
.teach-section-header {
  display: flex;
  align-items: center;
  gap: 1rem;
  margin-bottom: 1.1rem;
}
.teach-section-title {
  font-family: 'Playfair Display', serif;
  font-size: 1.05rem;
  font-weight: 600;
  color: #0d2b5e;
  white-space: nowrap;
}
.teach-section-line { flex: 1; height: 1px; background: #e2ddd8; }

.subsection-label {
  font-size: 0.68rem;
  font-weight: 500;
  letter-spacing: 0.1em;
  text-transform: uppercase;
  color: #8a8789;
  margin-bottom: 0.6rem;
}

/* ── Cards ── */
.teach-list { display: flex; flex-direction: column; }

.teach-card {
  display: grid;
  grid-template-columns: 90px 1fr;
  gap: 0 1.2rem;
  padding: 0.9rem 0;
  border-bottom: 1px solid #eceae6;
}
.teach-card:last-child { border-bottom: none; }

.teach-year {
  font-family: 'IBM Plex Mono', monospace;
  font-size: 0.7rem;
  color: #bbb;
  padding-top: 0.22rem;
  text-align: right;
  letter-spacing: 0.02em;
  white-space: nowrap;
}

.teach-title {
  font-size: 0.93rem;
  font-weight: 400;
  line-height: 1.45;
  margin: 0 0 0.18rem;
}
.teach-title a { color: #141416; text-decoration: none; }
.teach-title a:hover { color: #d4852a; }

.teach-sub {
  font-size: 0.78rem;
  color: #666;
  line-height: 1.5;
  margin: 0.1rem 0;
}
.teach-sub a { color: #0d2b5e; text-decoration: none; }
.teach-sub a:hover { text-decoration: underline; }

.teach-detail {
  font-size: 0.75rem;
  color: #999;
  font-style: italic;
  margin-top: 0.2rem;
}

/* ── Stats grid (for TFM/TFG) ── */
.thesis-stats {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 1px;
  background: #e2ddd8;
  border: 1px solid #e2ddd8;
  border-radius: 4px;
  overflow: hidden;
  margin-bottom: 0.6rem;
}
.thesis-stats-cell {
  background: #fff;
  padding: 0.9rem 1rem;
  text-align: center;
}
.thesis-stats-cell:hover { background: #faf7f3; }
.thesis-stats-number {
  display: block;
  font-family: 'Playfair Display', serif;
  font-size: 1.5rem;
  font-weight: 700;
  color: #0d2b5e;
  line-height: 1;
}
.thesis-stats-label {
  display: block;
  font-size: 0.65rem;
  font-weight: 500;
  letter-spacing: 0.08em;
  text-transform: uppercase;
  color: #8a8789;
  margin-top: 0.3rem;
}

/* ── Badges ── */
.badge-row { display: flex; flex-wrap: wrap; gap: 0.4rem; margin-top: 0.4rem; }
.badge {
  font-size: 0.62rem;
  font-weight: 500;
  letter-spacing: 0.08em;
  text-transform: uppercase;
  padding: 0.18rem 0.55rem;
  border-radius: 2px;
}
.badge-grad       { background: #f0ecff; color: #3d1f80; }
.badge-undergrad  { background: #fdf0e8; color: #7a3d14; }
.badge-english    { background: #f5f5f5; color: #555; }
.badge-spanish    { background: #fff8f0; color: #8b4513; }
.badge-active     { background: #eef7ee; color: #2a5a2a; }
.badge-phd        { background: #0d2b5e; color: #fff; }
.badge-note       { background: #fff3f0; color: #b03a2e; border: 1px solid #f5c0b8; }

@media (max-width: 640px) {
  .metrics-bar    { grid-template-columns: repeat(3, 1fr); }
  .thesis-stats   { grid-template-columns: repeat(2, 1fr); }
  .teach-card     { grid-template-columns: 1fr; }
  .teach-year     { text-align: left; padding-bottom: 0.2rem; }
}
</style>

<div class="teach-page">

<!-- ── Metrics ── -->
<div class="metrics-bar">
  <div class="metric-item">
    <span class="metric-number">{{ all_courses | size }}</span>
    <span class="metric-label">Courses</span>
  </div>
  <div class="metric-item">
    <span class="metric-number">{{ active_courses | size }}</span>
    <span class="metric-label">Active courses</span>
  </div>
  <div class="metric-item">
    <span class="metric-number">{{ phd_theses | size }}</span>
    <span class="metric-label">PhD Theses</span>
  </div>
  <div class="metric-item">
    <span class="metric-number">{{ master_theses | size }}</span>
    <span class="metric-label">Master's Theses</span>
  </div>
  <div class="metric-item">
    <span class="metric-number">{{ bachelor_theses | size }}</span>
    <span class="metric-label">Bachelor's Theses</span>
  </div>
</div>

<!-- ── Courses ── -->
<div class="teach-section">
  <div class="teach-section-header">
    <span class="teach-section-title">Courses</span>
    <div class="teach-section-line"></div>
  </div>

  <p class="subsection-label">Active</p>
  <div class="teach-list" style="margin-bottom: 1.6rem;">
    {% for course in active_courses %}
    <div class="teach-card">
      <div class="teach-year">{{ course.year_start }} –</div>
      <div>
        <p class="teach-title">{{ course.name }}</p>
        <p class="teach-sub">
          <a href="{{ course.degree_url }}" target="_blank" rel="noopener">{{ course.degree }}</a>
        </p>
        {% if course.description %}<p class="teach-detail">{{ course.description }}</p>{% endif %}
        <div class="badge-row">
          {% if course.level == "graduate" %}<span class="badge badge-grad">Graduate</span>
          {% else %}<span class="badge badge-undergrad">Undergraduate</span>{% endif %}
          {% if course.language == "English" %}<span class="badge badge-english">English</span>
          {% else %}<span class="badge badge-spanish">Spanish</span>{% endif %}
          <span class="badge badge-active">Active</span>
        </div>
      </div>
    </div>
    {% endfor %}
  </div>

  <p class="subsection-label">Past</p>
  <div class="teach-list">
    {% assign sorted_past = past_courses | sort: "year_end" | reverse %}
    {% for course in sorted_past %}
    <div class="teach-card">
      <div class="teach-year">{{ course.year_start }}–{{ course.year_end }}</div>
      <div>
        <p class="teach-title">{{ course.name }}</p>
        <p class="teach-sub">
          <a href="{{ course.degree_url }}" target="_blank" rel="noopener">{{ course.degree }}</a>
        </p>
        {% if course.description %}<p class="teach-detail">{{ course.description }}</p>{% endif %}
        <div class="badge-row">
          {% if course.level == "graduate" %}<span class="badge badge-grad">Graduate</span>
          {% else %}<span class="badge badge-undergrad">Undergraduate</span>{% endif %}
          {% if course.language == "English" %}<span class="badge badge-english">English</span>
          {% else %}<span class="badge badge-spanish">Spanish</span>{% endif %}
        </div>
      </div>
    </div>
    {% endfor %}
  </div>
</div>

<!-- ── PhD Theses ── -->
<div class="teach-section">
  <div class="teach-section-header">
    <span class="teach-section-title">PhD Theses Supervised</span>
    <div class="teach-section-line"></div>
  </div>

  <div class="teach-list">
    {% assign sorted_phd = phd_theses | sort: "year" | reverse %}
    {% for thesis in sorted_phd %}
    <div class="teach-card">
      <div class="teach-year">{{ thesis.year }}</div>
      <div>
        <p class="teach-title">
          {% if thesis.url %}<a href="{{ thesis.url }}" target="_blank" rel="noopener">{{ thesis.title }}</a>
          {% else %}{{ thesis.title }}{% endif %}
        </p>
        <p class="teach-sub">{{ thesis.student }}</p>
        {% if thesis.co-supervised %}
        <p class="teach-detail">Co-supervised with {{ thesis.co-supervised }}</p>
        {% endif %}
        <div class="badge-row">
          <span class="badge badge-phd">PhD</span>
          {% if thesis.note %}<span class="badge badge-note">{{ thesis.note }}</span>{% endif %}
        </div>
      </div>
    </div>
    {% endfor %}
  </div>
</div>

<!-- ── Master's & Bachelor's Theses (stats only) ── -->
<div class="teach-section">
  <div class="teach-section-header">
    <span class="teach-section-title">Master's &amp; Bachelor's Theses</span>
    <div class="teach-section-line"></div>
  </div>

  {% assign led_to_pub_m = 0 %}
  {% for t in master_theses %}{% if t.led_to_pub %}{% assign led_to_pub_m = led_to_pub_m | plus: 1 %}{% endif %}{% endfor %}
  {% assign noted_m = 0 %}
  {% for t in master_theses %}{% if t.note %}{% assign noted_m = noted_m | plus: 1 %}{% endif %}{% endfor %}

  <p class="subsection-label" style="margin-bottom: 0.8rem;">Master's Theses — {{ master_theses | size }} supervised</p>
  <div class="thesis-stats" style="margin-bottom: 1.4rem;">
    <div class="thesis-stats-cell">
      <span class="thesis-stats-number">{{ master_theses | size }}</span>
      <span class="thesis-stats-label">Total</span>
    </div>
    <div class="thesis-stats-cell">
      <span class="thesis-stats-number">{{ led_to_pub_m }}</span>
      <span class="thesis-stats-label">Led to publication</span>
    </div>
    <div class="thesis-stats-cell">
      <span class="thesis-stats-number">{{ noted_m }}</span>
      <span class="thesis-stats-label">Awarded</span>
    </div>
  </div>

  {% assign led_to_pub_b = 0 %}
  {% for t in bachelor_theses %}{% if t.led_to_pub %}{% assign led_to_pub_b = led_to_pub_b | plus: 1 %}{% endif %}{% endfor %}

  <p class="subsection-label" style="margin-bottom: 0.8rem;">Bachelor's Theses — {{ bachelor_theses | size }} supervised</p>
  <div class="thesis-stats">
    <div class="thesis-stats-cell">
      <span class="thesis-stats-number">{{ bachelor_theses | size }}</span>
      <span class="thesis-stats-label">Total</span>
    </div>
    <div class="thesis-stats-cell">
      <span class="thesis-stats-number">{{ led_to_pub_b }}</span>
      <span class="thesis-stats-label">Led to publication</span>
    </div>
    <div class="thesis-stats-cell">
      {% assign noted_b = 0 %}
      {% for t in bachelor_theses %}{% if t.note %}{% assign noted_b = noted_b | plus: 1 %}{% endif %}{% endfor %}
      <span class="thesis-stats-number">{{ noted_b }}</span>
      <span class="thesis-stats-label">Awarded</span>
    </div>
  </div>
</div>

</div><!-- /.teach-page -->
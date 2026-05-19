---
layout: archive
title: "CV"
permalink: /cv/
author_profile: true
redirect_from:
  - /resume
---

{% assign all_pubs     = site.data.publications %}
{% assign journals     = all_pubs   | where: "type", "journal" %}
{% assign q1_pubs      = journals   | where: "quartile", "Q1" %}
{% assign q2_pubs      = journals   | where: "quartile", "Q2" %}
{% assign conferences  = all_pubs   | where: "type", "conference" %}
{% assign all_projects  = site.data.projects %}
{% assign eu_projects  = all_projects | where: "funding_type", "european" %}
{% assign pi_projects  = all_projects | where: "role", "PI" %}
{% assign active_proj  = all_projects | where: "active", true %}
{% assign active_teach = site.data.teaching | where: "active", true %}
{% assign thesis_count   = site.data.theses %}
{% assign phd_theses   = thesis_count   | where: "type", "phd" %}
{% assign master_theses  = thesis_count   | where: "type", "master" %}
{% assign bachelor_theses  = thesis_count   | where: "type", "bachelor" %}
{% assign awards_own  = site.data.awards   | where: "type", "own" %}
{% assign awards_supervised  = site.data.awards   | where: "type", "supervised" %}

{% assign metrics = site.data.metrics %}

{% assign code_count = 0 %}
{% for pub in all_pubs %}{% if pub.code %}{% assign code_count = code_count | plus: 1 %}{% endif %}{% endfor %}

<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Playfair+Display:wght@600;700&family=IBM+Plex+Sans:ital,wght@0,300;0,400;0,500;1,300;1,400&family=IBM+Plex+Mono:wght@400&display=swap" rel="stylesheet">

<style>
/* ── Base ──────────────────────────────────────────────────── */
.cv-page * { box-sizing: border-box; }
.cv-page {
  font-family: 'IBM Plex Sans', sans-serif;
  font-weight: 300;
  color: #141416;
  max-width: 860px;
}

/* ── Metrics bar ───────────────────────────────────────────── */
.metrics-bar {
  display: grid;
  grid-template-columns: repeat(5, 1fr);
  gap: 0;
  border: 1px solid #e2ddd8;
  border-radius: 4px;
  margin: 1.8rem 0 2.6rem;
  overflow: hidden;
}
.metric-item {
  padding: 1.3rem 0.8rem;
  text-align: center;
  border-right: 1px solid #e2ddd8;
  transition: background 0.18s;
}
.metric-item:last-child { border-right: none; }
.metric-item:hover { background: #faf7f3; }
.metric-number {
  display: block;
  font-family: 'Playfair Display', serif;
  font-size: 2rem;
  font-weight: 700;
  color: #0d2b5e;
  line-height: 1;
  letter-spacing: -0.03em;
}
.metric-label {
  display: block;
  font-size: 0.65rem;
  font-weight: 500;
  letter-spacing: 0.09em;
  text-transform: uppercase;
  color: #8a8789;
  margin-top: 0.4rem;
}

/* ── Section headers ───────────────────────────────────────── */
.cv-section {
  margin: 2.6rem 0 1.4rem;
}
.cv-section-header {
  display: flex;
  align-items: center;
  gap: 1rem;
  margin-bottom: 1.2rem;
}
.cv-section-title {
  font-family: 'Playfair Display', serif;
  font-size: 1.05rem;
  font-weight: 600;
  color: #0d2b5e;
  white-space: nowrap;
  letter-spacing: 0.01em;
}
.cv-section-line {
  flex: 1;
  height: 1px;
  background: #e2ddd8;
}

/* ── Summary ───────────────────────────────────────────────── */
.cv-summary {
  font-size: 0.88rem;
  line-height: 1.75;
  color: #333;
  border-left: 3px solid #0d2b5e;
  padding-left: 1.2rem;
  margin-bottom: 0.5rem;
}

/* ── Timeline entries (education, experience, stays) ────────── */
.cv-list { display: flex; flex-direction: column; gap: 0; }

.cv-entry {
  display: grid;
  grid-template-columns: 100px 1fr;
  gap: 0 1.2rem;
  padding: 0.9rem 0;
  border-bottom: 1px solid #eceae6;
}
.cv-entry:last-child { border-bottom: none; }

.cv-entry-year {
  font-family: 'IBM Plex Mono', monospace;
  font-size: 0.7rem;
  color: #bbb;
  padding-top: 0.2rem;
  text-align: right;
  letter-spacing: 0.02em;
  line-height: 1.5;
}

.cv-entry-main {}

.cv-entry-title {
  font-size: 0.9rem;
  font-weight: 400;
  color: #141416;
  margin: 0 0 0.18rem;
  line-height: 1.45;
}
.cv-entry-title a {
  color: #141416;
  text-decoration: none;
  transition: color 0.15s;
}
.cv-entry-title a:hover { color: #d4852a; }

.cv-entry-sub {
  font-size: 0.78rem;
  color: #666;
  line-height: 1.5;
  margin: 0.1rem 0;
}
.cv-entry-sub a { color: #0d2b5e; text-decoration: none; }
.cv-entry-sub a:hover { text-decoration: underline; }

.cv-entry-detail {
  font-size: 0.75rem;
  color: #999;
  margin-top: 0.2rem;
  font-style: italic;
}

/* ── Badges ────────────────────────────────────────────────── */
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
.badge-researcher { background: #f5f5f5; color: #777; }
.badge-active     { background: #eef7ee; color: #2a5a2a; }
.badge-english    { background: #f5f5f5; color: #555; }
.badge-spanish    { background: #fff8f0; color: #8b4513; }
.badge-grad       { background: #f0ecff; color: #3d1f80; }
.badge-undergrad  { background: #fdf0e8; color: #7a3d14; }
.badge-area       { background: #e8f0fb; color: #1a3a70; }
.badge-q1         { background: #fffbf0; color: #b07d12; border: 1px solid #e8cc78; }
.badge-q2         { background: #f9f9f9; color: #777; border: 1px solid #ddd; }
.badge-winner     { background: #fff8f0; color: #b07d12; border: 1px solid #e8cc78; }
.badge-accesit    { background: #f5f5f5; color: #666; }
.badge-phd        { background: #0d2b5e; color: #fff; }
.badge-master     { background: #e8f0fb; color: #1a3a70; }
.badge-bachelor   { background: #fdf0e8; color: #7a3d14; }

/* ── Project cards ─────────────────────────────────────────── */
.project-card {
  display: grid;
  grid-template-columns: 100px 1fr;
  gap: 0 1.2rem;
  padding: 0.9rem 0;
  border-bottom: 1px solid #eceae6;
}
.project-card:last-child { border-bottom: none; }

.project-acronym {
  font-family: 'IBM Plex Mono', monospace;
  font-size: 0.72rem;
  color: #bbb;
  padding-top: 0.2rem;
  text-align: right;
  letter-spacing: 0.04em;
}

/* ── Award cards ───────────────────────────────────────────── */
.award-entry {
  display: grid;
  grid-template-columns: 100px 1fr;
  gap: 0 1.2rem;
  padding: 0.9rem 0;
  border-bottom: 1px solid #eceae6;
}
.award-entry:last-child { border-bottom: none; }
.award-year {
  font-family: 'IBM Plex Mono', monospace;
  font-size: 0.7rem;
  color: #bbb;
  padding-top: 0.2rem;
  text-align: right;
}

/* ── Publications summary ──────────────────────────────────── */
.pub-summary-grid {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  gap: 1px;
  background: #e2ddd8;
  border: 1px solid #e2ddd8;
  border-radius: 4px;
  overflow: hidden;
  margin-bottom: 1rem;
}
.pub-summary-cell {
  background: #fff;
  padding: 1rem;
  text-align: center;
}
.pub-summary-cell:hover { background: #faf7f3; }
.pub-summary-number {
  display: block;
  font-family: 'Playfair Display', serif;
  font-size: 1.6rem;
  font-weight: 700;
  color: #0d2b5e;
  line-height: 1;
}
.pub-summary-label {
  display: block;
  font-size: 0.65rem;
  font-weight: 500;
  letter-spacing: 0.08em;
  text-transform: uppercase;
  color: #8a8789;
  margin-top: 0.35rem;
}

/* ── CTA link ──────────────────────────────────────────────── */
.cv-cta {
  font-size: 0.78rem;
  color: #0d2b5e;
  text-decoration: none;
  font-weight: 500;
  letter-spacing: 0.04em;
  display: inline-flex;
  align-items: center;
  gap: 0.3rem;
  transition: color 0.15s;
}
.cv-cta:hover { color: #d4852a; }

/* ── Teaching grid ─────────────────────────────────────────── */
.teaching-section { margin-bottom: 1.2rem; }
.teaching-section-label {
  font-size: 0.68rem;
  font-weight: 500;
  letter-spacing: 0.1em;
  text-transform: uppercase;
  color: #8a8789;
  margin-bottom: 0.6rem;
}

/* ── Responsive ────────────────────────────────────────────── */
@media (max-width: 640px) {
  .metrics-bar        { grid-template-columns: repeat(3, 1fr); }
  .pub-summary-grid   { grid-template-columns: repeat(2, 1fr); }
  .cv-entry,
  .project-card,
  .award-entry        { grid-template-columns: 1fr; }
  .cv-entry-year,
  .project-acronym,
  .award-year         { text-align: left; padding-bottom: 0.2rem; }
}
</style>

<div class="cv-page">

<!-- ── Metrics ──────────────────────────────────────────────── -->
<div class="metrics-bar">
  <div class="metric-item">
    <span class="metric-number">{{ all_pubs | size }}</span>
    <span class="metric-label">Publications</span>
  </div>
  <div class="metric-item">
    <span class="metric-number">{{ q1_pubs | size }}</span>
    <span class="metric-label">Q1 Journals</span>
  </div>
  <div class="metric-item">
    <span class="metric-number">{{ all_projects | size }}</span>
    <span class="metric-label">R&D Projects</span>
  </div>
  <div class="metric-item">
    <span class="metric-number">{{ metrics.h_index }}</span>
    <span class="metric-label">H-index</span>
  </div>
  <div class="metric-item">
    <span class="metric-number">{{ awards_own | size }}</span>
    <span class="metric-label">Awards</span>
  </div>
</div>

<!-- ── Summary ──────────────────────────────────────────────── -->
<div class="cv-section">
  <div class="cv-section-header">
    <span class="cv-section-title">Summary</span>
    <div class="cv-section-line"></div>
  </div>
  <p class="cv-summary"> Juan Parras is an Associate Professor (Profesor Contratado Doctor) at Universidad Politécnica de Madrid (UPM), where he has worked since 2015. He holds a PhD in Telecommunication Technologies and Systems (UPM, 2020, Cum Laude, International Mention), a Master's in Telecommunications Engineering (UPM, 2016, GPA 9.11, awarded for Excellent Academic Performance), and a Bachelor's in Telecommunication Technologies Engineering (Universidad de Jaén, 2014, GPA 9.59, Best Academic Record). </p>
  <p class="cv-summary"> His research sits at the intersection of optimization (including optimal control and game theory) and statistical learning, with applications in AI for healthcare, secure communications, autonomous underwater navigation, and industry. His research has been funded by {{ all_projects | size }} funded projects, including {{ eu_projects | size }} European projects and {{ pi_projects | size }} projects where he is the Principal Investigator. His research results have been published in internationally recognized venues: to date, Juan has authored {{ all_pubs | size }} publications, including {{ journals | size }} journals ({{q1_pubs | size}} in JCR Q1 journals, {{q2_pubs | size}} in JCR Q2 journals) and {{conferences | size}} conference papers. Being commited to facilitate the replication and dissemination of his research results, his webpage contains the code for most of his research outputs. </p>
  <p class="cv-summary"> Juan also plays a significant role in education. Since the 2018–2019 academic year, he has been teaching at UPM and was awarded an "Excellent" rating in the Docentia teaching evaluation in 2023. Additionally, he has mentored numerous young researchers, supervising {{ bachelor_theses | size }} Bachelor's and {{ master_theses | size }} Master's theses, several of which have led to publications in journals or conferences, as well as {{phd_theses | size}} PhD theses. </p>
  <p class="cv-summary"> Regarding awards, Juan has received {{ awards_own | size }} distinctions, including the Best Signal Processing Thesis from the Spanish Chapter of IEEE in Communications and Signal Processing. He got also an accésit in the Luis Felipe Torrente divulgation award in medicine (2025). Finally, his students have also received {{awards_supervised | size}} awards. </p>
</div>

<!-- ── Education ────────────────────────────────────────────── -->
<div class="cv-section">
  <div class="cv-section-header">
    <span class="cv-section-title">Education</span>
    <div class="cv-section-line"></div>
  </div>
  <div class="cv-list">

    <div class="cv-entry">
      <div class="cv-entry-year">2016 – 2020</div>
      <div class="cv-entry-main">
        <p class="cv-entry-title">PhD in Telecommunication Technologies and Systems</p>
        <p class="cv-entry-sub"><a href="https://www.upm.es/">Universidad Politécnica de Madrid</a></p>
        <p class="cv-entry-detail">Cum Laude · International Mention · Program: Communications Technologies and Systems</p>
        <p class="cv-entry-detail">PhD Thesis: <a href="../files/2020-thesis.pdf">Adversarial detection games in network security applications with imperfect and incomplete information</a>, <a href="https://doi.org/10.20868/UPM.thesis.57986">DOI</a></p>
      </div>
    </div>

    <div class="cv-entry">
      <div class="cv-entry-year">2014 – 2016</div>
      <div class="cv-entry-main">
        <p class="cv-entry-title">Master's Degree in Telecommunications Engineering</p>
        <p class="cv-entry-sub"><a href="https://www.upm.es/">Universidad Politécnica de Madrid</a></p>
        <p class="cv-entry-detail">GPA 9.11 · Excellence Mention</p>
        <p class="cv-entry-detail">Master's Thesis: <a href="../files/2016-tfm.pdf">Development of an application based on dynamic game theory for designing optimal trajectories for two UAVs in a jamming problem</a></p>
      </div>
    </div>

    <div class="cv-entry">
      <div class="cv-entry-year">2023 – 2026</div>
      <div class="cv-entry-main">
        <p class="cv-entry-title">Master of Arts in Theology</p>
        <p class="cv-entry-sub">
          <a href="https://kairos.edu/">Kairos</a> &amp;
          <a href="https://tsr.de/">Theologische Seminar Rheinland</a>
        </p>
      </div>
    </div>


    <div class="cv-entry">
      <div class="cv-entry-year">2010 – 2014</div>
      <div class="cv-entry-main">
        <p class="cv-entry-title">Bachelor's Degree in Telecommunication Technologies Engineering</p>
        <p class="cv-entry-sub"><a href="https://www.ujaen.es/">Universidad de Jaén</a></p>
        <p class="cv-entry-detail">GPA 9.59 · Best Academic Record · Tracks: Telecommunications Systems, Image and Sound · Erasmus: <a href="https://www.thm.de/site/">Technische Hochschule Mittelhessen</a> (Germany)</p>
        <p class="cv-entry-detail">Bachelor's Thesis: <a href="../files/2014-tfg.pdf">Analysis and comparison of different indoor location methods</a></p>
      </div>
    </div>

    <div class="cv-entry">
      <div class="cv-entry-year">2012 – 2022</div>
      <div class="cv-entry-main">
        <p class="cv-entry-title">Bachelor's Degree in Theology</p>
        <p class="cv-entry-sub"><a href="https://eetfieide.com/">Escuela Evangélica de Teología</a></p>
      </div>
    </div>

  </div>
</div>

<!-- ── Work Experience ───────────────────────────────────────── -->
<div class="cv-section">
  <div class="cv-section-header">
    <span class="cv-section-title">Work Experience</span>
    <div class="cv-section-line"></div>
  </div>
  <div class="cv-list">

    <div class="cv-entry">
      <div class="cv-entry-year">2023 – Today</div>
      <div class="cv-entry-main">
        <p class="cv-entry-title">Associate Professor <span style="font-weight:300; color:#888">(Profesor Contratado Doctor)</span></p>
        <p class="cv-entry-sub"><a href="https://www.upm.es/">Universidad Politécnica de Madrid</a>, Spain</p>
      </div>
    </div>

    <div class="cv-entry">
      <div class="cv-entry-year">2020 – 2023</div>
      <div class="cv-entry-main">
        <p class="cv-entry-title">Assistant Professor <span style="font-weight:300; color:#888">(Profesor Ayudante Doctor)</span></p>
        <p class="cv-entry-sub"><a href="https://www.upm.es/">Universidad Politécnica de Madrid</a>, Spain</p>
      </div>
    </div>

    <div class="cv-entry">
      <div class="cv-entry-year">2019 – 2020</div>
      <div class="cv-entry-main">
        <p class="cv-entry-title">Teaching &amp; Research Assistant <span style="font-weight:300; color:#888">(Ayudante)</span></p>
        <p class="cv-entry-sub"><a href="https://www.upm.es/">Universidad Politécnica de Madrid</a>, Spain</p>
      </div>
    </div>

    <div class="cv-entry">
      <div class="cv-entry-year">2016 – 2019</div>
      <div class="cv-entry-main">
        <p class="cv-entry-title">PhD Candidate</p>
        <p class="cv-entry-sub"><a href="https://www.upm.es/">Universidad Politécnica de Madrid</a>, Spain</p>
      </div>
    </div>

    <div class="cv-entry">
      <div class="cv-entry-year">2015 – 2016</div>
      <div class="cv-entry-main">
        <p class="cv-entry-title">Research Internship</p>
        <p class="cv-entry-sub"><a href="https://www.upm.es/">Universidad Politécnica de Madrid</a>, Spain</p>
      </div>
    </div>

    <div class="cv-entry">
      <div class="cv-entry-year">2014</div>
      <div class="cv-entry-main">
        <p class="cv-entry-title">Research Internship</p>
        <p class="cv-entry-sub"><a href="https://www.transmit.de/">Transmit GmbH</a>, Germany</p>
      </div>
    </div>

  </div>
</div>

<!-- ── Publications ──────────────────────────────────────────── -->
<div class="cv-section">
  <div class="cv-section-header">
    <span class="cv-section-title">Publications</span>
    <div class="cv-section-line"></div>
  </div>

  <div class="pub-summary-grid">
    <div class="pub-summary-cell">
      <span class="pub-summary-number">{{ journals | size }}</span>
      <span class="pub-summary-label">Journal Papers</span>
    </div>
    <div class="pub-summary-cell">
      <span class="pub-summary-number">{{ q1_pubs | size }}</span>
      <span class="pub-summary-label">Q1 Journals</span>
    </div>
    <div class="pub-summary-cell">
      <span class="pub-summary-number">{{ metrics.citations }}</span>
      <span class="pub-summary-label">Citations</span>
    </div>
    <div class="pub-summary-cell">
      <span class="pub-summary-number">{{ metrics.h_index }}</span>
      <span class="pub-summary-label">H-index</span>
    </div>
  </div>

  <a class="cv-cta" href="../publications">
    <svg width="13" height="13" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M14 2H6a2 2 0 0 0-2 2v16a2 2 0 0 0 2 2h12a2 2 0 0 0 2-2V8z"/><polyline points="14 2 14 8 20 8"/></svg>
    Browse full publication list →
  </a>
</div>

<!-- ── Research Projects ─────────────────────────────────────── -->
<div class="cv-section">
  <div class="cv-section-header">
    <span class="cv-section-title">Research Projects</span>
    <div class="cv-section-line"></div>
  </div>

  <div class="pub-summary-grid">
    <div class="pub-summary-cell">
      <span class="pub-summary-number">{{ all_projects | size }}</span>
      <span class="pub-summary-label">Total Projects</span>
    </div>
    <div class="pub-summary-cell">
      <span class="pub-summary-number">{{ eu_projects | size }}</span>
      <span class="pub-summary-label">EU Projects</span>
    </div>
    <div class="pub-summary-cell">
      <span class="pub-summary-number">{{ pi_projects | size }}</span>
      <span class="pub-summary-label">As PI</span>
    </div>
    <div class="pub-summary-cell">
      <span class="pub-summary-number">{{ active_proj | size }}</span>
      <span class="pub-summary-label">Active</span>
    </div>
  </div>

  <a class="cv-cta" href="../projects">
    <svg width="13" height="13" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
      <path d="M14 2H6a2 2 0 0 0-2 2v16a2 2 0 0 0 2 2h12a2 2 0 0 0 2-2V8z"/>
      <polyline points="14 2 14 8 20 8"/>
    </svg>
    Browse full project list →
  </a>
</div>

<!-- ── Research Stays ────────────────────────────────────────── -->
<div class="cv-section">
  <div class="cv-section-header">
    <span class="cv-section-title">Research Stays</span>
    <div class="cv-section-line"></div>
  </div>
  <div class="cv-list">

    <div class="cv-entry">
      <div class="cv-entry-year">2025</div>
      <div class="cv-entry-main">
        <p class="cv-entry-title">Postdoctoral Research Stay · 1.5 months</p>
        <p class="cv-entry-sub">
          <a href="https://www.icv.csic.es/" target="_blank" rel="noopener">Instituto de Cerámica y Vidrio</a>,
          <a href="https://www.csic.es/es" target="_blank" rel="noopener">CSIC</a>, Spain
        </p>
      </div>
    </div>

    <div class="cv-entry">
      <div class="cv-entry-year">2018</div>
      <div class="cv-entry-main">
        <p class="cv-entry-title">Predoctoral Research Stay · 3.5 months</p>
        <p class="cv-entry-sub">
          <a href="https://lcas.lincoln.ac.uk/wp/" target="_blank" rel="noopener">Lincoln Centre for Autonomous Systems</a>,
          <a href="https://www.lincoln.ac.uk/" target="_blank" rel="noopener">University of Lincoln</a>, United Kingdom
        </p>
      </div>
    </div>

  </div>
</div>

<!-- ── Teaching ──────────────────────────────────────────────── -->
<div class="cv-section">
  <div class="cv-section-header">
    <span class="cv-section-title">Teaching</span>
    <div class="cv-section-line"></div>
  </div>

  <div class="pub-summary-grid">
    <div class="pub-summary-cell">
      <span class="pub-summary-number">{{ site.data.teaching | size }}</span>
      <span class="pub-summary-label">Courses</span>
    </div>
    <div class="pub-summary-cell">
      <span class="pub-summary-number">{{ phd_theses | size }}</span>
      <span class="pub-summary-label">PhD Theses</span>
    </div>
    <div class="pub-summary-cell">
      <span class="pub-summary-number">{{ master_theses | size }}</span>
      <span class="pub-summary-label">Master's Theses</span>
    </div>
    <div class="pub-summary-cell">
      <span class="pub-summary-number">{{ bachelor_theses | size }}</span>
      <span class="pub-summary-label">Bachelor's Theses</span>
    </div>
  </div>

  <a class="cv-cta" href="../teaching">
    <svg width="13" height="13" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
      <path d="M12 2L2 7l10 5 10-5-10-5z"/><path d="M2 17l10 5 10-5"/><path d="M2 12l10 5 10-5"/>
    </svg>
    Browse full teaching record →
  </a>
</div>

<!-- ── Awards ────────────────────────────────────────────────── -->
<div class="cv-section">
  <div class="cv-section-header">
    <span class="cv-section-title">Awards &amp; Distinctions</span>
    <div class="cv-section-line"></div>
  </div>

  <div class="teaching-section">
    <p class="teaching-section-label">Awards</p>
    <div class="cv-list">
      {% assign sorted_own = awards_own | sort: "year" | reverse %}
      {% for award in sorted_own %}
      <div class="award-entry">
        <div class="award-year">{{ award.year }}</div>
        <div class="cv-entry-main">
          <p class="cv-entry-title">
            {% if award.url %}<a href="{{ award.url }}" target="_blank" rel="noopener">{{ award.name }}</a>
            {% else %}{{ award.name }}{% endif %}
          </p>
          {% if award.awarded_by %}
          <p class="cv-entry-sub">{{ award.awarded_by }}</p>
          {% endif %}
          {% if award.description %}
          <p class="cv-entry-detail">{{ award.description }}</p>
          {% endif %}
          <div class="badge-row">
            <span class="badge badge-winner">{{ award.result | capitalize }}</span>
          </div>
        </div>
      </div>
      {% endfor %}
    </div>
  </div>

  <div class="teaching-section" style="margin-top: 1.4rem;">
    <p class="teaching-section-label">Awards to students</p>
    <div class="cv-list">
      {% assign sorted_sup = awards_supervised | sort: "year" | reverse %}
      {% for award in sorted_sup %}
      <div class="award-entry">
        <div class="award-year">{{ award.year }}</div>
        <div class="cv-entry-main">
          <p class="cv-entry-title">
            {% if award.url %}<a href="{{ award.url }}" target="_blank" rel="noopener">{{ award.name }}</a>
            {% else %}{{ award.name }}{% endif %}
          </p>
          {% if award.awarded_by %}
          <p class="cv-entry-sub">{{ award.awarded_by }}</p>
          {% endif %}
          {% if award.description %}
          <p class="cv-entry-detail">{{ award.description }}</p>
          {% endif %}
          <div class="badge-row">
            <span class="badge badge-winner">{{ award.result | capitalize }}</span>
          </div>
        </div>
      </div>
      {% endfor %}
    </div>
  </div>

</div>

</div><!-- /.cv-page -->
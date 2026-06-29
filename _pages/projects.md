---
layout: editorial
title: "Projects"
permalink: /projects/
excerpt: "Larger research agendas and the papers within them."
author_profile: false
heading: "Projects"
dek: "Ongoing research agendas, each gathering related papers and work."
---

<header class="page-head">
  <div class="kicker">Projects</div>
  <h1 class="page-head__title">{{ page.heading | default: page.title }}</h1>
  {% if page.dek %}<p class="page-head__dek">{{ page.dek }}</p>{% endif %}
</header>

{% assign agendas = site.data.projects | where_exp: "a", "a.title" %}
{% if agendas and agendas.size > 0 %}
  {% for agenda in agendas %}
    <section class="project">
      <div class="section-rule">
        <h2>{{ agenda.title }}</h2>
        <span class="rule"></span>
      </div>
      {% if agenda.description %}<p class="project__dek">{{ agenda.description }}</p>{% endif %}
      {% if agenda.papers %}
        {% for paper in agenda.papers %}
          {% include research-entry.html item=paper %}
        {% endfor %}
      {% endif %}
    </section>
  {% endfor %}
{% else %}
  <p class="empty-note">No projects added yet.</p>
{% endif %}

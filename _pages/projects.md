---
layout: editorial
title: "Projects"
permalink: /projects/
excerpt: "Larger research agendas and the papers within them."
author_profile: false
heading: "Projects"
dek: "Ongoing research agendas. Click a project to see what it is about and the related papers."
---

<header class="page-head">
  <div class="kicker">Projects</div>
  <h1 class="page-head__title">{{ page.heading | default: page.title }}</h1>
  {% if page.dek %}<p class="page-head__dek">{{ page.dek }}</p>{% endif %}
</header>

{% assign agendas = site.data.projects | where_exp: "a", "a.title" %}
{% if agendas and agendas.size > 0 %}
  <div class="projects-grid">
    {% for agenda in agendas %}
      <details class="proj">
        <summary class="proj__summary">
          <span class="proj__photo">
            {% if agenda.photo %}<img src="{{ agenda.photo | relative_url }}" alt="{{ agenda.title }}" loading="lazy">{% endif %}
          </span>
          <span class="proj__bar">
            <span class="proj__title">{{ agenda.title }}</span>
            <span class="proj__toggle" aria-hidden="true"></span>
          </span>
        </summary>
        <div class="proj__body">
          {% if agenda.description %}<p class="proj__desc">{{ agenda.description }}</p>{% endif %}
          {% if agenda.papers %}
            <ul class="proj__papers">
              {% for paper in agenda.papers %}
                <li class="proj__paper">
                  <p class="proj__paper-title">{{ paper.title }}</p>
                  {% if paper.venue or paper.year %}
                    <p class="proj__paper-meta">{% if paper.venue %}{{ paper.venue }}{% endif %}{% if paper.venue and paper.year %} · {% endif %}{% if paper.year %}{{ paper.year }}{% endif %}</p>
                  {% endif %}
                  {% if paper.links %}
                    <p class="proj__paper-links">{% for link in paper.links %}<a class="arrow-link" href="{{ link.url }}" target="_blank" rel="noopener">{{ link.label }} →</a>{% endfor %}</p>
                  {% endif %}
                </li>
              {% endfor %}
            </ul>
          {% endif %}
        </div>
      </details>
    {% endfor %}
  </div>
{% else %}
  <p class="empty-note">No projects added yet.</p>
{% endif %}

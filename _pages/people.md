---
layout: editorial
title: "People"
permalink: /people/
excerpt: "Students, co-authors, and collaborators."
author_profile: false
heading: "People"
dek: "Students I have supervised, co-authors, and people I have worked with."
---

<header class="page-head">
  <div class="kicker">People</div>
  <h1 class="page-head__title">{{ page.heading | default: page.title }}</h1>
  {% if page.dek %}<p class="page-head__dek">{{ page.dek }}</p>{% endif %}
</header>

{% assign groups = site.data.people | where_exp: "g", "g.group" %}
{% if groups and groups.size > 0 %}
  {% for group in groups %}
    <section class="people-group">
      <div class="section-rule">
        <h2>{{ group.group }}</h2>
        <span class="rule"></span>
      </div>
      {% if group.members %}
        <ul class="people-list">
          {% for person in group.members %}
            <li class="person">
              <p class="person__name">
                {% if person.url %}<a href="{{ person.url }}" target="_blank" rel="noopener">{{ person.name }}</a>{% else %}{{ person.name }}{% endif %}
              </p>
              {% if person.role %}<p class="person__role">{{ person.role }}</p>{% endif %}
              {% if person.note %}<p class="person__note">{{ person.note }}</p>{% endif %}
            </li>
          {% endfor %}
        </ul>
      {% endif %}
    </section>
  {% endfor %}
{% else %}
  <p class="empty-note">No people added yet.</p>
{% endif %}

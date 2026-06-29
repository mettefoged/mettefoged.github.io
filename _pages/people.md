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
<h1 class="page-head__title">{{ page.heading | default: page.title }}</h1>
{% if page.dek %}<p class="page-head__dek">{{ page.dek }}</p>{% endif %}
</header>

{% assign groups = site.data.people | where_exp: "g", "g.group" %}
{% if groups and groups.size > 0 %}
{% for group in groups %}
<section class="people-group">
<div class="section-rule"><h2>{{ group.group }}</h2><span class="rule"></span></div>
{% if group.members %}
<ul class="people-grid">
{% for member in group.members %}
{%- assign co = nil -%}
{%- if member.key %}{% assign co = site.data.coauthors[member.key] %}{% endif -%}
{%- assign p_name = member.name | default: co.name -%}
{%- assign p_url = member.url | default: co.url -%}
{%- assign p_role = member.role | default: co.role -%}
{%- assign p_affil = member.affiliation | default: co.affiliation -%}
{%- assign p_photo = member.photo | default: co.photo -%}
{%- if p_photo and p_photo != "" %}{% unless p_photo contains "/" %}{% assign p_photo = p_photo | prepend: "/images/people/" %}{% endunless %}{% endif -%}
<li class="pcard">
{% if p_url %}<a class="pcard__link" href="{{ p_url }}" target="_blank" rel="noopener">{% endif %}
<div class="pcard__photo">{% if p_photo %}<img src="{{ p_photo | relative_url }}" alt="{{ p_name }}" loading="lazy">{% else %}<span class="pcard__initial">{{ p_name | strip | slice: 0, 1 }}</span>{% endif %}</div>
<p class="pcard__name">{{ p_name }}</p>
{% if p_role %}<p class="pcard__role">{{ p_role }}</p>{% endif %}
{% if p_affil %}<p class="pcard__affil">{{ p_affil }}</p>{% endif %}
{% if p_url %}</a>{% endif %}
</li>
{% endfor %}
</ul>
{% endif %}
</section>
{% endfor %}
{% else %}
<p class="empty-note">No people added yet.</p>
{% endif %}

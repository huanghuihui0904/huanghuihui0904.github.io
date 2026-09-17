---
layout: page
permalink: /bugs/
title: Found Bugs
nav: true
nav_order: 3
---

{% assign bugs = site.data.bugs %}

<p class="bug-count">{{ bugs.size }} bugs found so far.</p>

<style>
  .bug-count { color: var(--global-text-color-light); margin-top: -0.5rem; margin-bottom: 1.2rem; font-size: 0.95rem; }
  table.bug-table { width: 100%; }
  table.bug-table td, table.bug-table th { vertical-align: middle; }
  table.bug-table td.id { text-align: right; color: var(--global-text-color-light); width: 3em; }
  .bug-badge { display: inline-block; padding: 0.12em 0.5em; border-radius: 6px; font-size: 0.72rem; font-weight: 600; white-space: nowrap; background: var(--global-theme-color); color: #fff; }
  .bug-badge a, .bug-badge a:hover, .bug-badge a:focus { color: #fff !important; text-decoration: none !important; background-image: none !important; border-bottom: none !important; }
  .cvss-badge { display: inline-block; padding: 0.12em 0.5em; border-radius: 6px; font-size: 0.72rem; font-weight: 600; white-space: nowrap; color: #fff; }
  .cvss-badge.critical { background: #b30000; }
  .cvss-badge.high { background: #d9534f; }
  .cvss-badge.medium { background: #f0ad4e; }
  .cvss-badge.low { background: #5cb85c; }
  .cve-line { display: block; margin-top: 0.2em; font-size: 0.78rem; }
</style>

<table class="table table-sm bug-table">
  <thead>
    <tr>
      <th>ID</th>
      <th>Project</th>
      <th>Bug ID</th>
      <th>Type</th>
      <th>Method</th>
    </tr>
  </thead>
  <tbody>
    {% for b in bugs %}
    <tr>
      <td class="id">{{ forloop.index }}</td>
      <td>{% if b.project_url %}<a href="{{ b.project_url }}">{{ b.project }}</a>{% else %}{{ b.project }}{% endif %}</td>
      <td>
        <a href="{{ b.link }}" target="_blank" rel="noopener">{% if b.bug_id %}{{ b.bug_id }}{% else %}report{% endif %}</a>
        {% if b.cve and b.cve != "" %}
          <span class="cve-line">
            <a href="https://www.cve.org/CVERecord?id={{ b.cve }}" target="_blank" rel="noopener">{{ b.cve }}</a>
            {% if b.severity %}
              {% assign skey = b.severity | downcase %}
              <span class="cvss-badge {{ skey }}" title="CVSS {{ b.cvss }}">{{ b.severity }}{% if b.cvss %} ({{ b.cvss }}){% endif %}</span>
            {% endif %}
          </span>
        {% endif %}
      </td>
      <td>{{ b.type }}</td>
      <td>
        {% if b.method and b.method != "" and b.method != "---" %}
          {% assign mkey = b.method | downcase %}
          {% if mkey == "memhint" %}
            <span class="bug-badge"><a href="https://github.com/jiekeshi/MemHint">{{ b.method }}</a></span>
          {% elsif mkey == "securevibebench" %}
            <span class="bug-badge"><a href="https://github.com/iCSawyer/SecureVibeBench">{{ b.method }}</a></span>
          {% else %}
            <span class="bug-badge">{{ b.method }}</span>
          {% endif %}
        {% else %}
          <span style="color: var(--global-text-color-light);">&mdash;&mdash;&mdash;</span>
        {% endif %}
      </td>
    </tr>
    {% endfor %}
  </tbody>
</table>

---
title: "Research"
layout: single
permalink: /research/
---

<div class="rt">
  {% assign years = site.data.research | group_by: "year" | sort: "name" | reverse %}
  {% for yg in years %}
    {% assign projects = yg.items | sort: "order" %}
    <section class="rt__year">
      <span class="rt__year-label">{{ yg.name }}</span>
      <span class="rt__node" aria-hidden="true"></span>

      <div class="rt__projects">
        {% for p in projects %}
          {% assign pid = p.title | slugify | append: "-" | append: yg.name %}
          <article class="rt__project">
            <span class="rt__tick" aria-hidden="true"></span>

            <button class="rt__row" type="button" aria-expanded="false" aria-controls="{{ pid }}-detail">
              {% if p.visual %}
                <img class="rt__thumb" src="{{ p.visual | relative_url }}" alt="{{ p.title }}" loading="lazy">
              {% endif %}
              <span class="rt__meta">
                <span class="rt__title">{{ p.title }}</span>
                {% if p.skills %}
                  <span class="rt__tags">{{ p.skills | join: " · " }}</span>
                {% endif %}
              </span>
              <span class="rt__toggle-icon" aria-hidden="true">+</span>
            </button>

            <div class="rt__detail" id="{{ pid }}-detail" role="region" aria-label="{{ p.title }} details">
              {% if p.visual %}
                <img class="rt__detail-img" src="{{ p.visual | relative_url }}" alt="{{ p.title }}" loading="lazy">
              {% endif %}
              {% if p.summary %}
                <p class="rt__summary">{{ p.summary }}</p>
              {% endif %}
              {% if p.methods or p.papers or p.code_repos %}
                <div class="rt__resources">
                  {% if p.methods %}
                    <div class="rt__resgroup">
                      <span class="rt__reslabel">Methods</span>
                      <ul class="rt__reslist rt__reslist--plain">
                        {% for m in p.methods %}
                          <li>{{ m }}</li>
                        {% endfor %}
                      </ul>
                    </div>
                  {% endif %}

                  {% if p.papers %}
                    <div class="rt__resgroup">
                      <span class="rt__reslabel">Papers</span>
                      <ul class="rt__reslist">
                        {% for paper in p.papers %}
                          {% assign href = paper.url %}
                          {% if paper.url %}{% unless paper.url contains "://" %}{% assign href = "https://" | append: paper.url %}{% endunless %}{% endif %}
                          <li>
                            {% if paper.url %}
                              <a class="rt__link" href="{{ href }}" target="_blank" rel="noopener noreferrer"{% if paper.note %} title="{{ paper.note | escape }}"{% endif %}><i class="fas fa-file-lines" aria-hidden="true"></i>{{ paper.label }}</a>
                            {% else %}
                              <span class="rt__link rt__link--pending"{% if paper.note %} title="{{ paper.note | escape }}"{% endif %}><i class="fas fa-file-lines" aria-hidden="true"></i>{{ paper.label }}</span>
                            {% endif %}
                          </li>
                        {% endfor %}
                      </ul>
                    </div>
                  {% endif %}

                  {% if p.code_repos %}
                    <div class="rt__resgroup">
                      <span class="rt__reslabel">Code</span>
                      <ul class="rt__reslist">
                        {% for repo in p.code_repos %}
                          {% assign href = repo.url %}
                          {% if repo.url %}{% unless repo.url contains "://" %}{% assign href = "https://" | append: repo.url %}{% endunless %}{% endif %}
                          <li>
                            {% if repo.url %}
                              <a class="rt__link" href="{{ href }}" target="_blank" rel="noopener noreferrer"><i class="fab fa-github" aria-hidden="true"></i>{{ repo.label }}</a>
                            {% else %}
                              <span class="rt__link rt__link--pending"><i class="fab fa-github" aria-hidden="true"></i>{{ repo.label }}</span>
                            {% endif %}
                          </li>
                        {% endfor %}
                      </ul>
                    </div>
                  {% endif %}
                </div>
              {% endif %}
            </div>
          </article>
        {% endfor %}
      </div>
    </section>
  {% endfor %}
</div>

<script>
document.addEventListener('DOMContentLoaded', function () {
  var rows = Array.prototype.slice.call(document.querySelectorAll('.rt__row'));

  function close(project) {
    project.classList.remove('is-open');
    var row = project.querySelector('.rt__row');
    var icon = project.querySelector('.rt__toggle-icon');
    if (row) row.setAttribute('aria-expanded', 'false');
    if (icon) icon.textContent = '+';
  }

  function open(project) {
    project.classList.add('is-open');
    var row = project.querySelector('.rt__row');
    var icon = project.querySelector('.rt__toggle-icon');
    if (row) row.setAttribute('aria-expanded', 'true');
    if (icon) icon.textContent = '−';
  }

  rows.forEach(function (row) {
    row.addEventListener('click', function () {
      var project = row.closest('.rt__project');
      if (!project) return;
      var wasOpen = project.classList.contains('is-open');

      document.querySelectorAll('.rt__project.is-open').forEach(function (p) {
        if (p !== project) close(p);
      });

      if (wasOpen) {
        close(project);
      } else {
        open(project);
      }
    });
  });
});
</script>

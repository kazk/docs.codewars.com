---
title: Languages
permalink: /languages/
layout: default
---

<h1 class="f3 lh-title">Languages</h1>

<table class="center w-80 collapse">
  <thead>
    <tr class="lh-title tl">
      <th class="pl2">Language</th>
      <th class="pl2">Version</th>
      <th class="pl2">Test Framework</th>
    </tr>
  </thead>

  <tbody>
  {% assign langs = site.languages | where_exp: 'language', 'language != nil' | sort 'language' %}
  {% for env in langs %}
    {% assign n = env.versions.size %}
    {% capture darken %}{% cycle '', ' darken-bg' %}{% endcapture %}
    {% if n == 1 %}
      <tr class="lh-copy">
        <td class="pl2{{ darken }}">{{ env.title }}</td>
        <td class="pl2{{ darken }}">{{ env.versions | first }}</td>
        <td class="pl2{{ darken }}">{{ env.tests | join: '<br>' }}</td>
      </tr>
    {% else %}
      {% for v in env.versions %}
      <tr class="lh-copy">
        {% if forloop.first %}<td class="pl2{{ darken }}" rowspan="{{ n }}">{{ env.title }}</td>{% endif %}
        <td class="pl2{{ darken }}">{{ v }}</td>
        {% if forloop.first %}<td class="pl2{{ darken }}" rowspan="{{ n }}">{{ env.tests | join: '<br>' }}</td>{% endif %}
      </tr>
      {% endfor %}
    {% endif %}
  {% endfor %}
  </tbody>
</table>



<footer class="pv4 ph2">
  {% assign langs = site.languages | where_exp: 'lang', 'lang.language != nil' | sort 'language' %}
  {% for x in langs %}
    <a class="no-underline near-white bg-animate bg-near-black hover-bg-gray inline-flex items-center ma2 tc br2 pa2"
      href="{{ x.url | remove: '/index' | relative_url }}"
      title="{{ x.title }}">
    <i class="pl1 icon-lang-{{ x.language }}"></i>
    <span class="f6 ml3 pr2">{{ x.title }}</span>{% if x.is_beta %}<sup class="dark-gray">Beta</sup>{% endif %}
    </a>
  {% endfor %}
</footer>


{% comment %}
<div class="flex flex-wrap ph2-l">
  {% assign envs = site.languages | sort 'language' %}
  {% for env in envs %}
  <div class="flex w-100 w-50-m w-25-l ph4">
    <h2 class="f6 self-center"><i class="pl1 icon-lang-{{ env.language }}"></i><span class="ml3">{{ env.title }}</span></h2>
    <div>
    <dl>
    <dt>Versions:</dt>
    <dd>{{ env.versions | join: '<br>' }}</dd>
    <dt>Test Frameworks:</dt>
    <dd>{{ env.tests | join: '<br>' }}</dd>
    </dl>
    </div>
  </div>
  {% endfor %}
</div>
{% endcomment %}


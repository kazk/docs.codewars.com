---
title: Honor
category: platform
---

## Honor {#honor}

Honor represents the level of respect a user has earned from the community, based on their skill and contributions.

Honor is earned fastest through creating kata, crafting great solutions, and constructive comments.

<figure>
<figcaption>
This table shows all of the honor you can earn.
</figcaption>

<table class="f6 w-100 mw6 center" cellspacing="0">
<thead>
<tr><th class="pa3 tl">Reason</th><th class="pa3 tl">Honor</th></tr>
</thead>
<tbody class="lh-copy">
{% for row in site.data.honor_points %}
<tr class="stripe-dark"><td class="pa3">{{ row.name }}</td><td class="pa3">{{ row.points }}</td></tr>
{% endfor %}
</tbody>
</table>
</figure>

### Privileges

As you increase your honor, you will be rewarded with additional site privileges.

<figure>
<figcaption>
This table shows all of the privileges you can earn.
</figcaption>

<table class="f6 w-100 mw6 center" cellspacing="0">
<thead>
<tr><th class="pa3 tl">Privilege</th><th class="pa3 tl">Required Honor</th></tr>
</thead>
<tbody class="lh-copy">
{% for row in site.data.privileges %}
<tr class="stripe-dark"><td class="pa3">{{ row.name }}</td><td class="pa3">{{ row.points }}</td></tr>
{% endfor %}
</tbody>
</table>
</figure>


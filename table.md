---
title: Table test
---

Table


{% assign row = site.data.schedule[0] %}
{{ row | inspect }}

==================================================

<table>
 <tr>
      {% for item in row limit:7 offset:0  %}
        <th>{{ item[0] }}</th>
      {% endfor %}
    </tr>
   <tr>
      {% for item in row limit:7 offset:0  %}
        <th>{{ item[1] }}</th>
      {% endfor %}
    </tr>
</table>
==================================================



<table>
     <tr>
      {% for item in row limit:7 offset:0  %}
        <th>{{ item[0] }}</th>
      {% endfor %}
    </tr>

  {% for table in site.data.schedule %}
   
    {% tablerow row in table limit:7 offset:0 %}
      {{ row[1] }}
    {% endtablerow %}
  {% endfor %}
</table>


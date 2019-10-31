# Home Page

{% include plotly/header.md %}

{% assign setups = (site.setups | sort: "index") %}
{% for setup in setups %}

## {{setup.label}}

{% assign runs = site.runs | where: "setup", setup.uid %}
{% assign runs = runs | sort: "date" %}
{% assign runs_reversed = runs | reverse %}
{% assign runs_count = runs | size %}
{% assign subset_max = 5 %}
{% if runs_count <= subset_max %}
{% assign runs_subset_count = runs_count %}
{% else %}
{% assign runs_subset_count = subset_max %}
{% endif %}

{% if runs_count != 0 %}

Last {{ runs_subset_count }} runs for this setup ([see graphs and stats for all {{ runs_count }} runs so far]({{setup.url}})):

|  | Round-trip PDR (%) | RTT (s) | Duty cycle (%) |
| --- | ---: | ---: | ---:  |
{% for run in runs_reversed -%}
{% assign min_index = runs_count | minus: runs_subset_count -%}
{% if forloop.rindex > min_index -%}
{% assign date = run.date | date: "%m/%d/%Y %H:%M:%S" -%}
[{{date}}]({{ run.url }}) | {{run.global-stats.pdr}} | {{run.global-stats.latency}} | {{run.global-stats.duty-cycle}} |
{% endif -%}
{% endfor %}

{% else %}

No run for this setup ([{{setup.uid}}]({{setup.url}})).

{% endif %}

{% endfor %}

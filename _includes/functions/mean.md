[//]: # Computes mean on an array.
[//]: # Input: variable data, the array
[//]: # Return: variable return

{% assign sum__ = 0. %}
{% assign count__ = 0. %}
{% for val in {{data}} %}
{% if forloop.rindex <= mean_head_count %}
{% assign sum__ = sum__ | plus: val %}
{% assign count__ = count__ | plus: 1 %}
{% endif %}
{% endfor %}
{% assign return = sum__ | divided_by: count__ %}

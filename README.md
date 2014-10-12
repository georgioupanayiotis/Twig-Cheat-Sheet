Twig-Cheat-Sheet
================

This sheet is perfect for both developers and designers. It'll list all the structure controls and tests you can do with twig's engine. Assets, templates, filters, operators won't be a hard thing to remember with that sheet.

### Table of Contents

* [Operators](#operators)
* [Variables](#variables)
* [Filters](#filters)
* [Comment](#comment)
* [Whitespace Control](#whitespace-control)
* [Macro](#macro)
* [Escaping](#escaping)
* [Control Structures](#control-structures)
* [Templates and Blocks](#templates-and-blocks)

<h3>Operators</h3>
<pre><code>[not] in Containment operator
is [not] Test operator
.. Creates a sequence
| Applies a filter
~ Concatenation
. or [] Gets an attribute of an object
?: Ternary operator
{{ }} Used to print the result of an expression evalution
{% %} Used to execute statements</code></pre>

<h3>Variables</h3>
<h4>Print</h4>
<pre><code>{{ a_variable }}
{{ foo.bar }}
{{ foo['bar'] }}</code></pre>

<h4>Set</h4>
```
{% set value = 'foobar' %}
{% set foo = 'foo' %}
{% set foo = [ 1, 2] %}
{% set foo = {'foo': 'bar'} %}
{% set foo = 'foo' ~ 'bar' %}
{% set foo, bar = 'foo', 'bar' %}
```

```
{% set value %}
<div id="foobar">
...
</div>
{% endset %}
```

<h4>Filters</h4>
```
{{ foo|striptags }}
{% filter upper %}This text becomes uppercase{% endfilter %}
```

<h4>Comment</h4>
```
{# single line comment #}
```

<h4>Whitespace Control</h4>
```
{% spaceless %}
  <div>
    <strong>title</strong>
  </div>
{% endspaceless %}
{# Output will be <div><strong>title</strong></div> #}
{% set value = 'Lorem Ipsum' %}
{{- value -}}
<h1> {{- value }} </h1>
{# Will output <h1>Lorem Ipsum </h1> #}
```

<h4>Macro</h4>
```
{% macro link(url,label) %}
  <a href="{{ url }}"> {{ label }}</a>
{% endmacro %}
{{ _self.link('index.html','Home') }}
{% import "forms.html" as forms %}
{% from 'forms.html' import input as input_field %}
{{ form.input('foobar') }}
{{ input_field('foobar') }}
```

<h4>Escaping</h4>
```
{{ '{{' }}
```
```
{% raw %}
  {% set value = 'Lorem Ipsum' %}
  <h1>{{ value }}</h1>
{% endraw %}
```

<h4>Control Structures</h4>
FOR
```
<ul>
  {% for item in collection %} <li>{{ item }}</li> {% endfor %}
</ul>
```
```
{% for letter in 'a'..'z' %}
  {{ letter }}
{% endfor %}
```
```
{% for i in 0..9 %}
  {{ i }}
{% endfor %}
```
```
{% for item in collection %}
  {{ item }}
{% else %}
  No item.
{% endfor %}
```
```
{% for i in range(0,10,2) %}
  {{ i }}
{% endfor %}
{% for item in collection %}
  {{ loop.index }}
{% endfor %}
```
```
{% for key in items|keys %}
  {{ key }}
{% endfor %}
```
```
{% for key, item in items %}
  {{ key }} : {{ item }}
{% endfor %}
```

```
loop.index        The current iteration of the loop (1 indexed)
loop.index0       The current iteration of the loop (0 indexed)
loop.revindex     The number of iterations from the end of the loop (1 indexed)
loop.revindex0    The number of iterations from the end of the loop (0 indexed)
loop.first        True if first iteration
loop.last         True if last iteration
loop.length       The number of items in the sequence
loop.parent       The parent context
```
IF
```
{% if foo %}
...
{% elseif bar %}
...
{% else %}
...
{% endif %}
```
```
{% if items %}
  <ul>
    {% for item in items %}
      <li>{{ item }}</li>
    {% endfor %}
  </ul>
{% endif %}
```

<h4>Templates and Blocks</h4>

<h5>Define a block (redefine is existing)</h5>
```
{% block sidebar %} ... {% endblock %}
```
<h5>Parent block</h5>
```
{% block sidebar %} {{ parent() }} {% endblock %}
```
<h5>Extends a template</h5>
```
{% extends "base.html.twig" %}
```
<h5>Include a template</h5>
```
{% include "header.html.twig" %}
```
<h5>Include with access options</h5>
```
{% include "header.html.twig" with { 'foo' : 'bar' } only %}
```
<h5>Import blocks from a template</h5>
```
{% use "blocks.html.twig" %}
```
<h5>Import blocks with alias</h5>
```
{% use "blocks.html.twig" with sidebar as base_sidebar %}
```
<h5>Call a block</h5>
```
{{ block('base_sidebar') }}
```


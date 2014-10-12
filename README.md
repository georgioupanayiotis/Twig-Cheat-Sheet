Twig-Cheat-Sheet
================

![alt tag](http://inchoo.net/wp-content/uploads/2011/06/twig1.jpg)

This sheet is perfect for both developers and designers. It'll list all the structure controls and tests you can do with twig's engine. Assets, templates, filters, operators won't be a hard thing to remember with that sheet.

## Table of Contents

* [Operators](#operators)
* [Variables](#variables)
* [Filters](#filters)
* [Comment](#comment)
* [Whitespace Control](#whitespace-control)
* [Macro](#macro)
* [Escaping](#escaping)
* [Control Structures](#control-structures)
* [Templates and Blocks](#templates-and-blocks)

## Operators
```
[not] in Containment operator
is [not] Test operator
.. Creates a sequence
| Applies a filter
~ Concatenation
. or [] Gets an attribute of an object
?: Ternary operator
{{ }} Used to print the result of an expression evalution
{% %} Used to execute statements
```

## Variables
**Print**
<pre><code>{{ a_variable }}
{{ foo.bar }}
{{ foo['bar'] }}</code></pre>

**Set**
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

## Filters
```
{{ foo|striptags }}
{% filter upper %}This text becomes uppercase{% endfilter %}
```

## Comment
```
{# single line comment #}
```

## Whitespace Control
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

## Macro
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

## Escaping
```
{{ '{{' }}
```
```
{% raw %}
  {% set value = 'Lorem Ipsum' %}
  <h1>{{ value }}</h1>
{% endraw %}
```

## Control Structures
**FOR**
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
**IF**
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

## Templates and Blocks

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

##Built-in Filters
**date**
```
{{ post.created_at|date("d/m/Y") }}
{{ "now"|date("d/m/Y") }}
```
**format**
```
format {{ "I like %s and %s"|format(foo, 'bar') }}
```
**replace**
```
{{ "Hello %name% !"|replace({'%name%': 'world'}) }}
```
**url_encode**  URL encodes a given string.
**json_encode** Return the JSON representation of a given string.
**title**       Return a titlecased version of the value.
**capitalize**  Return a capitalized version of the value.
**upper**       Convert a value to uppercase
**lower**       Convert a value to lowercase
**striptags**   Strips SGML/XML tags and replace adjacent whitespaces by one space




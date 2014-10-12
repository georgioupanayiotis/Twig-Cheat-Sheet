#Twig-Cheat-Sheet


![alt tag](http://sensiolabs.com/images/illustration/inner_pages/products/twig.jpg)This sheet is perfect for both developers and designers. It'll list all the structure controls and tests you can do with twig's engine. Assets, templates, filters, operators won't be a hard thing to remember with that sheet.

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
* [Built-in Filters](#built-in-filters)
* [Global Functions](#global-functions)
* [Automatic Escaping](#automatic-escaping)
* [Symfony2](#symfony2)


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
[Back to top](#twig-cheat-sheet)

## Comment
```
{# single line comment #}
```
[Back to top](#twig-cheat-sheet)

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
[Back to top](#twig-cheat-sheet)

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
[Back to top](#twig-cheat-sheet)

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
[Back to top](#twig-cheat-sheet)

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
[Back to top](#twig-cheat-sheet)

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
[Back to top](#twig-cheat-sheet)

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
```
url_encode  URL encodes a given string.
```
```
json_encode Return the JSON representation of a given string.
```
```
title       Return a titlecased version of the value.
```
```
capitalize  Return a capitalized version of the value.
```
```
upper       Convert a value to uppercase
```
```
lower       Convert a value to lowercase
```
```
striptags   Strips SGML/XML tags and replace adjacent whitespaces by one space
```
**join**
```
{{ [a, b, c]|join(', ') }} {# return "a,b,c" #}
{{ [a, b, c]|join }} {# return abc #}
```
```
reverse     Reverses an array or an object implementing the iterator interface
```
```
length      Return the number of items of a sequence or array, or the length of a string
```
```
sort        Sort an array
```
**default**
```
{{ var|default('var is not defined') }}
```
**keys**
```
{% for key in array|keys %} ... {% endfor %}
```
```
escape, e   Convert a string to HTML-safe sequences.
```
```
raw         Value will not be escaped
```
```
merge       Merge an array with the value.
```
[Back to top](#twig-cheat-sheet)

##Global Functions
**range**
```
{% for i in range(0, 3) %} {{ i }} {% endfor %}
{# returns 0, 1, 2, 3 #}

{% for i in range (0, 6, 2) %} {{ i }} {% endfor %}
```
**cycle**
```
{% for i in 0..10 %}
  {{ cycle(['odd', 'even'], i) }}
{% endfor %}
```
**constant**
```
Returns the constant value for a given string.
  {{ some_date|date(constant('DATE_W3C')) }}
```
[Back to top](#twig-cheat-sheet)

##Automatic Escaping
```
{% autoescape %}
  Everything will be automatically escaped in this block
  using the HTML strategy
{% endautoescape %}
{% autoescape 'html' %}
  Everything will be automatically escaped in this block
  using the HTML strategy
{% endautoescape %}
{% autoescape 'js' %}
  Everything will be automatically escaped in this block
  using the js escaping strategy
{% endautoescape %}
{% autoescape false %}
  Everything will be outputted as is in this block
{% endautoescape %}
```
[Back to top](#twig-cheat-sheet)

##Symfony2
**Generate URL**
```
{{ path('route_name', {'param': 'value'}) }}
```
**Generate absolute URL**
```
{{ url('route_name') }}
```
**Link to Assets**
```
<link rel="stylesheet" href="{{ asset('css/style.css') }}" type="text/css" />
<img src="{{ asset('images/logo.png') }}" alt="Logo" />
```
**Registering extension**
```
<services>
  <service id="acme.twig.acme_extension" class="Project_Twig_Extension">
    <tag name="twig.extension" />
  </service>
</services>
```
[Back to top](#twig-cheat-sheet)

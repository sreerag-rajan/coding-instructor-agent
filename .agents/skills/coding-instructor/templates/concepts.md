# Lesson {{ number }}: {{ title }}

## Overview

{{ overview }}

---

## Core Concepts

{% for concept in concepts %}
### {{ concept.name }}

{{ concept.explanation }}

{% if concept.analogy %}
**Analogy**: {{ concept.analogy }}
{% endif %}

{% if concept.key_points %}
**Key Points**:
{% for point in concept.key_points %}
- {{ point }}
{% endfor %}
{% endif %}

{% endfor %}

---

## Why This Matters

{{ why_matters }}

---

## Further Resources

{% for resource in resources %}
- [{{ resource.title }}]({{ resource.url }}) — {{ resource.description }}
{% endfor %}

---

## Before You Start

Make sure you understand the concepts above. If anything is unclear, chat with your instructor (the agent) by asking clarifying questions. You can use `/hint` if you need a nudge on the task. Remember: the instructor **will not write code for you**. Every line must be yours.

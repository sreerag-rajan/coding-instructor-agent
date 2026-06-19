# Task {{ number }}: {{ title }}

## Objective

{{ objective }}

---

## Requirements

{% for requirement in requirements %}
{{ loop.index }}. {{ requirement }}
{% endfor %}

---

## Acceptance Criteria

{% for criterion in acceptance_criteria %}
- [ ] {{ criterion }}
{% endfor %}

---

## Instructions

Write your solution in `lessons/lesson-{{ '%02d' % number }}-{{ slug }}/solution.{{ extension }}`.

1. Read the `concepts.md` file for this lesson first
2. Plan your approach — think about what the task is asking
3. Write your code in the solution file
4. Run any tests if provided, or check against the acceptance criteria manually
5. Submit for review with `/review @lessons/lesson-{{ '%02d' % number }}-{{ slug }}/solution.{{ extension }}`

---

## Hints (Use Sparingly)

The instructor will not provide hints unless you ask with `/hint`.

---

## Notes

- Focus on **understanding**, not just making it work
- The reviewer will check: correctness, readability, idiomatic patterns, conceptual alignment, and error handling
- If you're stuck, ask the instructor conceptual questions — they can clarify the "what" and "why"

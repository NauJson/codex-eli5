---
name: eli5
description: Explain a topic like I'm a 5 year old as a single HTML page with big pictures and very few words. Use when the user types $eli5 <topic>, /eli5 <topic>, says ELI5, 像给五岁小孩解释, 用图解释, or asks for a dead-simple picture explainer of how something works.
---

# eli5

Explain like I'm someone who knows nothing about this topic, using a self-contained HTML file with big pictures (inline SVG) and few words. Do not use an image model. The HTML page is the explanation.

Topic: the subject in the user's message. If they did not give one, ask once.

Write the HTML to `eli5-<short-slug>.html` in the current workspace and report the path. Do not replace the page with a long chat explanation.

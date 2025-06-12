---
layout: default
title: "🧠 Build Log"
has_children: true
image: /assets/images/volt_X.png
nav_order: 1
permalink: /blog/
---

# 🧠 Build Log

This section documents the ongoing development of the VOLT engine — a modular crypto trading system focused on clarity, allocation, and beating buy-and-hold with fewer, smarter trades.

VOLT started as a single-symbol backtest script. It has evolved into a **full research engine and allocation model** — now operating under the PRISM framework.

The log will track major architecture improvements, system philosophy, and practical lessons as PRISM continues to mature.

---

### Recent Highlights

<ul>
{% assign children = site.pages | where: "parent", "🧠 Build Log" | sort: "nav_order" %}
{% for child in children %}
  <li><a href="{{ child.url | relative_url }}">{{ child.title }}</a></li>
{% endfor %}
</ul>

---

More build notes coming soon as PRISM’s live features, sweep engine, and strategy framework continue to evolve.

Stay sharp.

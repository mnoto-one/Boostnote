---
title: 2 - How to get current  language
tags:
  - Current
  - Language
  - Translation
  - Django
---

### 📜 List files
```python
1 -> "example/templates/index.html"
```
---

### 💬 html index
📁 -1 example/templates/index.html

```html
{% get_current_language as LANGUAGE_CODE %}
{{ LANGUAGE_CODE }}
```

▶️ Result in Terminal

```shell
en
```

---
title: "Categories"
date: 2025-10-25
draft: false
---

# Categories

{{< ul >}}
{{ range $name, $taxonomy := .Site.Taxonomies.categories }}
- [{{ $name }}](/categories/{{ $name | urlize }})
{{ end }}
{{< /ul >}}

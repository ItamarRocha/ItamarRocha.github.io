# ItamarRocha.github.io

* Repository with the code used to generate my [personal website](https://itamarrocha.github.io)
* Still under construction just like myself

## Blogging (internal and external posts)

This site uses Jekyll. You can publish:

- Internal posts: add a Markdown file under `_posts/` named `YYYY-MM-DD-title.md` with front matter:

```yaml
---
layout: post
title: My Post Title
---
```

- External posts (e.g., Medium, Substack): create a file under `_posts/` as usual, but include `external_url` in the front matter. Optionally set `source` and `excerpt`:

```yaml
---
layout: post
title: Title of the external post
date: 2025-01-15
external_url: https://example.com/my-post
source: Medium # or Substack/LinkedIn/etc
excerpt: Short summary that will appear on the blog page
---

Optional extra context can go here (it will appear on the local page under the external link CTA).
```

The blog index automatically renders a “Read on Medium/… ↗” button for entries with `external_url`.


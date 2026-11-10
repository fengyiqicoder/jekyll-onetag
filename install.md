---
layout: page
title: Install
description: Three steps. Copy two includes, add one line to your layout, copy the two llms templates.
permalink: /install/
---

You copy four small files from [this repository](https://github.com/fengyiqicoder/jekyll-onetag) into your site. Nothing to install.

## 1. Copy the includes

Copy these two files into the `_includes/` folder of your site:

- [`_includes/onetag.html`](https://github.com/fengyiqicoder/jekyll-onetag/blob/main/_includes/onetag.html): the Ask AI script tag.
- [`_includes/onetag-pages.html`](https://github.com/fengyiqicoder/jekyll-onetag/blob/main/_includes/onetag-pages.html): the list of pages the llms files use.

## 2. Add the box to your layout

Open the layout your pages use, usually `_layouts/default.html`, and add one line right before `</body>`:

{% raw %}
```liquid
    {% include onetag.html %}
  </body>
```
{% endraw %}

Your theme comes from a gem, like `minima`, and you have no `_layouts/default.html`? Copy the theme's `default.html` into `_layouts/` first. For minima 2.5 it is [this file](https://github.com/jekyll/minima/blob/v2.5.1/_layouts/default.html). Your copy then wins over the theme's.

## 3. Copy the llms templates

Copy these two files to the root of your site, next to `_config.yml`:

- [`llms.txt`](https://github.com/fengyiqicoder/jekyll-onetag/blob/main/llms.txt): becomes `/llms.txt`.
- [`zz-llms-full.txt`](https://github.com/fengyiqicoder/jekyll-onetag/blob/main/zz-llms-full.txt): becomes `/llms-full.txt`.

Keep the `zz-` in the second name. Jekyll renders pages in file name order, and this file must come last so that the other pages are already turned into HTML when it reads them. [How it works]({{ "/how-it-works/" | relative_url }}) has the details.

## Get a key

Add a key before you deploy. Without one the box uses a demo key that answers on localhost only. Get a free key with one request; it arrives in the inbox of the email you send:

```sh
curl -X POST https://onetagai.com/api/signup -H "Content-Type: application/json" -d '{"email":"you@example.com"}'
```

Put it in `_config.yml`:

```yaml
onetag:
  key: ot_...
```

The key is public by design: it ends up in the built HTML, like an analytics ID. The free plan has 1,000,000 tokens a month, with a hard cap, so no bill can appear.

## Check that it works

```sh
bundle exec jekyll serve
```

- Open `http://localhost:4000/llms.txt` and `/llms-full.txt`. Every page should be there.
- An **Ask AI** button floats in the bottom right corner. Ask something your pages answer. You should see an answer and, under it, **Sources** with links to your pages.

If you see an error instead, the browser console has a line starting with `[OneTag AI Ask Docs]` and the error code.

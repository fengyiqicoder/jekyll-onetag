---
layout: page
title: Ask AI for Jekyll
description: An Ask AI box, llms.txt and llms-full.txt for Jekyll sites, on stock GitHub Pages.
permalink: /
---

An Ask AI box for Jekyll sites, and the `llms.txt` and `llms-full.txt` files it reads. Readers ask a question in their own words and get an answer written from your pages, with links to the pages it used.

This site runs it. Press **Ask AI** in the bottom right corner, or `Ctrl+/`, and try:

- How do I add this to my Jekyll site?
- Does it work on GitHub Pages without a plugin?
- 可以改按钮的位置吗？

## What it is

Four small files you copy into your site. It is not a gem and not a plugin, because GitHub Pages does not run custom plugins. Everything is plain Liquid, so it builds on stock GitHub Pages.

- **`llms.txt`**: an index of your site in the [llmstxt.org](https://llmstxt.org) shape. Title, description, one link per page.
- **`llms-full.txt`**: the text of every page in one file, each page under its own heading with a `Source:` link. AI tools can read your whole site from it.
- **The Ask AI box**: one script tag, added by `_includes/onetag.html`. It reads `llms-full.txt` in the reader's browser and answers from it.

The two llms files need no key and no account. They are useful on their own.

## Add it to your site

1. Copy `_includes/onetag.html` and `_includes/onetag-pages.html` into your `_includes/` folder.
2. Add {% raw %}`{% include onetag.html %}`{% endraw %} right before `</body>` in your layout.
3. Copy `llms.txt` and `zz-llms-full.txt` to the root of your site.

The full steps are on [Install]({{ "/install/" | relative_url }}).

## What you do not need

- **No plugin and no gem.** It works on stock GitHub Pages, with "Deploy from a branch".
- **No server and no crawler.** The files are rebuilt with your site, so they are never out of date.
- **No AI provider account.** The key is a OneTag AI key, made to sit in a public page. Free: 1,000,000 tokens a month.

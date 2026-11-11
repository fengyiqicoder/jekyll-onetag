---
layout: page
title: FAQ
description: Keys, GitHub Pages, themes, subfolder sites and languages.
permalink: /faq/
---

## Why is this not a gem?

GitHub Pages builds sites with a fixed list of plugins and does not run any other. A gem would only work for sites built with GitHub Actions or on another host. Liquid files work everywhere Jekyll runs.

## Is it safe to put the key in a public page?

Yes. A OneTag AI key can only ask the AI questions, and it has a hard cap. It cannot read anything, and it is not the key of an AI provider account with a bill behind it. If someone copies it, they share your month's allowance.

## What happens without a key?

You still get `llms.txt` and `llms-full.txt`. The box uses a demo key that answers on `localhost` only, so you can try it with `jekyll serve`. On a deployed site it tells the reader that Ask AI is not set up yet. The built HTML has a comment with the signup command.

## Does it work with my theme?

Yes, with any theme where you can add one line before `</body>`. With a gem theme, copy its `default.html` into `_layouts/` and add the line there. The button floats in the bottom right corner and takes the page's accent color.

## Does it work when the site is in a subfolder, like username.github.io/project/?

Yes. The links in both files use `absolute_url`, which adds `url` and `baseurl` from `_config.yml`. The box looks for `llms-full.txt` from the current page up to the site root. This site is such a site.

## Can I keep my own llms.txt?

Yes. Do not copy the templates, or copy only `zz-llms-full.txt`. The box needs only `llms-full.txt`.

## My pages are not in English. Does it work?

Yes. The answer is in the language of the question. The box's own text is in English, Simplified Chinese or Traditional Chinese, following the page's `lang`; set `lang` in the `onetag` block to choose.

## Can I see what readers ask?

No. OneTag AI does not store questions or answers. It only counts the tokens your key uses.

## Where is the source?

This site is its own source: [fengyiqicoder/jekyll-onetag](https://github.com/fengyiqicoder/jekyll-onetag). The script is one file, MIT licensed: [ask-docs.js](https://github.com/fengyiqicoder/onetagai/blob/main/sdk/ask-docs.js).

---
layout: page
title: How it works
description: What the files do at build time, and what the box does in the reader's browser.
permalink: /how-it-works/
---

## At build time

`llms.txt` and `zz-llms-full.txt` are Liquid templates with `layout: null`. Jekyll builds them like any other page, into `/llms.txt` and `/llms-full.txt`. They list `site.pages`, `site.posts` and the documents of every collection that has `output: true`.

`llms-full.txt` has one block per page:

```text
# Install

Source: https://example.com/install/

The page text. Its own headings are moved down to ### and below.
```

The page text is the HTML Jekyll made from your Markdown, turned back into plain text: paragraphs, lists, tables and fenced code blocks are kept, tags are removed. Headings inside a page start at `###`, so a `# ` or `## ` line always starts a new page. That is how the box tells pages apart, and it keeps every passage linked to the right page.

### Why the file name starts with zz-

Jekyll renders pages one after the other, in file name order. When `zz-llms-full.txt` reads another page, that page is only turned into HTML if it came first. With `zz-` in front, the template comes after your pages, so it reads finished HTML, with includes and Liquid already run. Posts and collection documents are rendered before all pages, so they are always ready.

Pages that plugins add during the build, like the feed or pagination pages, come after it either way. Those are left out.

## In the reader's browser

`_includes/onetag.html` adds one script tag:

```html
<script async src="https://onetagai.com/ask-docs.js" data-key="ot_..." data-ref="jekyll-onetag"></script>
```

The script draws an **Ask AI** button. When a reader asks, it looks for an index, starting from the folder of the current page and going up to the site root: a MkDocs search index, then a Pagefind index, then `llms-full.txt`. On a Jekyll site with these files it finds `llms-full.txt`.

A file under 20,000 characters is sent whole with each question. A longer one is split at its `# ` lines, one entry per page, and the entries that match the question are sent. The answer streams back and is shown as it arrives. Under it are links to the pages it came from.

## The instructions

This is what the AI is told, unless you replace it with the `rules` option:

> You are the help desk for this documentation site. Answer only from the pages provided. When the pages cover the question, answer it directly and stop. Only when they do not, say so in one sentence and name the closest page. Under 150 words, no headings. Put commands, code and configuration in a fenced code block, copied the way the pages write them; never invent syntax the pages do not show, and never put ordinary sentences in a code block. Answer in the language of the question.

## What is sent, and where

With each question the browser sends OneTag AI the question, the passages picked from your already public pages, and the conversation so far. Nothing is sent before a reader asks.

OneTag AI does not store questions, passages or answers. It logs token counts, the time, which key was used and the hostname of the site, to count the monthly allowance. The details are on the [privacy page](https://onetagai.com/privacy?ref=jekyll-onetag).

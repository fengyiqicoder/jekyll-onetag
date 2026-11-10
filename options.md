---
layout: page
title: Options
description: Every setting goes in the onetag block of _config.yml.
permalink: /options/
---

All options go in the `onetag:` block of `_config.yml`. Only `key` is needed.

```yaml
onetag:
  key: ot_...
  label: Ask the docs
  position: left
  exclude:
    - /tags/
```

| Option | What it does | Default |
| --- | --- | --- |
| `key` | Your OneTag AI key. | The demo key, which answers on localhost only |
| `ask_ai` | `false` leaves the box out. The llms files are still written. | `true` |
| `label` | The text on the button and at the top of the box. | `Ask AI` |
| `placeholder` | The text in the empty question field. | `Ask a question about these docs` |
| `position` | Where the button goes: `auto`, `float`, `left` or `none`. | `auto` |
| `button` | A CSS selector for your own element that opens the box. | none |
| `color` | The accent color, as hex: `ff6600`. | Taken from the page |
| `theme` | `light` or `dark`. | Follows the page |
| `lang` | The language of the box's own text: `en`, `zh-CN`, `zh-TW`. | The page's language |
| `rules` | Replaces the instructions the AI gets. | See [How it works]({{ "/how-it-works/" | relative_url }}) |
| `index` | The address of the index, when it is not found on its own, for example `/llms-full.txt`. | Found on its own |
| `exclude` | URL prefixes to leave out of both llms files, for example `/tags/`. | none |

## Leave one page out

Add `llms: false` to the page's front matter. Pages with `sitemap: false` are left out too, as are 404 pages, redirects and pagination pages.

## Only the llms files, or only the box

- Only the llms files: set `ask_ai: false`, or do not add the include to your layout.
- Only the box, because another tool already writes `llms.txt`: do not copy the two templates. The box finds the other tool's `llms-full.txt` on its own.

## Your own button

```yaml
onetag:
  position: none
  button: .ask-ai
```

```html
<a class="ask-ai" href="#">Ask AI</a>
```

## From JavaScript

```js
onetagAskDocs.open();                      // open the box
onetagAskDocs.close();                     // close it
onetagAskDocs.ask("How do I deploy?");     // open it and ask
```

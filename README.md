# Ask AI for Jekyll

An Ask AI box for Jekyll sites, and the `llms.txt` and `llms-full.txt` files it reads. Readers ask a question in their own words and get an answer written from your pages, with links to the pages it used. It is plain Liquid, so it works on stock GitHub Pages: no gem, no plugin, no server.

**Live demo: [fengyiqicoder.github.io/jekyll-onetag](https://fengyiqicoder.github.io/jekyll-onetag/)**. Press **Ask AI** in the bottom right corner.

## What you get

- **`llms.txt`**: an index of your site in the [llmstxt.org](https://llmstxt.org) shape. Title, description, one link per page.
- **`llms-full.txt`**: the text of every page, post and collection document in one file, each under its own `# Title` with a `Source:` link.
- Both files need no key and no account, and are rebuilt with your site.
- **The Ask AI box**: one script tag on every page. It reads `llms-full.txt` in the reader's browser and answers from it, in the language of the question.

## Install

1. Copy [`_includes/onetag.html`](_includes/onetag.html) and [`_includes/onetag-pages.html`](_includes/onetag-pages.html) into your `_includes/` folder.
2. Add `{% include onetag.html %}` right before `</body>` in your layout (usually `_layouts/default.html`). With a gem theme such as minima, copy the theme's `default.html` into `_layouts/` first.
3. Copy [`llms.txt`](llms.txt) and [`zz-llms-full.txt`](zz-llms-full.txt) to the root of your site. Keep the `zz-` in the name: Jekyll renders pages in file name order, and this template has to come after your pages so it reads them as finished HTML. It is written to `/llms-full.txt`.

Then run `bundle exec jekyll serve` and open `/llms.txt`, `/llms-full.txt` and any page.

## Before you deploy: get a free key

Without a key the box uses a demo key that answers on localhost only. Get your own key with one request; it arrives in the inbox of the email you send:

```sh
curl -X POST https://onetagai.com/api/signup -H "Content-Type: application/json" -d '{"email":"you@example.com"}'
```

```yaml
onetag:
  key: ot_...
```

The key is public by design: it ends up in the built HTML, like an analytics ID. The free plan has 1,000,000 tokens, one time, no monthly reset, with a hard cap, so no bill can appear. More at [onetagai.com](https://onetagai.com/?ref=jekyll-onetag).

## Options

All options go in the `onetag:` block of `_config.yml`. Only `key` is needed.

| Option | What it does | Default |
| --- | --- | --- |
| `key` | Your OneTag AI key | The demo key (localhost only) |
| `ask_ai` | `false` leaves the box out; the llms files are still written | `true` |
| `label` | Text on the button and at the top of the box | `Ask AI` |
| `placeholder` | Text in the empty question field | `Ask a question about these docs` |
| `position` | `auto`, `float`, `left` or `none` | `auto` |
| `button` | CSS selector of your own element that opens the box | none |
| `color` | Accent color as hex, for example `ff6600` | Taken from the page |
| `theme` | `light` or `dark` | Follows the page |
| `lang` | Language of the box's own text: `en`, `zh-CN`, `zh-TW` | The page's language |
| `rules` | Replaces the instructions the AI gets | Built in |
| `index` | Address of the index, when it is not found on its own | Found on its own |
| `exclude` | URL prefixes to leave out of both llms files, for example `/tags/` | none |

A page with `llms: false` or `sitemap: false` in its front matter is left out of the llms files. So are 404 pages, redirects, pagination pages and pages with no text. Only the box, because another tool writes `llms.txt`? Do not copy the two templates.

## How it works

- `llms.txt` and `zz-llms-full.txt` are Liquid templates with `layout: null`. They list `site.pages`, `site.posts` and the documents of collections with `output: true`, with links made by `absolute_url` (so `url` and `baseurl` count).
- In `llms-full.txt` each page is `# Title`, a blank line, `Source: <absolute URL>`, a blank line, and the page text. The text is the page's HTML turned back into plain text, with paragraphs, lists, tables and fenced code kept. Headings inside a page are moved down to `###` and below, so the box reads every page as one entry with its own link (long pages are cut into parts, all with the same link).
- `_includes/onetag.html` writes `<script async src="https://onetagai.com/ask-docs.js" data-key="..." data-ref="jekyll-onetag">`. When a reader asks, the script fetches `llms-full.txt`, picks the parts that match, and sends them with the question. Nothing is sent before a reader asks.

## Works without a key

With no key you still get both llms files on every build, on GitHub Pages or anywhere else. The box answers on `localhost`, so you can try it with `jekyll serve`. On a deployed site it says Ask AI is not set up yet, and the built HTML has a comment with the signup command. Nothing fails.

## This repository

It is the demo site itself, built with the same gems as GitHub Pages (`github-pages`, theme `minima`). `_layouts/default.html` is minima's layout with the one include added.

The key of the live demo is not in this repository: `_config.yml` keeps `key: ""`. The maintainer sets it as the repository secret `ONETAG_KEY`, and [`.github/workflows/pages.yml`](.github/workflows/pages.yml) writes it into `_config.demo.yml` at build time (`JEKYLL_ENV=production`, `--config _config.yml,_config.demo.yml`). For that, the Pages setting is **Source: GitHub Actions**. Forks without the secret build fine and use the demo key. On your own site you do not need a workflow: stock **Deploy from a branch** works, with your key written in `_config.yml`.

To run it locally:

```sh
bundle install
bundle exec jekyll serve
```

## License

MIT

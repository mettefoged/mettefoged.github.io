# Academic Website

A static Jekyll site styled as a New York Times–style editorial layout
(Newsreader + Libre Franklin, black-on-white, hairline/scotch rules). Pages:

- **Home** (`/`) — bio, news ("The Latest"), and the profile rail.
- **Research** (`/research/`) — articles, working papers, projects, edit `_data/research.yml`.
- **Projects** (`/projects/`) — research agendas that group related papers, edit `_data/projects.yml`.
- **People** (`/people/`) — students and collaborators, edit `_data/people.yml`.
- **CV** — the nav links straight to `files/CV.pdf` (add your CV there).

You never edit HTML/CSS to add content — just the data files below. The header
nav lives in `_data/navigation.yml` (Home is added automatically).

## Preview locally

```
bundle install                       # first time only
bundle exec jekyll serve --livereload
```

Then open <http://localhost:4000>. Edits to data files and posts reload
automatically; after editing `_sass/` or `_includes/`, hard-refresh the browser.

## Easiest way: the Content Manager

Instead of editing YAML by hand, open **`content-manager.html`** (double-click it;
it lives in the repo root and is excluded from the published site). It's a small
graphical tool for adding news and research entries.

1. Click **Connect _data folder** and pick the `_data` folder (or the repo root).
2. Choose the **News** or **Research** tab and fill in the form. A live YAML
   preview shows exactly what will be written.
3. Click **Add to file** — the entry is inserted into `news.yml` / `research.yml`
   (newest first), keeping everything else in the file intact.
4. Rebuild / refresh the site to see it. Because the repo is in git, you can
   always undo a change.

Direct saving works in **Chrome or Edge**. In other browsers the tool switches to
copy-paste mode: click **Copy snippet** and paste it into the file at the spot it
tells you. The manual schema below still applies if you'd rather edit the files
directly.

## Where to edit

### Homepage news (`_data/news.yml`)

Add a new item to the **top** of the list:

```yml
- date: 2026-03-18
  kicker: "Working Paper · In Press"   # optional small eyebrow above the headline
  title: "Short headline"
  body: "One or two sentences of context."
  link:                                # a single link …
    label: "Read more"
    url: "https://example.com"
  # … or several, using `links:` instead of `link:`
  # links:
  #   - label: "Venue A"
  #     url: "https://example.com/a"
  #   - label: "Venue B"
  #     url: "https://example.com/b"
```

The Home page shows the latest four items under "The Latest".

### Research outputs (`_data/research.yml`)

The file is a list of `sections`; add items under the relevant section's
`items:`. Sections with no items show their `empty_message` as an italic note.

```yml
- title: "Paper title"
  year: 2026
  status: "Working paper"          # shown in the metadata line, in accent colour
  venue: "Series or journal"
  series: "Working Paper No. 1"    # optional; appended after venue with " · "
  authors:
    - key: "mette_foged"           # lookup from _data/coauthors.yml
    - name: "Mette Foged"  # inline name (no lookup) — your own name stays plain
  summary: "Abstract text. HTML like <i>italics</i> is allowed."
  bibtex: |
    @unpublished{key2026,
      author = {Last, First and Last, First},
      title  = {Paper Title},
      year   = {2026},
      url    = {https://example.com}
    }
  links:
    - label: "Working paper"
      url: "https://example.com/paper"
    - label: "RFBerlin version"
      url: "https://example.com/old"
      older: true                  # tucked under an "Older versions +" toggle
```

#### Two entry layouts (controlled by `summary`)

- **Has a `summary`** → full "working paper" layout: index number (`01`, `02`…),
  metadata line, author byline, **Read summary** and **BibTeX** toggles, and the
  version-links row.
- **No `summary`** → compact layout (used for older / RA work): metadata, title,
  byline, and links only. No abstract or BibTeX panel.

So: add a `summary` to give a paper the full treatment; leave it out for a short
entry.

#### Current vs. older version links

List every version under `links:`. The current/canonical versions show as
prominent accent links. Mark any superseded link with `older: true` and it moves
behind an **"Older versions +"** toggle, rendered de-emphasised. You can flag any
number of links this way. To add a published-version link later, just add another
entry to `links:` (leave `older` off so it shows as current).

> Note: the old `primary:` and `type:` fields are no longer used by the templates
> (arrows replaced the icons, and `older:` now controls emphasis). They're
> harmless if left in place, but you don't need them on new entries.

#### Co-authors (`_data/coauthors.yml`)

Frequent co-authors are defined once and reused with `key`. Their name becomes a
clickable link to their homepage; your own name (added inline with `name:`) stays
plain text.

```yml
mette_foged:
  name: "Mette Foged"
  url: "https://example.com"
```

For one-off collaborators, use an inline `name` (with an optional `url`).

### Projects (`_data/projects.yml`)

Each project is a research agenda that gathers a few related papers:

```yml
- title: "Refugee integration"
  description: "A line of work on how reception policy shapes outcomes."
  papers:
    - title: "Paper title"
      year: 2024
      venue: "Journal of Something"
      authors:
        - name: "Mette Foged"
        - key: "coauthor_key"
      links:
        - label: "Paper"
          url: "https://example.com"
```

The papers use the same fields as `research.yml` entries (so co-author links and
`older:` flags work the same way).

### People (`_data/people.yml`)

A grid of photo cards, organised into groups (PhD students, collaborators, …).
Each member is either a reference to someone in `coauthors.yml` (so you don't
retype the name/url) or an inline person:

```yml
- group: "PhD students"
  members:
    # reuse a person from coauthors.yml — pulls name, url, photo, role, affiliation
    - key: "jens_hainmueller"
      role: "PhD student"            # optional: override for this context
    # or define a one-off inline:
    - name: "Student Name"
      photo: "/images/people/student.jpg"   # optional (else shows an initial)
      role: "PhD student"                    # optional — position/title
      affiliation: "University of Copenhagen" # optional
      url: "https://example.com"             # optional — makes the card a link
```

Photos live in `images/people/`. Because `coauthors.yml` is shared with
Research, you can add `photo`, `role`, and `affiliation` to an entry there once
and reference it by `key` on both pages.

### CV

The **CV** nav item links straight to `files/CV.pdf`. Drop your PDF in the
`files/` folder with that exact name (or change the URL in
`_data/navigation.yml`). The link opens in a new tab.

### Notes / blog (disabled)

A Notes/blog section exists in the templates but is turned off
(`_pages/notes.md` has `published: false`, and it's not in the nav). To bring it
back, set `published: true` there and add a `Notes` item to
`_data/navigation.yml`; posts go in `_posts/` as `YYYY-MM-DD-title.md`.

### Your name and preferred citation

Your display name and the "Cite as" callout come from `_config.yml`:

```yml
title: "Mette Foged"        # masthead nameplate + browser title
author:
  name: "Mette Foged"       # bylines, footer, photo caption
  citation_name: "Foged, M."             # shown in the Home rail "Cite as" block
                                          # and as "Preferred citation" on Research
```

Change these in one place and they update everywhere. The BibTeX panels are
separate — edit the `author = {…}` line in each entry's `bibtex:` if you want a
copied citation to read a particular way.

## Tweaking the design

- **Accent colour:** change `--accent` in `_sass/layout/_custom.scss` (default
  editorial blue `#326891`; the design also suggests `#121212` or oxblood
  `#7a2e2e`).
- **Section headings, type, spacing, hairlines:** all live in
  `_sass/layout/_custom.scss` as CSS custom properties and component classes.
- **Masthead / nav / footer:** `_includes/masthead.html` and
  `_includes/footer.html`. The nav (`HOME · RESEARCH · NOTES`) sticks to the top
  when you scroll; the active page is detected from the URL.
- The expand/collapse and copy-to-clipboard behaviour is a few lines of inline
  vanilla JS in `_includes/research-entry.html` — no framework or build step.

Dark mode was removed as part of the editorial redesign; the site is
intentionally black-on-white.

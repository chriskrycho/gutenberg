+++
title = "Sections and Pages"
weight = 20
+++

Pages and sections are actually very similar.

## Page variables
Gutenberg will try to load the `templates/page.html` template, the `page.html` template of the theme if one is used
or will render the built-in template: a blank page.

Whichever template you decide to render, you will get a `page` variable in your template
with the following fields:


```ts
content: String;
title: String?;
description: String?;
date: String?;
slug: String;
path: String;
draft: Bool;
// the path, split on '/'
components: Array<String>;
permalink: String;
summary: String?;
taxonomies: HashMap<String, Array<String>>;
extra: HashMap<String, Any>;
// Naive word count, will not work for languages without whitespace
word_count: Number;
// Based on https://help.medium.com/hc/en-us/articles/214991667-Read-time
reading_time: Number;
// `earlier` and `later` are only populated if the section variable `sort_by` is set to `date`
earlier: Page?;
later: Page?;
// `heavier` and `lighter` are only populated if the section variable `sort_by` is set to `weight`
heavier: Page?;
lighter: Page?;
// See the Table of contents section below for more details
toc: Array<Header>;
// Year/month/day is only set if the page has a date and month/day are 1-indexed
year: Number?;
month: Number?;
day: Number?;
// Paths of colocated assets, relative to the content directory
assets: Array<String>;
```

## Section variables
By default, Gutenberg will try to load `templates/index.html` for `content/_index.md`
and `templates/section.html` for others `_index.md` files. If there isn't
one, it will render the built-in template: a blank page.

Whichever template you decide to render, you will get a `section` variable in your template
with the following fields:


```ts
content: String;
title: String?;
description: String?;
date: String?;
slug: String;
path: String;
// the path, split on '/'
components: Array<String>;
permalink: String;
extra: HashMap<String, Any>;
// Pages directly in this section, sorted if asked
pages: Array<Pages>;
// Direct subsections to this section, sorted by subsections weight
subsections: Array<Section>;
// Unicode word count
word_count: Number;
// Based on https://help.medium.com/hc/en-us/articles/214991667-Read-time
reading_time: Number;
// See the Table of contents section below for more details
toc: Array<Header>;
// Paths of colocated assets, relative to the content directory
assets: Array<String>;
```

## Table of contents

Both page and section have a `toc` field which corresponds to an array of `Header`.
A `Header` has the following fields:

```ts
// The hX level
level: 1 | 2 | 3 | 4 | 5 | 6;
// The generated slug id
id: String;
// The text of the header
title: String;
// A link pointing directly to the header, using the inserted anchor
permalink: String;
// All lower level headers below this header
children: Array<Header>;
```

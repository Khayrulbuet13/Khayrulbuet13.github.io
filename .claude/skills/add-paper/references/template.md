# index.md template for content/papers/paperN/

Fill every `{{PLACEHOLDER}}`. Sections marked OPTIONAL: drop entirely (heading +
`---` divider) when there is no real content — never invent. Structure mirrors
the existing papers (paper13 is the reference).

```markdown
---
title: "{{TITLE}}"
date: {{YYYY-MM-DD}}
tags: [{{TAGS_QUOTED_COMMA_SEPARATED}}]
author: [{{AUTHORS_QUOTED_COMMA_SEPARATED}}]
description: "{{ONE_SENTENCE_DESCRIPTION_PLAIN_LANGUAGE}}"
summary: "{{ONE_TO_TWO_SENTENCE_SUMMARY_PLAIN_LANGUAGE}}"
cover:
    image: "paper{{N}}.png"
    alt: "{{SHORT_COVER_ALT}}"
    relative: true
editPost:
    URL: "{{JOURNAL_LANDING_URL}}"
    Text: "{{JOURNAL_NAME}}"
---


---

##### Download

+ [Paper](paper{{N}}.pdf)
+ [{{JOURNAL_NAME}}]({{JOURNAL_LANDING_URL}})
+ [Supplementary Materials]({{SUPP_URL}})          <!-- OPTIONAL -->
+ [arXiv]({{ARXIV_URL}})                           <!-- OPTIONAL -->
+ [GitHub Repository]({{GITHUB_URL}})              <!-- OPTIONAL -->
+ [Dataset]({{DATASET_URL}})                       <!-- OPTIONAL -->

---

##### Abstract

<div class="justify-text">

{{ABSTRACT_VERBATIM}}

</div>

---

##### Key Highlights
<!-- Plain-language bullets for a general reader — see SKILL.md "Tone" section -->

+ **{{LABEL_1}}**: {{HIGHLIGHT_1}}
+ **{{LABEL_2}}**: {{HIGHLIGHT_2}}
+ **{{LABEL_3}}**: {{HIGHLIGHT_3}}
+ **{{LABEL_4}}**: {{HIGHLIGHT_4}}

---

##### Citation

{{CHICAGO_STYLE_CITATION_WITH_DOI_LINK}}

```BibTeX
{{BIBTEX_FROM_DOI_ORG}}
```

---

##### Affiliations                                  <!-- OPTIONAL -->

1. {{AFFILIATION_1}}
2. {{AFFILIATION_2}}

---

##### Acknowledgments                               <!-- OPTIONAL -->

{{FUNDING_ONE_LINER}}
```

Conventions observed across existing papers:

- `date` drives list ordering (newest first). Use the publication date.
- `tags`: Title Case, reuse existing site tags where they fit.
- `author`: full names, paper order, `"Khayrul Islam"` exactly.
- `summary` renders on the papers list; `description` is the meta description.
- `summary`, `description`, and Key Highlights: plain-language, blog-post tone
  for a general reader (see SKILL.md → Tone). Abstract stays verbatim academic text.
- Abstract always wrapped in `<div class="justify-text">`.
- Citation: Chicago style ending with the DOI URL, then a `BibTeX` fenced block.
- A figure section (`##### Figure 1: …` + `![alt](paperN.png)`) may be added
  when the cover figure deserves explanation — optional.

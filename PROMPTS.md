# Content prompts

Prompts for the site text. Most fields are filled; a `[PROMPT <id>]` placeholder or an empty field marks one that is not.

To fill a placeholder, give an LLM:

1. the **Shared rules** block,
2. the **Source material** the prompt lists (all of it is in this repo),
3. the prompt itself,

then paste the answer over the placeholder in the file listed. This file and `linkedin.yml` are excluded from the Jekyll build.

## Shared rules (prepend to every prompt)

```
You are filling in text for Alexander Stepanov's personal academic website (al-folio theme).
Rules:
- Use only facts present in the source material below. Do not invent results, numbers, tools, or claims.
- Where LinkedIn already has a description for the item, reuse its wording verbatim or trim it. Only rephrase when it
  must be shortened or is grammatically broken (fix capitalization and typos only).
- Plain, factual tone. No flavor copy, taglines, metaphors, or mood lines (nothing like "building the future").
- Never use em dashes. Use a hyphen, comma, colon, or middle dot (·) instead.
- Do not mention or list skills, and do not mention GitHub.
- Return only the requested text, in the requested format, with no preamble.
```

## Source material

| Key            | Where                                                         | Notes                                                                                                                                             |
| -------------- | ------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------- |
| `LINKEDIN`     | `linkedin.yml` (verbatim snapshot, 2026-10-10)                | Sections: `HEADLINE`, `LOCATION`, `EXPERIENCE`, `EDUCATION`, `VOLUNTEER`, `ACTIVITY`. Projects, Publications, Honors, Certs, Languages are empty. |
| `ABOUT`        | `linkedin.yml` → `ABOUT`                                      | **Do not use.** It is only "building the future", which is exactly the kind of copy the rules forbid.                                             |
| `PREVIOUS_BIO` | below                                                         | Hero text from the old site, already approved in tone. Predates the HPE Labs role (Jun 2026) and the end of HERO2 (Aug 2026).                     |
| `PINCER`       | `_bibliography/papers.bib` + https://arxiv.org/abs/2610.02569 | Title, authors, arXiv id, abstract.                                                                                                               |

`PREVIOUS_BIO`:

```
Computer Science student at DHBW Stuttgart and UC Berkeley. Focused on AI security, machine learning, and optimization,
with a background in high-performance and GPU computing. Currently a researcher at SkyLab, Berkeley EECS, and a Corporate
Student in research and SWE at HPE, while building HERO2.
```

To refresh `linkedin.yml` later, see [Refreshing the LinkedIn snapshot](#refreshing-the-linkedin-snapshot) at the end.

---

## Site-wide

### site-description

- **File:** `_config.yml` → `description`
- **Used for:** HTML meta description, Open Graph / search snippet.
- **Source:** `HEADLINE`, current `EXPERIENCE` entries, `EDUCATION`

```
Write one sentence (max 155 characters) describing who Alexander Stepanov is: the study programs and current
research roles (SkyLab at UC Berkeley EECS, HPE Labs). Third person. Plain text, no Markdown.
```

### site-keywords

- **File:** `_config.yml` → `keywords`
- **Source:** `HEADLINE`, `EXPERIENCE`, `PINCER`

```
List 6 to 10 comma-separated SEO keywords: the full name, the institutions (UC Berkeley, SkyLab, HPE Labs,
DHBW Stuttgart) and research areas exactly as named in the source (e.g. AI security, LLM inference optimization).
No skills or tool names.
```

### contact-note

- **File:** `_config.yml` → `contact_note`
- **Used for:** one line under the social icons at the bottom of the about page.

```
Write one short sentence telling visitors that email is the best way to reach Alexander, with LinkedIn as an
alternative. Max 20 words. No exclamation marks.
```

---

## About page (`_pages/about.md`)

### about-bio

- **Field:** page body above the experience overview (Markdown)
- **Source:** `PREVIOUS_BIO`, `HEADLINE`, `PINCER`
- The experience and education tables below it already list every role, so the bio must not repeat them.

```
Write the homepage intro: 1 to 2 sentences, max 45 words, first person. Say what Alexander studies (CS at DHBW
Stuttgart, with time at UC Berkeley) and the research focus areas as worded in PREVIOUS_BIO (AI security, machine
learning, optimization). Do not list roles, employers, or advisors; those are in the experience table.
Plain Markdown, at most one link.
```

---

## Experience overview (`_data/experience.yml`)

Rendered on the home page by `_includes/experience.liquid` as a date | role table, followed by an education table.
Titles, organizations, dates, locations and URLs already match `linkedin.yml`. Only the one-line `line:` values are
placeholders. Education entries have no prose.

### experience-lines

- **Fields:** each `line:` (`[PROMPT exp:<slug>]`), including the three HPE `roles:` nested under Corporate Student
- **Source:** that role in `EXPERIENCE`, plus the extra facts listed

| Slug           | Role                                   | LinkedIn text to start from                                                                      | Extra facts                                                                         |
| -------------- | -------------------------------------- | ------------------------------------------------------------------------------------------------ | ----------------------------------------------------------------------------------- |
| `hpe_labs`     | Research Scientist Intern, HPE Labs    | "Research on building algorithms for LLM inference optimization"                                 | none                                                                                |
| `skylab`       | Researcher, SkyLab, UC Berkeley EECS   | "Research on AI security @ SkyLab" + advisor Prof. Dr. Raluca Ada Popa                           | co-author of the `PINCER` preprint (link https://arxiv.org/abs/2610.02569)          |
| `ieor`         | Researcher, Berkeley IEOR              | "Research at the intersection of optimization and machine learning" + advisor Prof. Dr. Hochbaum | none                                                                                |
| `hero2`        | Lead Engineer, HERO2                   | "Co-led building up app & web infra and ml pipelines; mentored 4 interns"                        | old site: "platform tokenizing sustainable mobility into verifiable carbon credits" |
| `hpe_lsip`     | Research Engineering Intern, LSIP Labs | GPU-based hardware simulator text                                                                | presented this work at the Stanford Software Theory Group (Apr 2026)                |
| `hpe_hpc`      | SWE Intern, HPC AI & Delivery Services | OS image automation text                                                                         | none                                                                                |
| `hpe_services` | SWE Intern, Services                   | X-ray device update text                                                                         | none                                                                                |
| `pinetco`      | IT Consultant, Pinetco                 | software testing and project coordination text                                                   | none                                                                                |
| `freelance`    | Software Programmer & Python Teacher   | automation for small businesses & teaching kids Python                                           | none                                                                                |

```
For the role "<role>" write one line (max 22 words) to show under it in an experience table. Start from the
LinkedIn text verbatim and trim it; fix only capitalization, typos and "@". Name the advisor as "Advisor: <name>"
if LinkedIn does. Add the extra fact only if it fits within the word limit. Markdown links allowed for URLs in the
source. No trailing period needed if it is a fragment. Return the line only.
```

---

## Interests (`_pages/interests.md`)

A short page of research interests, one `###` section each. These are research topics, not a skills list.

### interests-page-description

- **Field:** `_pages/interests.md` front matter `description`

```
Write a one-line description for the interests page (max 12 words), e.g. "Research topics I work on or follow."
Plain text.
```

### interests

- **Fields:** `[PROMPT interest:<n>_title]` and `[PROMPT interest:<n>_body]` in `_pages/interests.md`
  (3 sections are stubbed; add or delete sections to end up with 3 to 5)
- **Source:** `PREVIOUS_BIO` focus areas, `HEADLINE`, `EXPERIENCE`, `PINCER`, `ACTIVITY`
- **Candidates** (Alexander confirms the final list and order):
  1. AI security and agent security · SkyLab, `PINCER`
  2. ML systems and LLM inference optimization · HPE Labs, `HEADLINE` ("ML Systems @ HPE")
  3. Optimization and machine learning · Berkeley IEOR
  4. Hardware for hard optimization problems: in-memory computing, SAT solving · HPE LSIP Labs, Stanford talk
  5. High-performance and GPU computing · `PREVIOUS_BIO`, HPE HPC and LSIP roles

```
For the interest "<topic>" write:
title: 2 to 5 words, lowercase except proper nouns and acronyms.
body: 1 to 2 sentences, max 40 words, first person. Say what about the topic Alexander works on, then name the related
role or paper from the source with a Markdown link (e.g. the Pincer preprint, SkyLab, HPE Labs).
Only claim work that appears in the source. No tool or programming language lists.
Return:
title: ...
body: ...
```

---

## Publications (`_pages/publications.md`, `_bibliography/papers.bib`)

`papers.bib` already has the Pincer entry (from arXiv) marked `selected={true}`, so it shows on the about page and the
publications page.

### publications-page-description

- **Field:** `_pages/publications.md` front matter `description`

```
Write a one-line description for the publications page (max 12 words), e.g. noting reverse chronological order.
Plain text.
```

### publications-bibtex

- **File:** `_bibliography/papers.bib`, for future papers
- **Note:** the Pincer `abstract` field was left out because the arXiv abstract contains em dashes. Add it back verbatim
  if the abstract button is wanted, or leave it out.

```
Convert this paper into a BibTeX entry (@article, @inproceedings, or @misc for preprints). Use the exact title,
author list and order, venue, year and URL from the source; leave a field out rather than guess. Add al-folio fields
when known: abbr={VENUE_SHORT}, arxiv={id}, pdf={url}, html={url}, bibtex_show={true}, selected={true} if it should
appear on the homepage. Cite key: <firstauthorlastname><year><firsttitleword>.
```

---

## Refreshing the LinkedIn snapshot

Give this to an agent that can open LinkedIn while logged in (for example Claude in Chrome), then replace
`linkedin.yml` with its answer and re-check `_data/experience.yml` facts against it.

```
Open my LinkedIn profile at https://www.linkedin.com/in/alxstx/ while logged in as me, and pull out its content
exactly as written.

Rules:
- Copy text word for word. Do not summarize, rephrase, fix typos, or add anything.
- Expand every "see more" / "…more" and open every "Show all N …" page so nothing is cut off.
- List each position separately, even when grouped under one company.
- Dates as YYYY-MM, "present" for current roles. Include every URL shown.
- Write NONE for an empty or missing section. Never guess.
- Skip Skills, Endorsements, Recommendations, People also viewed, ads, and the birthday.
- Don't click anything that changes the profile, sends a message, or follows/connects.

Return one YAML document with these keys, using | block scalars for multi-line text:
HEADLINE, LOCATION, CONTACT_INFO {website, email}, ABOUT, FEATURED [title, type, url, description],
EXPERIENCE [company, company_url, title, employment_type, start, end, location, work_mode, description, attached_media],
EDUCATION [school, degree, field, start, end, grade, activities, description],
PROJECTS [name, start, end, associated_with, url, contributors, description],
PUBLICATIONS [title, publisher_or_venue, date, url, authors, description],
HONORS [title, issuer, date, associated_with, description], CERTS [name, issuer, issued, credential_url],
LANGUAGES [name, proficiency], VOLUNTEER [organization, role, cause, start, end, description],
COURSES_AND_TEST_SCORES,
ACTIVITY [date, url, text]: my own posts from the last 12 months announcing a new role, program, paper, talk, award,
or project launch (first ~3 sentences verbatim; skip reposts and comments).

Finish with a short list of anything you couldn't open or read completely.
```

---
name: express-audit
description: Quick audit of a website or web page with CheckSite — what is broken and what to fix first. Use when the user asks to check, audit or review a site, asks why a site is not in Yandex or Google, asks whether a site is ready for launch or indexing, or asks whether a Russian site complies with 152-FZ (personal data), consumer protection or advertising law.
---

# Express audit with CheckSite

The goal is a short, prioritized answer: **what to fix first and why**, not a dump of every factor.

## 1. Run the check

1. Take the URL from the user. A bare domain is fine (`example.ru`). If they gave several sites, check each one separately; do not crawl many pages of one site — one call checks one page, usually the home page is enough for an express audit.
2. Pick the search engine norms:
   - `searcher: "yandex"` when the site targets Russia/CIS or the user mentions Yandex;
   - `searcher: "google"` when the user mentions Google or the site targets other markets;
   - otherwise leave the default `all`.
3. Call the CheckSite connector's `checksite_audit` tool. Keep `onlyProblems: true` for an express audit.
4. If the tool refuses (bad URL, site owner forbade checks, rate limit), tell the user the reason in plain words and stop. If the connector is not available, say that the CheckSite connector needs to be connected and suggest a manual check at `https://checksite.ru/?url=<domain>`. Do not invent results.

The report texts come in Russian. Answer in the language the user writes in. If the request is only a URL
(for example the `/checksite:audit` command with no other words), answer in the language of the site's
audience: Russian for `.ru`, `.рф`, `.su` and other Russian-language sites, English otherwise.

## 2. Prioritize

Sort the findings into three tiers, in this order:

1. **Blocks the site from search or from visitors.** Server errors, broken redirects, `noindex` or `robots.txt` closing the site, bots getting a different answer than visitors, missing or broken sitemap, SSL problems, the site being on the Roskomnadzor block list. Nothing else matters until these are fixed.
2. **Legal risk (for sites aimed at Russia).** 152-FZ: no personal data policy, no consent checkbox in forms or a pre-checked one, analytics counters firing before consent, no cookie banner or no way to refuse cookies. Consumer protection: no seller name, address, OGRN/INN. Advertising and child-protection law findings. These carry fines — say so, without exaggerating amounts.
3. **Ranking and snippet quality.** Title and description length and presence, a single H1, thin or keyword-poor content, missing Open Graph, heavy pages with too many resources, missing security headers (CSP, Permissions-Policy).

Items marked `[CRITICAL]` go up a tier. `[ADVICE]` items are recommendations, not errors — mention them last, only if they are cheap to do.

## 3. Answer

It is an **express** audit: the whole answer should fit on one screen, roughly 15–20 lines.

- **Verdict:** one line with the overall score and the main conclusion.
- **Fix first:** at most **3** items. Each item is one or two lines: what is wrong and exactly what to do,
  with the page's own values ("title is 33 characters — make it 40–60"). Add *why* only in a short clause
  when it is not obvious. No sub-bullets, no separate "Why it matters" / "Fix" lines.
- **Also worth doing:** at most 3 one-line items, only if there is something left worth mentioning.
- Do not list passed checks or every group score; mention a group score only when it explains the verdict.
- No jargon without a few-word explanation — the reader is often a site owner, not an SEO specialist.
- Last line: the link to the full interactive report exactly as the tool returned it
  (`https://checksite.ru/?url=<domain>`), not the bare site address.

If the user asks for details on a point, then expand — not before.

Do not claim things the check did not measure: positions in search, traffic, backlinks, competitors and page speed in a real browser are not part of this audit.

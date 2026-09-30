# CheckSite

Express website audit by [CheckSite.ru](https://checksite.ru) inside Claude. Ask Claude to check a site and get
a short, prioritized answer: what blocks the site from Yandex and Google, what creates legal risk under
Russian law, and what to improve next.

## What it checks

- **Indexing and access:** server response and redirects, `robots.txt`, sitemap, `noindex`, whether search
  and AI bots get the same page as visitors, SSL, Roskomnadzor block list.
- **Meta tags and content:** title, description, headings, Open Graph, text volume and keyword density,
  page weight and number of resources, security headers (CSP, Permissions-Policy).
- **Russian-law compliance:** 152-FZ personal data (policy, consent checkbox, cookie banner, analytics
  before consent), consumer protection (seller details, OGRN/INN), advertising law, child-protection law.

Norms for title and description differ between Yandex and Google; Claude picks the right set from your request.

## How to use

Install the plugin and connect the bundled **CheckSite** connector. Then just ask:

- "Check example.ru and tell me what to fix first"
- "Is my site ready for Yandex indexing?"
- "Does example.ru comply with 152-FZ?"

In Claude Code you can also run `/checksite:audit example.ru`.

One request checks one page (usually the home page). Checks take 10–60 seconds. Report texts from CheckSite
are in Russian; Claude answers in your language.

## Data and privacy

The plugin connects to one remote MCP server: `https://api.checksite.ru/mcp`, operated by CheckSite.

- **What is sent:** only the URL you ask to check and the chosen search-engine norms. No personal data,
  no files, no conversation content.
- **What CheckSite does:** fetches the public page and its `robots.txt` from its own servers and analyzes them.
  The page must be publicly reachable. Site owners can forbid checks of their domain in their CheckSite account.
- **What is stored:** the checked URL and time are written to the CheckSite check log for statistics.
- **Limits:** the connector has shared rate limits; when they are reached, Claude tells you to retry later.

No account or API key is needed.

## License

MIT — see [LICENSE](LICENSE).

---

## По-русски

Экспресс-аудит сайта от [CheckSite.ru](https://checksite.ru) прямо в Claude: что мешает попасть в Яндекс
и Google, что грозит штрафами по ФЗ-152, ЗоЗПП и закону о рекламе, и что чинить в первую очередь.
Попросите Claude «проверь сайт example.ru» или в Claude Code наберите `/checksite:audit example.ru`.
В CheckSite уходит только адрес проверяемой страницы; регистрация и ключи не нужны.

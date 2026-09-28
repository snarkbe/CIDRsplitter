# Discoverability

All three pages carry per-page SEO metadata (title, description, Open Graph and Twitter cards), an inline SVG favicon, and `WebApplication` + `FAQPage` [JSON-LD](https://schema.org/) structured data.

- **One FAQ per page.** Each page's `FAQPage` markup mirrors its own on-page FAQ: cloud reserved IPs on the Splitter, lookup questions on the Calculator, overlap and address planning on the Overlap Checker. The pages don't compete with duplicate content.
- **Separate URLs.** The tools each target their own search intent and are linked through the tool tabs.
- **Crawlers.** `robots.txt` and `sitemap.xml` at the repo root list all three pages.

When you add a page, update `sitemap.xml`, give it its own canonical URL and JSON-LD, and add it to the tool tabs of the other pages.

[Back to the overview](../README.md)

Pratishtha Finance Services — Website

Single-page website for Pratishtha Finance Services, an MSME-registered Direct Selling Agent (DSA) based in Maharajganj, Uttar Pradesh, offering loan facilitation through 116+ bank and NBFC partners, plus a daily/weekly/monthly savings (RD) enrollment tool.

Live domain: https://pratishtha.pro

File
File	Purpose
pratishtha-finance.html	The entire site — HTML, CSS, and JS in one file. No build step required.

Deployment reference for robots.txt and llms.txt is included as an HTML comment at the top of the file — copy that content into separate root-level files when deploying (see Deployment below).

Sections (in page order)
Home (#home) — Hero, loan types, quick CTA
Process (#process) — How it works
About (#about) — Company info
Loans (#loans) — Business, Personal, Home, LAP, MSME, Vehicle, Education, Gold
Eligibility (#eligibility)
Apply (#apply) — Loan application form → sends to WhatsApp
Calculator (#calculator) — EMI calculator
Tracking (#tracking) — Application status check
Savings (#savings) — RD/daily-collection savings plan enrollment + calculator
Partners (#partners) — 116+ bank/NBFC logos, filterable by category
Join (#join) — Become a DSA/agent/referral partner
Reviews (#reviews)
FAQ (#faq) — 25 questions, also exposed as static FAQPage schema (see SEO)
Knowledge (#knowledge)
Trust (#trust)
Contact (#contact) — Phone, WhatsApp, email, address, map
Forms & WhatsApp integration

All forms (loan application, RD enrollment, agent signup) build a formatted message client-side and open wa.me/917233023547 with the message pre-filled — there is no backend. Submissions are not stored anywhere except in the WhatsApp conversation.

Phone/WhatsApp: +91 7233023547, +91 6306864182
Email: pratishthafinance@gmail.com
Address: Dhanna Nayak, Partawal, Maharajganj, Uttar Pradesh 273301
Hours: Mon–Sat, 9:00 AM – 7:00 PM
SEO
<title>, meta description, keywords, canonical, hreflang (en/hi), Open Graph, Twitter Card
JSON-LD: FinancialService, BreadcrumbList, FAQPage (all 25 FAQs — kept static in <head>, not JS-injected, so non-JS crawlers can read it)
AI-crawler access explicitly allowed for GPTBot (ChatGPT), Google-Extended (Gemini), PerplexityBot, ClaudeBot, CCBot
llms.txt reference block included for AI-assistant discoverability
Deployment

The robots.txt, sitemap.xml, and llms.txt content is documented as a comment block at the very top of pratishtha-finance.html. On deploy, create these as separate files at the domain root — they don't function from inside the HTML file:

https://pratishtha.pro/robots.txt
https://pratishtha.pro/sitemap.xml
https://pratishtha.pro/llms.txt

After going live:

Submit sitemap.xml in Google Search Console
Set up a Google Business Profile with the Maharajganj address
Check load speed with PageSpeed Insights
Verify og-image.jpg and logo.png exist at the referenced paths
Known fix history
Partner-logo onerror fallback handlers used this.nextSibling (matches whitespace text nodes, not elements) — fixed to this.nextElementSibling across all 114 logo <img> tags. This was throwing a Cannot set properties of undefined (setting 'display') error on every logo-image load failure.

# Pratishtha Finance Services

**Single-page marketing & lead-generation website for a loan DSA (Direct Selling Agent) business.**

Live domain: **[pratishtha.pro](https://pratishtha.pro)**
Stack: Vanilla HTML / CSS / JS — zero dependencies, zero build step
Status: Production-ready

---

## Table of Contents

- [Overview](#overview)
- [Tech Stack](#tech-stack)
- [Project Structure](#project-structure)
- [Features](#features)
- [Page Sections](#page-sections)
- [Lead Capture Flow](#lead-capture-flow)
- [Internationalization](#internationalization)
- [SEO & Discoverability](#seo--discoverability)
- [Deployment](#deployment)
- [Post-Launch Checklist](#post-launch-checklist)
- [Business Details](#business-details)
- [Changelog](#changelog)

---

## Overview

Pratishtha Finance Services is an MSME-registered DSA in Maharajganj, Uttar Pradesh, that connects customers to loan products across **116+ bank and NBFC partners**. This site is the company's digital storefront: it explains loan products, runs eligibility and EMI calculators, and converts visitors into leads via WhatsApp — with no backend, database, or server required.

## Tech Stack

| Layer | Choice | Why |
|---|---|---|
| Markup | Semantic HTML5 | Single file, easy to host anywhere |
| Styling | Vanilla CSS (custom properties) | No framework overhead; `:root` design tokens for the brand palette |
| Fonts | Playfair Display (headings) + Poppins (body), via Google Fonts | Editorial/trustworthy finance feel |
| Interactivity | Vanilla JavaScript | Calculators, form validation, i18n, modals, filters |
| Lead delivery | WhatsApp Click-to-Chat (`wa.me`) | No backend — form data is formatted and handed to WhatsApp |
| Structured data | JSON-LD (`FinancialService`, `BreadcrumbList`, `FAQPage`) | Rich results + AI-assistant discoverability |

No package manager, no build pipeline. Open the file or deploy it as a static asset — that's the whole stack.

## Project Structure

```
pratishtha-finance.html   ← everything: <head> metadata, <style>, markup, <script>
README.md                 ← this file
```

Internally, the single file is organized as:

```
<head>
  Meta / SEO tags, canonical, hreflang, Open Graph, Twitter Card
  JSON-LD: FinancialService, BreadcrumbList, FAQPage
  <style> — design tokens (--navy, --teal, --gold, --green) + component styles

<body>
  <nav>                    Sticky nav + mobile hamburger menu
  <section id="home">      Hero
  <section id="process">   How it works
  <section id="about">
  <section id="loans">     8 loan product cards
  <section id="eligibility">
  <section id="apply">     Application form -> WhatsApp
  <section id="calculator">EMI calculator
  <section id="tracking">  Application status lookup
  <section id="savings">   RD / savings plan calculator + enrollment
  <section id="partners">  116+ bank/NBFC logos, filterable
  <section id="join">      Agent / DSA / referral signup
  <section id="reviews">
  <section id="faq">       25 Q&As
  <section id="knowledge">
  <section id="trust">
  <section id="contact">
  <footer>

  <script>                 All interactivity - see Features below
```

## Features

- **EMI Calculator** — `calcEMI()` computes monthly installment live from principal, rate, and tenure
- **Eligibility Checker** — `checkEligibility()` gives an instant read on loan eligibility from user inputs
- **RD / Savings Calculator** — `calcRD()`, `previewRD()`, `updateDurationOptions()` model daily/weekly/monthly savings plans with maturity and bonus projections
- **Application Tracking** — `trackApplication()`, `checkRDStatus()` — lightweight status lookup UI
- **Partner Directory** — `filterPartners()` filters 116+ bank/NBFC/MFI/HFC/Fintech logos by category, with graceful text-fallback if a logo image fails to load
- **Bilingual UI** — `setLanguage()` + `translations` object toggles the entire UI between English and Hindi
- **Animated Counters** — `IntersectionObserver`-driven count-up animation for hero stats
- **Modals & Toasts** — `openModal()`, `closeModal()`, `showToast()` for privacy policy, disclaimers, and form feedback
- **Aadhaar Input Formatting** — `formatAadhaar()` auto-spaces Aadhaar numbers as the user types
- **Photo Preview** — `previewPartnerPhoto()` lets agent applicants preview an uploaded photo before submitting

## Page Sections

| Anchor | Section |
|---|---|
| `#home` | Hero — loan types, amount range, primary CTA |
| `#process` | How it works |
| `#about` | Company overview |
| `#loans` | Business, Personal, Home, LAP, MSME, Vehicle, Education, Gold |
| `#eligibility` | Eligibility checker |
| `#apply` | Loan application form |
| `#calculator` | EMI calculator |
| `#tracking` | Application status lookup |
| `#savings` | RD/savings plan calculator + enrollment |
| `#partners` | Bank/NBFC partner directory, filterable |
| `#join` | Become a DSA / referral / branch partner |
| `#reviews` | Customer reviews |
| `#faq` | 25 FAQs (also exposed as structured data) |
| `#knowledge` | Financial literacy content |
| `#trust` | Trust signals / disclaimers |
| `#contact` | Phone, WhatsApp, email, address, map |

## Lead Capture Flow

There is no backend. Every form (`enrollRD()`, `submitForm()`, `submitPartnerForm()`) follows the same pattern:

1. Read and validate field values client-side
2. Build a formatted, emoji-labelled bilingual (EN/HI) message string
3. `encodeURIComponent()` the message and open `https://wa.me/917233023547?text=...`
4. Show a success toast

Nothing is stored server-side — the WhatsApp conversation *is* the CRM record.

## Internationalization

The `translations` object plus `setLanguage(lang)` swap all UI copy between English and Hindi without a page reload. WhatsApp-bound messages are always sent bilingually (label in English / Hindi side by side) regardless of the active UI language, so the business owner never has to context-switch.

## SEO & Discoverability

- Full metadata: `<title>`, meta description/keywords, canonical URL, `hreflang` (en/hi/x-default), Open Graph, Twitter Card
- Structured data (JSON-LD): `FinancialService`, `BreadcrumbList`, and a **static** `FAQPage` (25 entries) — deliberately kept static rather than JS-injected so crawlers that don't execute JavaScript can still read it
- AI-crawler access explicitly permitted: GPTBot (ChatGPT), Google-Extended (Gemini), PerplexityBot, ClaudeBot, CCBot
- `llms.txt` reference block for AI-assistant discoverability

The `robots.txt`, `sitemap.xml`, and `llms.txt` content is documented in an HTML comment at the very top of `pratishtha-finance.html`, ready to be extracted into real files at deploy time.

## Deployment

This is a static file — deploy it anywhere that serves static assets (Netlify, Vercel, GitHub Pages, cPanel, S3 + CloudFront, etc.).

1. Upload `pratishtha-finance.html` to the host as `index.html`
2. Extract the `robots.txt` / `sitemap.xml` / `llms.txt` content from the comment block at the top of the file into three separate files at the domain root:
   - `https://pratishtha.pro/robots.txt`
   - `https://pratishtha.pro/sitemap.xml`
   - `https://pratishtha.pro/llms.txt`
3. Point DNS for `pratishtha.pro` at the host
4. Confirm `og-image.jpg` and `logo.png` exist at the paths referenced in the `<head>` meta tags

## Post-Launch Checklist

- [ ] Submit `sitemap.xml` in Google Search Console
- [ ] Create a Google Business Profile with the Maharajganj address
- [ ] Run PageSpeed Insights and address any flagged issues
- [ ] Verify all 116+ partner logos render (or gracefully fall back) in production
- [ ] Test both WhatsApp numbers receive form submissions correctly
- [ ] Confirm EN/HI language toggle persists correctly across all sections

## Business Details

| | |
|---|---|
| Legal status | MSME Registered Direct Selling Agent (DSA) |
| Phone / WhatsApp | +91 7233023547 · +91 6306864182 |
| Email | pratishthafinance@gmail.com |
| Address | Dhanna Nayak, Partawal, Maharajganj, Uttar Pradesh 273301 |
| Hours | Mon–Sat, 9:00 AM – 7:00 PM |
| Loan range | ₹10,000 – ₹2.5 Crore |
| Rate | From 7.35% p.a. |
| Products | Business, Personal, Home, LAP, MSME, Vehicle, Education, Gold Loans |

## Changelog

**Domain migration** — All canonical/OG/Twitter/JSON-LD URLs updated from `pratishthafinance.in` to `pratishtha.pro`.

**AI-crawler SEO** — `FAQPage` JSON-LD moved from JS-injected to static `<head>` markup (non-JS crawlers such as GPTBot/ClaudeBot were missing it entirely); `robots.txt`/`llms.txt` reference blocks added with explicit AI-crawler allow rules.

**Bug fix** — Partner-logo `onerror` fallback handlers referenced `this.nextSibling`, which resolves to a whitespace text node (not the fallback `<div>`) due to the newline between tags in source. This threw `Cannot set properties of undefined (setting 'display')` on every logo load failure, across all 114 logo `<img>` tags. Fixed by switching to `this.nextElementSibling`, which correctly skips text nodes and targets the fallback element.

<h1 align="center">Hi, I'm Vivek 👋</h1>

<p align="center">
  <b>Founder &amp; full-stack engineer.</b> I build and ship products end to end —
  <br/>commerce apps, cross-platform mobile, native macOS/iOS, and polished web front ends.
</p>

<p align="center">
  📍 Bengaluru, India &nbsp;·&nbsp; 🛠 Building under <a href="https://github.com/starlance"><b>@starlance</b></a> &nbsp;·&nbsp; ⚡ Currently shipping <b>Starlog</b>
</p>

<p align="center">
  <a href="https://vivek-portfolio-vivekreddy.netlify.app"><img alt="Live portfolio" src="https://img.shields.io/badge/Interactive%20r%C3%A9sum%C3%A9-Live%20demo-2ea043?style=for-the-badge&logo=netlify&logoColor=white"></a>
  <a href="https://linkedin.com/in/vivekreddy"><img alt="LinkedIn" src="https://img.shields.io/badge/LinkedIn-0a66c2?style=for-the-badge&logo=linkedin&logoColor=white"></a>
  <a href="https://x.com/vivekreddy"><img alt="X" src="https://img.shields.io/badge/@vivekreddy-000000?style=for-the-badge&logo=x&logoColor=white"></a>
  <a href="mailto:starlancegrp@gmail.com"><img alt="Email" src="https://img.shields.io/badge/Email-ea4335?style=for-the-badge&logo=gmail&logoColor=white"></a>
</p>

---

## 🎯 What I do

I take products from a blank repo to something people actually use. In practice that means jumping across the stack in a single project — a **Shopify Cart Transform Function** one day, a **SwiftUI** view or a **Flutter** paywall the next, and a **Next.js** front end after that. Most of my work is private client and product code, so the sections below are **architectural write-ups** rather than open source — the "how it's built," with diagrams, since the source isn't public.

## 🖥 Interactive résumé — live demo

To make this profile more than a static page, I rebuilt GitHub's own profile **Overview** as a pixel-faithful clone and deployed it. It's a genuine front-end exercise (**Next.js 16 · React 19 · Tailwind v4 · TypeScript**), with a deterministically-seeded contribution heatmap that renders identically on server and client.

<p align="center">
  <a href="https://vivek-portfolio-vivekreddy.netlify.app">
    <img src="assets/portfolio.png" alt="Interactive résumé — a pixel-faithful GitHub profile clone" width="820">
  </a>
  <br/>
  <sub><b><a href="https://vivek-portfolio-vivekreddy.netlify.app">▶ vivek-portfolio-vivekreddy.netlify.app</a></b> — click to interact</sub>
</p>

---

## 🚀 Featured work

> Deep-dives are collapsed to keep this scannable. Expand any project for the full architecture.

### 🛒 Starbundle — Shopify "Mix &amp; Match" bundles app

A Shopify app that lets merchants build **Mix &amp; Match** bundles with **tiered discounts**. Shoppers pick any *N* items from configured collections; the storefront widget calculates the discount live, and — critically — the discount **survives checkout** via a Cart Transform Function instead of fragile cart attributes.

`Remix 2.16 (Vite)` · `Polaris 12 + App Bridge` · `Prisma + SQLite/Postgres` · `Cart Transform Function` · `Theme app extension` · `Vitest`

```mermaid
flowchart LR
    subgraph SF["🛍️ Storefront (theme)"]
      W["Bundle Widget<br/>Liquid + vanilla JS/CSS"]
    end
    subgraph SH["Shopify platform"]
      AP["App Proxy<br/>(HMAC-verified)"]
      CT["Cart Transform<br/>Function"]
      CO["Checkout"]
    end
    subgraph APP["Remix app · embedded admin"]
      R["Routes"]
      PL["pricing.ts<br/>tier evaluation"]
      DB[("Prisma<br/>Bundles · Tiers · Analytics")]
    end
    ADM["Merchant<br/>Polaris dashboard"] --> R
    W -->|"GET bundle + products"| AP --> R
    W -->|"POST view / add-to-cart / convert"| AP
    R <--> DB
    R -. "same tier logic" .-> PL
    CT -. "JS mirror of pricing.ts" .-> PL
    CO --> CT -->|"apply best-eligible tier"| CO
```

<details>
<summary><b>Architecture notes</b></summary>

- **One source of truth for pricing, mirrored across two runtimes.** Tier evaluation (`any 3 → 10%`, `any 5 → 20%`, highest-eligible wins) lives in `app/lib/pricing.ts`, unit-tested with Vitest. The Cart Transform Function can't import app code, so `pricing.js` is a deliberate mirror — the tests guard both.
- **Discounts persist without cart hacks.** Rather than writing cart attributes and hoping they survive, the **Cart Transform Function** re-derives the discount at checkout from the bundle definition, so totals are correct even if the shopper edits the cart.
- **App Proxy is the storefront's only door in.** The widget talks to `proxy.bundle.tsx` (definition + products) and `proxy.events.tsx` (analytics) through Shopify's App Proxy, with HMAC verification in `proxyAuth.server.ts`.
- **Attribution via webhooks.** `webhooks.orders.create.tsx` closes the loop — views → add-to-carts → conversions are counted per bundle for the analytics dashboard.
- **Onboarding that actually verifies.** The onboarding route polls live theme settings (`api.onboarding-check.tsx`) to confirm the storefront extension is enabled before declaring setup complete.

</details>

---

### 📱 Starlog — cross-platform mobile app *(in active development)*

The product I'm currently building. A **Flutter** app targeting **iOS and Android** from one codebase, monetized with subscriptions **and** consumable packs.

`Flutter / Dart` · `RevenueCat (purchases_flutter)` · `iOS + Android`

<details>
<summary><b>Architecture notes</b></summary>

- **Monetization via RevenueCat.** Subscriptions and consumable receipt packs are delivered through `purchases_flutter`, configured at boot with platform SDK keys.
- **No secrets in git.** Keys are injected with `--dart-define-from-file` from a gitignored `dart_defines.json`; `scripts/run.sh` and the VS Code launch configs wire it up so local runs and CI stay clean.
- **One codebase, two stores.** Shared Dart UI and business logic ship to both App Store and Play Store.

</details>

---

### 🗂 Mac File Organizer — native macOS app *(shipped)*

A **SwiftUI** macOS app that sorts a folder's files into categorized destinations by type, with a polished dark UI. Distributed to users via a public [releases repo](https://github.com/vivekreddy/Mac-File-Organizer-Releases).

`SwiftUI` · `macOS 14+` · `SF Symbols` · `Drag &amp; drop`

```mermaid
flowchart LR
    SRC["📁 Source folder"] --> SCAN["Scan + classify<br/>by extension"]
    SCAN --> C{"Category"}
    C --> IMG["Images"]
    C --> DOC["Documents"]
    C --> VID["Video / Audio"]
    C --> ARC["Archives"]
    C --> OTH["Other"]
```

<details>
<summary><b>Highlights</b></summary>

- **Real product, not a toy.** Ships as a distributable macOS build with a dedicated public releases channel.
- **SwiftUI-native UX** — real-time search, drag &amp; drop, quick-access sidebar, spring animations, translucent materials, and automatic SF Symbol icons per file type.

</details>

---

### 🧾 ReceiptScanner — iOS expense capture

An **iOS** app that photographs receipts, reads them with **on-device OCR**, and files them into Google Drive organized by month — no data leaves the phone until you upload.

`SwiftUI` · `Vision (on-device OCR)` · `Google Drive API` · `GoogleSignIn`

```mermaid
flowchart LR
    CAM["📷 Capture / library"] --> OCR["Vision OCR<br/>on-device"]
    OCR --> EX["Extract store · amount · date"]
    EX --> ED["Manual edit sheet"]
    ED --> FN["YYYY-MM-DD_Store_Amount.jpg"]
    FN --> GD[("Google Drive<br/>Receipts / YYYY-MM")]
```

<details>
<summary><b>Highlights</b></summary>

- **On-device OCR first.** Apple's Vision framework auto-detects store name, amount, and date locally; the user can correct any field before upload.
- **Deterministic filing.** Every receipt lands as `YYYY-MM-DD_Store_Amount.jpg` under a `Receipts / YYYY-MM` folder tree in Drive, with live upload progress.

</details>

---

### 🕉 HinduHub &amp; web work

A **Next.js** community platform for Hindu temples, events, and resources — notably using **`astronomy-engine`** to compute panchang/astronomical data (tithis, nakshatras) client-side. Part of a broader stream of Next.js / Astro / TypeScript sites I build for products and clients.

`Next.js` · `React` · `TypeScript` · `astronomy-engine` · `date-fns`

---

<details>
<summary><h3>📦 More projects</h3></summary>

| Project | What it is | Stack |
| --- | --- | --- |
| **starlance-website** | Studio / product site for Starlance | TypeScript · Next.js |
| **starlog-website** | Marketing site for the Starlog app | TypeScript · Next.js |
| **cultfit-attribution / -renewals** | Marketing attribution &amp; renewals analytics | JavaScript |
| **shopify-currency-converter** | Storefront currency conversion | Liquid |
| **WebLinkScan** | Broken-link / web link scanner | TypeScript |
| **dev-utility-hub** | Collection of developer utilities | TypeScript |
| **Expense-Manager-iOS** | See *ReceiptScanner* above | Swift |

</details>

---

## 🧰 Toolbox

**Languages**
<br/>
![TypeScript](https://img.shields.io/badge/TypeScript-3178c6?style=flat-square&logo=typescript&logoColor=white)
![Swift](https://img.shields.io/badge/Swift-f05138?style=flat-square&logo=swift&logoColor=white)
![Dart](https://img.shields.io/badge/Dart-0175c2?style=flat-square&logo=dart&logoColor=white)
![JavaScript](https://img.shields.io/badge/JavaScript-f7df1e?style=flat-square&logo=javascript&logoColor=black)
![Python](https://img.shields.io/badge/Python-3776ab?style=flat-square&logo=python&logoColor=white)

**Web &amp; mobile**
<br/>
![Next.js](https://img.shields.io/badge/Next.js-000000?style=flat-square&logo=nextdotjs&logoColor=white)
![React](https://img.shields.io/badge/React-20232a?style=flat-square&logo=react&logoColor=61dafb)
![Remix](https://img.shields.io/badge/Remix-000000?style=flat-square&logo=remix&logoColor=white)
![Tailwind CSS](https://img.shields.io/badge/Tailwind-06b6d4?style=flat-square&logo=tailwindcss&logoColor=white)
![SwiftUI](https://img.shields.io/badge/SwiftUI-0071e3?style=flat-square&logo=swift&logoColor=white)
![Flutter](https://img.shields.io/badge/Flutter-02569b?style=flat-square&logo=flutter&logoColor=white)

**Platform &amp; tooling**
<br/>
![Shopify](https://img.shields.io/badge/Shopify-7ab55c?style=flat-square&logo=shopify&logoColor=white)
![Prisma](https://img.shields.io/badge/Prisma-2d3748?style=flat-square&logo=prisma&logoColor=white)
![Node.js](https://img.shields.io/badge/Node.js-339933?style=flat-square&logo=nodedotjs&logoColor=white)
![Vite](https://img.shields.io/badge/Vite-646cff?style=flat-square&logo=vite&logoColor=white)
![Netlify](https://img.shields.io/badge/Netlify-00c7b7?style=flat-square&logo=netlify&logoColor=white)
![Vercel](https://img.shields.io/badge/Vercel-000000?style=flat-square&logo=vercel&logoColor=white)

---

## 📊 GitHub

<p align="center">
  <img height="165" src="https://github-readme-stats.vercel.app/api?username=vivekreddy&show_icons=true&hide_border=true&theme=github_dark&count_private=true&include_all_commits=true" alt="Vivek's GitHub stats" />
  <img height="165" src="https://github-readme-stats.vercel.app/api/top-langs/?username=vivekreddy&layout=compact&hide_border=true&theme=github_dark&langs_count=8" alt="Top languages" />
</p>

<sub>Language totals reflect public repos; most of my work is private, so this under-counts Swift, Dart, and Liquid.</sub>

---

<p align="center">
  <b>Let's build something.</b>
  <br/>
  <a href="https://vivek-portfolio-vivekreddy.netlify.app">Portfolio</a> ·
  <a href="https://linkedin.com/in/vivekreddy">LinkedIn</a> ·
  <a href="https://x.com/vivekreddy">X</a> ·
  <a href="mailto:starlancegrp@gmail.com">starlancegrp@gmail.com</a>
</p>

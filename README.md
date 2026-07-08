![header](https://capsule-render.vercel.app/api?type=waving&color=gradient&customColorList=6,11,20&height=280&section=header&text=Vivek%20Reddy&fontSize=80&fontColor=fff&animation=fadeIn&fontAlignY=32&desc=Founder%20%7C%20Full-Stack%20Engineer%20%7C%20Commerce%20Apps%20%7C%20Cross-Platform%20Mobile%20%7C%20Native%20macOS%20%2F%20iOS&descAlignY=52&descAlign=50&descSize=18)

<div align="center">

[![Typing SVG](https://readme-typing-svg.demolab.com/?lines=Founder+%26+Full-Stack+Engineer;Shipped%3A+Mac+File+Organizer+%7C+Native+macOS+App;Building+Starlog+%7C+Flutter+%7C+iOS+%2B+Android;Starbundle+%7C+Shopify+Mix+%26+Match+Bundles;TypeScript+%7C+Swift+%7C+Dart+%7C+Next.js+%7C+Remix;From+blank+repo+to+shipped+product&font=Fira+Code&size=22&duration=3500&pause=1200&color=36BCF7FF&center=true&vCenter=true&width=750&height=85)](https://git.io/typing-svg)

[![LinkedIn](https://img.shields.io/badge/LinkedIn-0077B5?style=for-the-badge&logo=linkedin&logoColor=white)](https://linkedin.com/in/vivekreddy)
[![Organization](https://img.shields.io/badge/Building_under-@starlance-2ea043?style=for-the-badge&logo=github&logoColor=white)](https://github.com/starlance)
[![Location](https://img.shields.io/badge/Bengaluru-India-FF9933?style=for-the-badge&logo=googlemaps&logoColor=white)]()

</div>

---

## About Me

I'm a **founder and full-stack engineer** who takes products from a blank repo to something people actually use. In practice that means jumping across the stack in a single project — a **Shopify Cart Transform Function** one day, a **SwiftUI** view or a **Flutter** paywall the next, and a **Next.js** front end after that. Most of my work is private client and product code, so this page is built from **architectural write-ups** — the "how it's built," with diagrams — rather than open source.

<table>
<tr>
<td width="50%">

```yaml
Current Focus  : Starlog — Flutter app (iOS + Android)
Shipped        : Mac File Organizer (native macOS)
               : ReceiptScanner (iOS, on-device OCR)
In Flight      : Starbundle (Shopify commerce app)
               : HinduHub (Next.js community platform)
Languages      : TypeScript · Swift · Dart · JavaScript
Platforms      : Web · iOS · Android · macOS · Shopify
Base           : Bengaluru, India — under @starlance
Mode           : Solo founder — design → build → ship
```

</td>
<td width="50%">

**Currently Building:**
- 📱 **Starlog** — cross-platform Flutter app, subscriptions & consumable packs via RevenueCat
- 🛒 **Starbundle** — Shopify Mix & Match bundles with checkout-safe tiered discounts
- 🕉 **HinduHub** — temple & events platform computing panchang data client-side
- 🌐 Product & marketing sites for the **Starlance** studio

</td>
</tr>
</table>

---

## 🛒 Flagship Project — Starbundle

**Shopify "Mix & Match" bundles app.** Merchants define bundles with tiered discounts (*any 3 → 10%, any 5 → 20%*); shoppers pick any *N* items from configured collections; the storefront widget calculates the discount live — and, critically, the discount **survives checkout** via a Cart Transform Function instead of fragile cart attributes.

<div align="center">

[![Framework](https://img.shields.io/badge/Remix_2.16-Vite-000000?style=flat-square&logo=remix)]()
[![Admin](https://img.shields.io/badge/Polaris_12-App_Bridge-5c6ac4?style=flat-square&logo=shopify)]()
[![DB](https://img.shields.io/badge/Prisma-SQLite_%2F_Postgres-2d3748?style=flat-square&logo=prisma)]()
[![Function](https://img.shields.io/badge/Cart_Transform-Function-95bf47?style=flat-square&logo=shopify)]()
[![Widget](https://img.shields.io/badge/Theme_App-Extension-95bf47?style=flat-square&logo=shopify)]()
[![Tests](https://img.shields.io/badge/Vitest-18_passing-brightgreen?style=flat-square)]()

</div>

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

    style W fill:#95bf47,color:#fff
    style AP fill:#5c6ac4,color:#fff
    style CT fill:#ff6b6b,color:#fff
    style CO fill:#231f20,color:#fff
    style R fill:#009688,color:#fff
    style PL fill:#1f6feb,color:#fff
    style DB fill:#2d3748,color:#fff
    style ADM fill:#8957e5,color:#fff
```

<details>
<summary><b>Key engineering decisions</b></summary>

| Decision | Why it matters |
|----------|----------------|
| **One pricing brain, two runtimes** | Tier evaluation lives in `pricing.ts` (unit-tested); the Cart Transform Function can't import app code, so `pricing.js` is a deliberate, test-guarded mirror |
| **Cart Transform over cart attributes** | The discount is re-derived at checkout from the bundle definition — totals stay correct even if the shopper edits the cart |
| **App Proxy is the only door in** | Storefront widget talks to the app exclusively through HMAC-verified App Proxy routes |
| **Attribution via webhooks** | `orders/create` webhook closes the loop — views → add-to-carts → conversions per bundle |
| **Onboarding that verifies** | Polls live theme settings to confirm the storefront extension is actually enabled before declaring setup complete |

</details>

---

## 🚀 Products

### 📱 Starlog — Cross-Platform Mobile App *(current focus)*

<div align="center">

[![Flutter](https://img.shields.io/badge/Flutter-iOS_%2B_Android-02569b?style=flat-square&logo=flutter)]()
[![RevenueCat](https://img.shields.io/badge/RevenueCat-Subscriptions_%2B_Consumables-f25a5a?style=flat-square)]()
[![Status](https://img.shields.io/badge/Status-Active_Development-yellow?style=flat-square)]()

</div>

```yaml
What      : The product I'm currently building — one Dart codebase, two stores
Monetize  : Subscriptions AND consumable packs via purchases_flutter
Secrets   : --dart-define-from-file from a gitignored dart_defines.json —
            keys never touch git, local runs and CI stay clean
Ecosystem : Companion marketing site (Next.js) built alongside the app
```

---

### 🗂 Mac File Organizer — Native macOS App *(shipped)*

<div align="center">

[![SwiftUI](https://img.shields.io/badge/SwiftUI-macOS_14+-0071e3?style=flat-square&logo=swift)]()
[![Releases](https://img.shields.io/badge/Public-Releases_Channel-2ea043?style=flat-square&logo=github)](https://github.com/vivekreddy/Mac-File-Organizer-Releases)
[![Status](https://img.shields.io/badge/Status-Shipped-brightgreen?style=flat-square)]()

</div>

A **SwiftUI** macOS app that sorts a folder's files into categorized destinations by type — real-time search, drag & drop, spring animations, translucent materials, SF Symbol icons per file type. Distributed to users via a [public releases repo](https://github.com/vivekreddy/Mac-File-Organizer-Releases).

```mermaid
flowchart LR
    SRC["📁 Source folder"] --> SCAN["Scan + classify<br/>by extension"]
    SCAN --> C{"Category"}
    C --> IMG["Images"]
    C --> DOC["Documents"]
    C --> VID["Video / Audio"]
    C --> ARC["Archives"]
    C --> OTH["Other"]

    style SRC fill:#1f6feb,color:#fff
    style SCAN fill:#8957e5,color:#fff
    style C fill:#f05138,color:#fff
```

---

### 🧾 ReceiptScanner — iOS Expense Capture *(shipped)*

<div align="center">

[![Vision](https://img.shields.io/badge/Vision-On--device_OCR-000000?style=flat-square&logo=apple)]()
[![Drive](https://img.shields.io/badge/Google_Drive-Auto--filing-4285F4?style=flat-square&logo=googledrive&logoColor=white)]()
[![SwiftUI](https://img.shields.io/badge/SwiftUI-iOS-f05138?style=flat-square&logo=swift)]()

</div>

Photograph a receipt → **on-device Vision OCR** extracts store, amount & date → manual-correct sheet → files to Google Drive as `YYYY-MM-DD_Store_Amount.jpg` under `Receipts / YYYY-MM`. No data leaves the phone until upload.

```mermaid
flowchart LR
    CAM["📷 Capture / library"] --> OCR["Vision OCR<br/>on-device"]
    OCR --> EX["Extract store · amount · date"]
    EX --> ED["Manual edit sheet"]
    ED --> FN["YYYY-MM-DD_Store_Amount.jpg"]
    FN --> GD[("Google Drive<br/>Receipts / YYYY-MM")]

    style CAM fill:#8957e5,color:#fff
    style OCR fill:#000000,color:#fff
    style GD fill:#4285F4,color:#fff
```

---

### 🕉 HinduHub — Community Platform

<div align="center">

[![Next.js](https://img.shields.io/badge/Next.js-React-000000?style=flat-square&logo=nextdotjs)]()
[![Astronomy](https://img.shields.io/badge/astronomy--engine-Panchang_computation-1f6feb?style=flat-square)]()
[![TypeScript](https://img.shields.io/badge/TypeScript-Strict-3178c6?style=flat-square&logo=typescript)]()

</div>

A **Next.js** platform for Hindu temples, events, and resources — notably computing **panchang data (tithis, nakshatras) client-side** with `astronomy-engine` instead of relying on a lookup API.

---

### 🖥 This Profile, Rebuilt as an App

I rebuilt GitHub's own profile **Overview** as a pixel-faithful clone — **Next.js 16 · React 19 · Tailwind v4 · TypeScript**, with a deterministically-seeded contribution heatmap that renders identically on server and client (no hydration mismatch).

<p align="center">
  <img src="assets/portfolio.png" alt="Pixel-faithful GitHub profile clone built with Next.js 16" width="820">
</p>

---

## 📦 More Projects

| Project | Stack | What it is |
|---------|-------|------------|
| **starlance-website** | TypeScript · Next.js | Studio / product site for Starlance |
| **starlog-website** | TypeScript · Next.js | Marketing site for the Starlog app |
| **[WebLinkScan](https://github.com/vivekreddy/WebLinkScan)** | TypeScript | Crawls a site and reports broken links |
| **[dev-utility-hub](https://github.com/vivekreddy/dev-utility-hub)** | TypeScript | Collection of developer utilities |
| **shopify-currency-converter** | Liquid | Storefront currency conversion for Shopify themes |
| **cultfit-attribution / -renewals** | JavaScript | Marketing attribution & renewals analytics pipelines |

---

## 🧰 Tech Stack

<div align="center">

**Languages & Frameworks**

[![Languages](https://skillicons.dev/icons?i=ts,js,swift,dart,flutter,react,nextjs,tailwind&theme=dark&perline=8)](https://skillicons.dev)

**Backend & Data**

[![Backend](https://skillicons.dev/icons?i=remix,nodejs,prisma,postgres,sqlite,graphql,vite,vitest&theme=dark&perline=8)](https://skillicons.dev)

**Platforms & Tools**

[![Tools](https://skillicons.dev/icons?i=apple,androidstudio,git,github,vscode,netlify,vercel,figma&theme=dark&perline=8)](https://skillicons.dev)

</div>

<details>
<summary><b>Full Stack Breakdown</b></summary>

```javascript
const stack = {
  languages: ["TypeScript", "Swift", "Dart", "JavaScript"],
  web: ["Next.js 16", "React 19", "Remix 2", "Tailwind v4", "Astro"],
  mobile: ["Flutter", "SwiftUI (iOS)", "RevenueCat (purchases_flutter)"],
  desktop: ["SwiftUI (macOS 14+)", "SF Symbols", "Vision framework"],
  commerce: ["Shopify Cart Transform Functions", "Theme App Extensions",
             "App Proxy (HMAC)", "Polaris 12 + App Bridge", "Liquid"],
  data: ["Prisma", "PostgreSQL", "SQLite"],
  apis: ["Shopify Admin GraphQL", "Google Drive API", "GoogleSignIn"],
  testing: ["Vitest"],
  deployment: ["Netlify", "Vercel", "App Store", "Play Store", "Shopify App Store"],
  practices: ["Secrets via dart-define / gitignored files",
              "Deterministic seeds over hydration bugs",
              "Shared logic mirrored across runtimes, guarded by tests"],
};
```

</details>

---

## 🎯 Focus Areas

<div align="center">

```mermaid
mindmap
  root((Focus))
    Starlog Launch
      App Store
      Play Store
      RevenueCat monetization
    Commerce
      Starbundle on Shopify App Store
      Cart Transform Functions
      Theme app extensions
    Native Apps
      SwiftUI macOS
      On-device Vision OCR
    Web Platform
      HinduHub community
      Next.js 16 · React 19
    Studio
      Starlance client work
      Product & marketing sites
```

</div>

---

## 📊 GitHub Stats

<div align="center">

[![trophy](https://github-profile-trophy.vercel.app/?username=vivekreddy&theme=tokyonight&no-frame=true&no-bg=true&row=1&column=7&margin-w=10)](https://github.com/ryo-ma/github-profile-trophy)

<img src="https://github-readme-stats.vercel.app/api?username=vivekreddy&show_icons=true&theme=tokyonight&hide_border=true&include_all_commits=true&count_private=true" width="49%" alt="GitHub Stats" />
<img src="https://streak-stats.demolab.com?user=vivekreddy&theme=tokyonight&hide_border=true" width="49%" alt="GitHub Streak" />

[![Top Languages](https://github-readme-stats.vercel.app/api/top-langs/?username=vivekreddy&layout=compact&theme=tokyonight&hide_border=true&langs_count=8)](https://github.com/anuraghazra/github-readme-stats)

[![Activity Graph](https://github-readme-activity-graph.vercel.app/graph?username=vivekreddy&theme=tokyo-night&hide_border=true&area=true&custom_title=Contribution%20Activity)](https://github.com/Ashutosh00710/github-readme-activity-graph)

<picture>
  <source media="(prefers-color-scheme: dark)" srcset="https://raw.githubusercontent.com/vivekreddy/vivekreddy/output/github-snake-dark.svg" />
  <source media="(prefers-color-scheme: light)" srcset="https://raw.githubusercontent.com/vivekreddy/vivekreddy/output/github-snake.svg" />
  <img alt="github-snake" src="https://raw.githubusercontent.com/vivekreddy/vivekreddy/output/github-snake.svg" />
</picture>

<sub>Most of my work is in private repos — public language stats under-count Swift, Dart, and Liquid.</sub>

</div>

---

## ✅ Goals

- [x] Ship **Mac File Organizer** — native macOS app with a public releases channel
- [x] Ship **ReceiptScanner** — on-device OCR receipt filing for iOS
- [x] Build **Starbundle v1** — Shopify Mix & Match bundles (18 tests passing)
- [x] Build **HinduHub** — panchang-aware community platform
- [x] Rebuild GitHub's profile UI as a pixel-faithful **Next.js 16** clone
- [ ] Launch **Starlog** on the App Store & Play Store
- [ ] Launch **Starbundle** on the Shopify App Store
- [ ] **Starbundle v2** — classic bundles, subscriptions, A/B testing

---

## Philosophy

> *"Building things that ship — a product isn't done until users have it."*

| Principle | Practice |
|-----------|----------|
| **Ship it** | Every project targets a store, a release channel, or production — not a demo folder |
| **One brain, many runtimes** | Shared logic (like bundle pricing) mirrored across runtimes, guarded by the same tests |
| **No fragile hacks** | Cart Transform over cart attributes · deterministic seeds over hydration bugs |
| **Secrets stay out of git** | `--dart-define-from-file`, gitignored key files, clean CI |
| **On-device first** | Vision OCR before cloud OCR — data leaves the phone only when the user says so |

---

<div align="center">

**Let's build something.**

[![LinkedIn](https://img.shields.io/badge/Connect_on-LinkedIn-0077B5?style=for-the-badge&logo=linkedin&logoColor=white)](https://linkedin.com/in/vivekreddy)

![footer](https://capsule-render.vercel.app/api?type=waving&color=gradient&customColorList=6,11,20&height=120&section=footer)

</div>

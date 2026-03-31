# LeadFabric LP Implementation Plan

> **For Claude:** REQUIRED SUB-SKILL: Use superpowers:executing-plans to implement this plan task-by-task.

**Goal:** Build a single-file dark-mode LP (`index.html`) for LeadFabric that recruits 3 PoC partner companies via a Google Form CTA.

**Architecture:** Pure static HTML file with embedded CSS and minimal vanilla JS. No framework, no build step, no external dependencies except optional Google Fonts. All 10 sections are in one file, pre-approved by the product owner.

**Tech Stack:** HTML5, CSS custom properties, vanilla JS (scroll animation only), deployed to `/Users/kacky/Desktop/Claude/LP/index.html`

---

## Design Token Reference

```
--bg:        #0a0e1a   (main background)
--bg2:       #0f1628   (alternate section background)
--bg3:       #151d35   (card background)
--accent:    #3d6bff   (primary blue)
--accent2:   #6b4fff   (purple gradient end)
--green:     #00d48a   (success / checkmark)
--text:      #e8ecf5   (body text)
--muted:     #8892aa   (subdued text)
--border:    rgba(255,255,255,0.08)
--card:      rgba(255,255,255,0.04)

Font stack: 'Hiragino Kaku Gothic ProN', 'Hiragino Sans', 'Noto Sans JP', sans-serif
```

---

## Task 1: File scaffold + CSS variables + Nav

**File:** `Create: /Users/kacky/Desktop/Claude/LP/index.html`

**Step 1: Invoke the frontend-design skill**

Use `superpowers:frontend-design` (or `frontend-design:frontend-design`) with the following spec. The skill handles all creative decisions.

**Step 2: Write the full HTML structure**

Produce the complete `index.html` covering all 10 sections below. Overwrite the existing file.

**Section specs:**

### Section 1 — `<nav>` (fixed, backdrop-blur)
```
Left:   dot-grid SVG logo  +  "Lead Fabric" (bold, gradient text)  +  "DATA CLEANSING FOR B2B" (tiny muted)
Center: anchor links → 課題 / ソリューション / PoC募集  (hidden on mobile)
Right:  <a href="YOUR_GOOGLE_FORM_URL"> primary button "PoC申込はこちら →"
Style:  position:fixed; backdrop-filter:blur(16px); border-bottom: 1px solid var(--border)
```

### Section 2 — Hero (`<section class="hero">`)
```
Badge:   animated pulsing dot  +  "3社限定 · 無償PoC募集中"
H1:      「リード情報の汚さが、
           CRM全体を壊している。」
         font-size: clamp(36px, 6vw, 68px); font-weight: 800; letter-spacing: -2px
         "CRM全体" → gradient highlight (#3d6bff → #6b4fff)
Sub:     「展示会・セミナーで獲得したリードデータを、エンジニア不要でMAやCRMに
           渡せる状態に自動変換。B2BマーケターとCRMOpsのためのリードクレンジングSaaS。」
Buttons: Primary "無償PoCに申し込む →"  |  Outline "LeadFabricとは？"
Note:    "完全無償 · 3社限定 · NDA締結の上でご提供"  (muted, small)
BG:      radial-gradient glow behind headline (blue, subtle)
```

### Section 3 — 課題 (`<section id="problem">`)
```
Label:   PROBLEM
H2:      「こんな状況、ありませんか？」
Grid:    5 cards (3+2 layout on desktop, 1 col on mobile)
Each card has: red-tinted icon box (emoji) + bold title + 2-line description

Cards:
1. 🗂️ 「展示会後のデータ加工が、毎回手作業」
   展示会・セミナーのたびにExcelでの突合作業が発生。マーケターの時間が奪われ続ける。

2. 👨‍💻 「エンジニアに頼まないと、一歩も前に進めない」
   CSVの加工・フォーマット変換・CRMへのインポート設定、すべてに開発リソースが必要。

3. 💔 「データが汚くて、CRMが誰にも使われない」
   「株式会社ABC」と「ABC（株）」が別レコードに。重複・表記揺れだらけで誰も信用しない。

4. 😤 「インサイドセールスが、CRMに入力しない」
   汚いデータを見て「どうせ使えない」とモチベーションが下がり、活動履歴が残らない。

5. 📊 「マーケ投資のROIを、経営に説明できない」
   データが整っていないため、施策の貢献度が可視化できず、予算獲得に苦労する。

Hover effect: border-color shifts to rgba(255,80,80,0.3); background shifts to rgba(255,80,80,0.04)
```

### Section 4 — 根本原因 (`<section id="rootcause">`)
```
BG: var(--bg2)
Label: ROOT CAUSE
H2: 「問題の根本は、リード情報の"上流"にある」

Cascade flow diagram (horizontal on desktop, vertical on mobile):
[マーケティング（上流）] --×破綻--> [インサイド/営業（中流）] --×破綻--> [CRM/経営（下流）]

Under each node, a 1-line description:
- マーケ: 「リードCSVの品質が低いまま共有」
- インサイド: 「汚いデータに基づいてフォロー、履歴を入力しない」
- CRM/経営: 「運用されないCRM、見えないROI」

Arrow style: red dashed with ✕ icon
Body text (2-3 lines): 「CRMを正しく運用するには、データが入る前の段階を正しくする必要があります。
上流のリード情報が整っていなければ、どれだけCRMを改善しても根本解決にはなりません。」
```

### Section 5 — ソリューション (`<section id="solution">`)
```
Label: SOLUTION
H2: 「LeadFabricが、上流を自動で整える」

Flow diagram:
[CSV入力] → [LeadFabric 自動クレンジング] → [MA / CRM ready]

Left node "CSV入力":
  - 展示会 / セミナー / ホワイトペーパー / 名刺

Center node "LeadFabric" (highlighted, larger):
  - 会社名正規化
  - 名寄せ・重複検知
  - 役職・部門コード付与
  - 業種・規模コード付与
  Style: gradient border, slightly larger box

Right node "MA / CRM ready":
  - Marketo互換CSV
  - インポート即可能

3 value pills below:
✦ エンジニア不要   ✦ 高速変換   ✦ MA・CRM連携対応
```

### Section 6 — 機能 (`<section id="features">`)
```
BG: var(--bg2)
Label: FEATURES
H2: 「正規化エンジンの機能」

4 cards (2×2 grid):

1. 🏢 会社名正規化・名寄せ
   「株式会社」「㈱」「(株)」などの表記揺れを統一。同一企業の重複レコードをグループ化し、デdup_group_idを付与。

2. 👤 役職・部門コードの自動付与
   「部長」「General Manager」など多様な表記をL1〜L6の役職コードに統一。部門もSALES・MKT・ENGなどのコードに変換。

3. 🏭 業種・企業規模の自動判定
   企業情報から業種コードと規模コード（ENT/MID/SMB）を自動付与。セグメント分析・スコアリングの精度が上がる。

4. 📤 Marketo互換CSVエクスポート
   UTF-8 BOM付き・26列フォーマットでMarketo直接インポート対応。エンジニア不要でMAに取り込み可能。

Each card: bg-3 background, hover border-color shifts to rgba(61,107,255,0.3)
```

### Section 7 — PoCオファー (`<section id="poc">`)
```
Label: LIMITED OFFER
H2: 「3社限定、完全無償でご提供します」
Sub: 「プロダクトを一緒に磨いてくれるパートナー企業を探しています。」

2-column layout:
Left — 「LeadFabricが提供すること」(green checkmarks):
  ✓ LeadFabricの全機能を無償で提供
  ✓ セットアップ・初期設定を個別サポート
  ✓ 導入後のフォローアップ対応
  ✓ 正式リリース時の優先プラン案内

Right — 「お願いしたいこと」(blue bullets):
  → 実際のリードCSVデータでの検証
  → 月1回・30〜60分のフィードバックヒアリング
  → UX・機能に関するご意見の共有
  → NDA締結（秘密保持契約）への同意

Bottom badge: "残り募集枠 3社" (large, highlighted, with countdown feel)
```

### Section 8 — FAQ (`<section id="faq">`)
```
BG: var(--bg2)
Label: FAQ
H2: 「よくある質問」

4 accordion items (click to expand, JS toggle):

Q1: 費用はかかりますか？
A1: PoC期間中は完全無償でご利用いただけます。正式リリース後の価格については、PoC参加企業には優先的にご案内いたします。

Q2: どんなCSV形式に対応していますか？
A2: 展示会・セミナー・ホワイトペーパーダウンロード・Sansanなど、任意のCSVフォーマットに対応しています。フィールドマッピングはAIが自動で行います。

Q3: 導入に何が必要ですか？
A3: ブラウザのみです。インストールは不要で、エンジニアリソースなしでご利用いただけます。

Q4: いつから利用できますか？
A4: 申込後、最短1週間以内にご利用開始いただけます。初回は個別にセットアップサポートをご提供します。
```

### Section 9 — 最終CTA (`<section id="contact">`)
```
BG: gradient overlay on --bg
H2: 「まず、話を聞いてみませんか。」
Sub: 「3社限定の無償PoCです。ご興味のある方は、まずお気軽にフォームからご連絡ください。」
Button (large): "Googleフォームで申し込む →"  href="YOUR_GOOGLE_FORM_URL"
Note (muted): "残り3社 · 完全無償 · NDA締結の上でご提供 · ご質問もお気軽に"
```

### Section 10 — Footer
```
LeadFabric dot-grid logo + name
Tagline: "DATA CLEANSING FOR B2B"
Copyright: © 2026 LeadFabric. All rights reserved.
[Company name placeholder]
```

**Step 3: Add scroll-reveal JS (minimal)**

```html
<script>
  // Intersection Observer for fade-in-up on scroll
  const observer = new IntersectionObserver((entries) => {
    entries.forEach(e => {
      if (e.isIntersecting) {
        e.target.classList.add('visible');
        observer.unobserve(e.target);
      }
    });
  }, { threshold: 0.1 });
  document.querySelectorAll('.reveal').forEach(el => observer.observe(el));

  // FAQ accordion
  document.querySelectorAll('.faq-item').forEach(item => {
    item.querySelector('.faq-q').addEventListener('click', () => {
      item.classList.toggle('open');
    });
  });
</script>
```

CSS for reveal:
```css
.reveal { opacity: 0; transform: translateY(24px); transition: opacity 0.5s ease, transform 0.5s ease; }
.reveal.visible { opacity: 1; transform: none; }
```

**Step 4: Verify in browser**

Open `http://localhost:3000/` and scroll through all 10 sections. Check:
- [ ] Nav is fixed and readable over all section backgrounds
- [ ] Hero badge pulses
- [ ] Problem cards have red hover effect
- [ ] Root cause flow diagram renders correctly
- [ ] Solution flow diagram renders correctly
- [ ] PoC offer 2-col layout is clear
- [ ] FAQ accordion opens/closes
- [ ] All CTA buttons point to `YOUR_GOOGLE_FORM_URL`
- [ ] Mobile layout at 375px width looks correct (use browser DevTools)

**Step 5: Replace Google Form placeholder**

When the actual Google Form URL is ready, replace all instances of `YOUR_GOOGLE_FORM_URL` in the file.

```bash
# Find all occurrences
grep -n "YOUR_GOOGLE_FORM_URL" /Users/kacky/Desktop/Claude/LP/index.html
```

---

## Dot-Grid SVG Logo Reference

Use this inline SVG for the LeadFabric logo (matches the product app):

```svg
<svg width="32" height="32" viewBox="0 0 32 32" fill="none">
  <!-- 4x4 dot grid with connecting lines forming a diamond/network pattern -->
  <g fill="currentColor" opacity="0.9">
    <circle cx="4" cy="4" r="1.5"/>
    <circle cx="12" cy="4" r="1.5"/>
    <circle cx="20" cy="4" r="1.5"/>
    <circle cx="28" cy="4" r="1.5"/>
    <circle cx="4" cy="12" r="1.5"/>
    <circle cx="12" cy="12" r="2"/>
    <circle cx="20" cy="12" r="2"/>
    <circle cx="28" cy="12" r="1.5"/>
    <circle cx="4" cy="20" r="1.5"/>
    <circle cx="12" cy="20" r="2"/>
    <circle cx="20" cy="20" r="2"/>
    <circle cx="28" cy="20" r="1.5"/>
    <circle cx="4" cy="28" r="1.5"/>
    <circle cx="12" cy="28" r="1.5"/>
    <circle cx="20" cy="28" r="1.5"/>
    <circle cx="28" cy="28" r="1.5"/>
  </g>
  <g stroke="currentColor" stroke-width="1" opacity="0.4">
    <line x1="4" y1="4" x2="28" y2="28"/>
    <line x1="28" y1="4" x2="4" y2="28"/>
    <line x1="16" y1="4" x2="16" y2="28"/>
    <line x1="4" y1="16" x2="28" y2="16"/>
  </g>
</svg>
```

---

## Responsive Breakpoints

```css
/* Mobile first */
@media (max-width: 768px) {
  nav .nav-links { display: none; }
  .hero h1 { font-size: 36px; }
  .problem-grid { grid-template-columns: 1fr; }
  .features-grid { grid-template-columns: 1fr; }
  .poc-grid { grid-template-columns: 1fr; }
  .flow-diagram { flex-direction: column; }
  .flow-arrow { transform: rotate(90deg); }
}
```

---

## Checklist Before Done

- [ ] All 10 sections present and readable
- [ ] No placeholder text other than `YOUR_GOOGLE_FORM_URL`
- [ ] Dark background, white text, blue accent consistent throughout
- [ ] Hover effects on cards
- [ ] FAQ accordion works
- [ ] Scroll reveal works
- [ ] Nav links anchor-scroll to correct sections
- [ ] Mobile layout passes 375px check
- [ ] LeadFabric logo visually matches the product app

---

## File Location

```
/Users/kacky/Desktop/Claude/LP/index.html   ← overwrite this
```

---
name: WUJI Paper-to-Web
developer: Wenji Li
version: 1.0.0-local-review
audience: WUJI internal and explicitly authorized collaborators
status: local review; not published
reference: DMA Paper v2, approved through 2026-11-25
source_of_values: tokens/tokens.css
fonts: tokens/fonts.css
preview: reference/index.html
starter: starter/index.html
primary: "#207FFF"
canvas: "#FFFFFF"
brand_surface: "#0C0C0C"
media_surface: "#F4F4F4"
frame_radius: 4px
reading_width: 720px
reference_viewport: 1440x900
---

# WUJI Paper-to-Web Design System

**Developer: Wenji Li**

A restrained research interface: clear claims, visible evidence, readable typography and purposeful interactions. Preserve the distinction between research content and UI. Readers should understand the contribution before they need to decode the method.

本规范用于 WUJI 论文网站。以最终 DMA v2 为基准，但不要求每篇论文复制 DMA 的研究结构。本文为核心规则；详细使用方式见 docs/，实际数值由 tokens/tokens.css 管理。内部评审阶段，不创建公开仓库、不发布网站、不设置伪密码页。

## 1. How to use / 人与 AI 的使用顺序

1. Read this file and docs/content-workflow.md before designing the page.
2. Inspect tokens/tokens.css and reference/index.html for exact appearance and behavior.
3. Gather the paper content using docs/paper-input-template.md. Never invent claims, data, authors or links.
4. Copy the whole package for a new project; implement inside starter/ while retaining relative token/font/asset paths, or adjust those paths explicitly.
5. Select components by information type. Implement the mapping between modes, media, timestamps and results.
6. Run the checks in docs/acceptance.md. A working hover state is not evidence that a content filter is implemented.

MUST = required. SHOULD = preferred default; record reasons for deviations. MAY = optional based on content. White-model labels and synthetic values MUST be removed or replaced before production. Follow explicit project/user requirements if they override defaults; document the exception.

## 2. Brand principles

- Evidence first: each claim has an adjacent demonstration, measurement or precise explanation.
- Quiet structure: black/white/gray surfaces; one interaction blue. No decorative gradients, glass effects or drop shadows on the page chrome.
- Deliberate typography: Algorytm Mono for display/technical hierarchy, Geist for explanatory text.
- Stable reading: switching modes must not unexpectedly move the chart origin or step labels.
- Useful motion: demonstrate sequence, direction, progress or correspondence. Do not animate merely to appear technical.
- Reader control: preserve keyboard focus, stop offscreen video work, respect reduced motion and autoplay failure.

## 3. Content architecture

Hero → Motivation → Demonstrations → Dataset (optional) → Method → Results → Citation.
Numbers and labels follow the actual paper, not fixed DMA numbering. Navigation and anchors MUST match rendered sections. Do not add a dataset or simulation section if the paper does not contain it.

Hero: title, authors, affiliation, concise abstract, paper/code/citation entry points, optional overview video. Motivation: problem and gap. Demonstrations: capabilities with conditions. Method: inputs, transformations, outputs. Results: data, units, sample counts, uncertainty and evaluation protocol. Citation: exact approved BibTeX.

## 4. Foundations / tokens

### Color

| Role | Value | Rule |
|---|---|---|
| Canvas / body ink | #FFFFFF / #0E0E0E | Main page |
| Brand surfaces | #0C0C0C | Menu, hero, footer |
| Dark captions | #0B0B0B | Media and controls |
| Media/chart/inner wells | #F4F4F4 | Neutral evidence areas |
| Method outer panels | #E7E7E7 | Hierarchy, not decoration |
| Results lower controls | #EDEDED | Separate from chart |
| Citation | #353535 | White regular text |
| Interaction | #207FFF | All new selected/progress/focus roles |
| Own series / comparison | #527DB2 / #AAAAAA | Data encoding, not interaction state |

DMA historically used #288BFF in some interactions. This new system unifies those interaction roles to #207FFF. Do not silently edit the original DMA project. Multiple semantic CSS aliases can share the single value. Scientific color encodings MAY differ, with a legend.

### Alpha

Use color alpha, not container opacity. On dark: primary 100%, authors 80%, secondary/unselected 60%, quiet object list 40%. On white: secondary labels 60%, nav rails 40%. Chapter 01/03 in DMA used black70%, chapter04 black100%: these are DMA-specific choices, not mandatory meanings of chapter numbers.
Navigation hover uses action blue with unchanged 60% text / 40% rail alpha. Selected metrics use black100% text and blue rail. Low-alpha text is intended for secondary roles, not essential long-form reading; review contrast in the final context.

### Typography

| Role | Family | Desktop size / line | Weight |
|---|---|---|---|
| Hero title | Algorytm Mono | 36 / 54px | 400, strong 700 |
| Authors | Algorytm Mono | 12 / 18px | 300 |
| Abstract | Geist | 16 / 20px | 400 |
| Body | Geist | 16 / 24px | 400 |
| Chapter label | Algorytm Mono | 20 / 25px | 400 |
| Chapter title | Algorytm Mono | 24 / 30px | 500–600 by emphasis |
| Level title | Algorytm Mono | 16 / 24px | 600 |
| Four-card title | Algorytm Mono | 14 / 17.5px | 500 |
| Step text | Algorytm Mono | 12 / 20px | 400 |
| Navigation option | Algorytm Mono | 12 / 18px | 400 |
| Results title / description | Algorytm Mono / Geist | 16 / 22.4px; 14 / 21px | 500 / 400 |
| BibTeX | Geist | 16 / 20px | 400 |

CSS family alias is `WUJI Algorytm Mono`. Local files spell the name `AlgorytmMonoTRIAL`; preserve accurate metadata. Bundled TRIAL OTFs are explicitly marked review assets. Use Geist Mono as fallback. Do not assume the reviewer has the font installed. See assets/fonts/README.md for replacement.

### Layout

1440px baseline: content720px, left/right360px; menu60px; wide hero video max1200px. Main sections120px apart. Hero top160px. **Hero action row to video gap80px desktop/tablet;52px mobile**, including the approved +20px revision. Main frame captions32px top /40px horizontal /40px bottom; compact mobile24/20/24. External frame corners4px; adjoining internal edges square. Controls may retain3px corners; square action buttons are allowed.

02-style three-column anchor navigation: equal tracks206px and gaps51px at720px content width. Desktop long labels may occupy the gap without moving tracks only when they do not overlap the next label. Mobile wraps. Never force arbitrary future paper titles into no-wrap without testing.

## 5. Components

See docs/components.md and eight SVG diagrams in components/anatomy/. SVG diagrams explain structure; they are NOT interactive production components.

- Media single: explicit ratio, optional caption, load/error state.
- Comparison: paired evidence with matched size and aligned captions.
- Video steps: currentTime-based progress, timestamp seeking and label stability.
- Sequence grid: four equal cards,14px titles, each timeline scoped to its own video.
- Dataset: source/reference pair, skills and statistics; no arbitrary changes to actual data.
- Method: semantic nodes and edges, brief details, controlled motion.
- Results: category/header, chart, then subset and metric controls in a vertical stack.
- Citation: readable selectable text with copy and fallback.

## 6. State and interaction

Default / hover / selected / pressed / focus-visible / disabled / loading / error are distinct states. Persist selection in state and aria-pressed (or full accessible tab semantics). Hover MUST NOT change the selected data. Do not use the mouse as the only means of access.

Results category selected: action-blue background + black text. Hover, including selected: white background + black text; pointer exit restores selection. Results lower metric: action-blue top rail + black100% text. Action buttons: contrast reversal, ~450ms acknowledgement; actions do not stay selected.

Step rail4px; label12/20px; left inset16px; min-height56px. Hover step: #555 background + white text. Progress derives from video playback; manual clock animation is allowed ONLY in a clearly marked white-model demo. Timestamp order and duration bounds MUST be validated. Loop and seeks reset progress correctly.

Only overview video keeps native controls by default. Supporting clips are muted, inline and looping; pause offscreen/in hidden tabs. For reduced motion or autoplay failure, offer an intentional way to start supporting media rather than silently leaving inaccessible stills. No always-on square play overlay is required. See docs/interactions.md.

## 7. Results chart standard

A stable top inset is mandatory: whole bar and line chart blocks start32px from the chart frame top (24px small screen), with no fake legend spacer over bars. Chart viewport490px desktop,650px ≤740px with contained scrolling if required. Header text area172px desktop,216px small screen; long content MAY grow rather than clip.
Data bars are square-ended; track#E1E1E1, own series#527DB2, baseline#AAAAAA. Own row highlight#E7E7E7. Show unit, value and uncertainty separately. Missing data is “Not reported” or “—”, never zero. Values must correspond to chosen category/subset/metric. Do not derive unseen values from seen values or fabricate error ranges.
Bottom toolbar is natural height; subset buttons ABOVE metric rails. Do not force equal height where content differs. Charts need text labels and accessible descriptions; colors alone cannot identify series. Line charts use real x-axis units and keyboard-accessible data readout when interactive.

## 8. Responsive

| Width | Rule |
|---|---|
| 1920 | 720px reading width;1200px max hero; generous outer space |
| 1440 | Baseline |
| 1280 | Reading width720px; hero width viewport−80px |
| 768 | Reading width720px; wide maps scroll inside their container |
| ≤767 | Reading width viewport−40px; hero28px; chapter20px; collapsed menu; anchor labels wrap |
| ≤740 | Chart height650px; error rows may stack |
| ≤600 | Category buttons two columns; header216px minimum |

80px mobile chapter gap is a normalized new-template default, not a claim that every historical DMA mobile gap was80px. Use actual reflow, not a scaled1440px screenshot. Avoid whole-page horizontal overflow; deliberate component scrolling is permitted.

## 9. Icons and identity

New common icon set:24×24 viewBox,1.5px stroke,currentColor; display16/20/24px. Icons inside buttons inherit text state. Provide accessible names for icon-only controls. This is a replaceable v1 proposal, not a claim that every old DMA icon had identical geometry. Four-pixel radius applies to frame edges, not every icon path.
Provided WUJI identity: transparent white PNG,1876×536. Keep native ratio; CSS brightness(0) may display black on light surfaces. Do not stretch, trace into an invented SVG or add gradients. DMA marks live in examples/dma/ and MUST NOT become the default WUJI logo. Formal minimum clearspace was not supplied; preview sizing is implementation guidance, not an approved brand manual.

## 10. Production boundary and delivery

The reference demonstrates states, not scientific evidence. The starter has synthetic data, placeholder media and simple relationships. AI MUST adapt material mapping, timestamps, subset/metric data and performance to the paper. Filling all blank URLs or enabling a filter is not a reason to invent values.

No password or identity system is implemented in this local package. A future private repository and protected website require separate server/platform access controls; a JavaScript password overlay is not protection. Authorized user review happens before publishing.

Production checklist: docs/acceptance.md. Copy/serve all dependencies, use HTTPS and correct media MIME types, support Range/206 for video seeking. Formal font replacement, real links, real materials and data approval are explicit production tasks.

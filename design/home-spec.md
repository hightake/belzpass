# BelzPass — Home page spec (from Figma)

Source: Figma file `6578GNItimABGeHKccRcL6`, page "עיצוב רספונסיבי", frame **דף הבית** (node `1114:5595`), desktop width 1280px (hero/footer backgrounds 1650px, centered).
Extracted: 2026-11-02 via Figma MCP (`get_design_context`).

> **Note (confirmed by owner, 2026-11-02):** the home page *is* the apartments directory ("מאגרי דירות"). There is no separate listings page — the nav link "מאגרי דירות" should point to the home page (or scroll to the cards grid).

## Design tokens

### Colors
| Token | Value | Used for |
|---|---|---|
| `ink` | `#1B1C1C` | Main text, dark sections (footer, popup), dark buttons, card border |
| `paper` | `#F4F4F4` | Page background, light text on dark, card background |
| `gold` | `#B7B275` | Primary CTA buttons ("שליחה", "לפרסום הדירה שלך", "לתשלום עבור העסקה", "שלח") |
| `white` | `#FFFFFF` | Popup base |
| overlay | `rgba(244,244,244,0.9)` | Top nav bar background |
| overlay | `rgba(244,244,244,0.2)` | Hero image tint |
| overlay | `rgba(0,0,0,0.7)` | Modal backdrop |

Gradients:
- Footer bg: `linear-gradient(179.8deg, #1B1C1C 3%, rgba(27,28,28,0.2) 53.7%, #1B1C1C 110%)` over photo at 15% opacity
- "Add apartment" section bg: `linear-gradient(177.7deg, rgba(244,244,244,.9) 2.6%, rgba(244,244,244,0) 45.2%, rgba(244,244,244,.9) 71.7%)` over photo at 15% opacity
- Payment popup: `linear-gradient(180.5deg, rgba(27,28,28,0) 7.8%, rgba(27,28,28,.43) 16%, rgba(27,28,28,.7) 27.6%, #1B1C1C 81.2%)` over photo at 70% opacity

### Fonts (all must be licensed + self-hosted — Hebrew commercial fonts)
| Family | Weights used | Role |
|---|---|---|
| **BA Ushpizin** | Regular, Bold | Display titles (hero 137px Bold, section titles 120px, popup 164px Bold) |
| **Fb Booster** | Regular, Medium, Bold | Body, nav, buttons, subtitles |
| **Leon** | Product Regular | Small notes/badges (12px) |

### Named text styles (Figma styles)
| Style name | Font | Size / line-height / tracking |
|---|---|---|
| רץ וכפתורים (body & buttons) | Fb Booster Regular | 20 / 18 / 0 |
| הערות (notes) | Leon Product Regular | 12 / 18 / 0 |
| אזור (section title) | BA Ushpizin Regular | 120 / 100% / 0 |
| משנה (subtitle) | Fb Booster Medium | 40 / 100% / 2% (0.8px) |

### Radii
- Pills/buttons: `50px` (fully rounded); big CTA `164px`
- Apartment card: `49px`, border `2px #1B1C1C`
- Popup: `55.5px`
- Checkbox: `5px`

## Page structure (top → bottom, RTL)

1. **Top nav** — 120px tall, `rgba(244,244,244,.9)`, sticky-looking. Logo center-right. Links (right→left): בית · מאגרי דירות · הוספת דירה · תשלום · אודות · הזמנת אוכל · הסבר · תמיכה טכנית. Language/"עבר" toggle on far right; two round 48px icon buttons on far left.
2. **Hero** — full-width photo (Belz synagogue) with light tint.
   - Top-right decorative tag: "א בעלזער תנועה" (BA Ushpizin 30px) on a notched shape.
   - Top-left: horizontal row of **holiday filter chips** (round icons + label): שבת סליחות · תשרי · ראש השנה · יום כיפור · סוכות · שמחת תורה.
   - Title (centered, BA Ushpizin Bold 137px): **"אזוי קומט מען היינט קיין בעלזא"**.
   - **Search/filter bar** (1010px wide, notched pill shape): icon dropdowns (right→left) — dates (time-and-date), beds, open-door (rooms), location, stairs (floor), arrows (size), and an "AI" icon with a "בקרוב" (coming soon) badge.
3. **Apartment cards grid** — 2 columns × 2 rows shown (cards 490×707).
   Card: rounded 49px, 2px ink border, paper bg. Photo occupies top ~70% (flipped). Price pill top-left: "החל מ" + **4,350** with ₪ icon (dark pill, Fb Booster 33px). Heart/favorite icon. Vertical strip on left with feature icons + numeric badges: beds 20, rooms 5, floor 3, size 5, location "מנחת יצחק". Title "פנטהאוז חלומי" (Fb Booster 38px) + short description (13px). Full-width dark button **"להזמנה"** (Fb Booster 43px, tracking 3px).
4. **"הוספת דירה להשכרה"** section — title (BA Ushpizin 120px), subtitle "אז איך זה עובד תכלס?" (40px Medium).
   Three steps, each: 180px dark circle with icon + big number, title (40px Medium), text (20px), and a gold CTA **"לפרסום הדירה שלך"**:
   1. **מעלים את התמונות** — "גוררים את התמונות הרלוונטיות של הדירה ומעלים אותן בקלות."
   2. **מספרים לנו על הדירה** — "מסמנים מה הדירה כוללת ומוסיפים את הפרטים החשובים – חדרים, מיטות, אבזור וכל מה שחשוב לאורחים לדעת."
   3. **מפרסמים ומתחילים להשכיר** — "הדירה שלכם מופיעה באתר, בדיוק מול האנשים שיכולים למצוא אותה בקלות ולהגיע אליכם."
   ⚠ Designer note in the frame: **animation reference — https://reactbits.dev/components/flying-posters** (red link "קישור לאנימציה").
5. **Footer / support** (dark, 1097px tall):
   - Title "תמיכה טכנית" (BA Ushpizin 120px), subtitle "יש לכם שאלה? רעיון לשיפור? אנחנו כאן בשביל לשמוע".
   - Contact form: fields שם · טלפון · מייל (pill inputs, white border), consent checkbox "אני מאשר את **מדיניות הפרטיות** ואת **תקנון האתר**", buttons **שליחה** (gold) / **ביטול** (outline).
   - Nav links row repeated (same as header) with logo.
   - Newsletter: "רוצה להתעדכן כשעולה דירה חדשה או סתם כשאנחנו משתדרגים?" + small pills: שם · מייל · מה אתה מחפש? · **שלח** (gold).
   - Legal links: מדיניות פרטיות · תנאי שימוש · הצהרת נגישות · נוהל האתר.
   - Credit line: "UX \ UI BY: SCHWIMMER   DEVELOPE BY: HIGHTAKE".
6. **Payment reminder popup** (overlaid in the design, modal state): 1090×725, rounded 55px, photo + dark gradient, close (X) top-left.
   - Title "ביומו תתן שכרו" (BA Ushpizin Bold 164px)
   - "סגרתם עסקה דרך המאגר? מזכירים לכם לבצע תשלום סמלי **בסך 25 ש״ח**" (44px)
   - Gold CTA **"לתשלום עבור העסקה"**.

## Wide desktop version — frame "דף הבית דוגמא" (node `835:7165`), 1650 × 6498

Primary desktop layout (no popup). Figma returned structure only (frame too large for full code), so exact styles come from the narrow version above — same tokens and components. Differences vs. the 1280px version:

| Area | Wide (1650) | Narrow (1280) |
|---|---|---|
| Nav | `Frame 33` component, 90px tall, full width | 120px bar |
| **Marquee strip** (new) | 29px strip right under the nav, repeating "האתר בהרצה" with small dot separators — scrolling ticker | — |
| Hero title | One line, 1410px wide, y≈416 | Two lines, 802px wide |
| Holiday chips | **Vertical column** of 54px circles on the left edge (x≈19, y 171–548), 10px gap: שבת שובה · ראש השנה · תשרי · יום כיפור · שמחת תורה · סוכות | Horizontal row |
| Search bar | 1290px notched shape, icons 60px with 80px gaps (right→left): dates · beds · rooms · location · floor · size · ₪/price(?) · AI "בקרוב" | 1010px |
| Card grid | **3 columns × 2 rows** (6 cards, 490×707, ~30px gutter, rows at y=840 and y=1577) | 2 × 2 |
| Add-apartment steps | Circles on the right (x≈1350), text right-aligned to them, **one** gold CTA "לפרסום הדירה שלך" at left (y≈3210) | CTA under every step |
| **"אודות המאגר"** (new section, y≈4784) | Title + paragraph inside a hand-drawn frame (two vectors), see text below | — |
| Footer | `Component 1`, same as narrow version | same |

"אודות המאגר" text:
> מגיעים לבעלזא לחג? מצוין. עכשיו נשאר רק למצוא איפה ישנים. במקום לעבור בין קבוצות, לשאול "מישהו יודע על דירה?" ולקבל 17 תשובות של "תנסה אצל..." — ריכזנו לכם במקום אחד דירות זמינות בקרית בעלזא, עם תמונות, פרטים וכל מה שצריך כדי להבין אם זה המקום שלכם. ובעלי הדירות? גם אתם יכולים לנשום. כמה תמונות, כמה פרטים — והדירה שלכם כבר מול מי שמחפש. כי ההכנות לחג מספיק מורכבות גם ככה. את הדירה לפחות אפשר למצוא בקלות.

Inconsistency to confirm: first holiday chip is **"שבת שובה"** here vs **"שבת סליחות"** in the narrow frame.

Node IDs for later detailed extraction (if Figma quota allows): nav `835:7339`, marquee `835:7341`, chips `835:7233`, search bar `835:7176`, card `835:7271`, steps `835:7279`/`835:7317`, about text `835:7330`, footer `835:7336`.

## Business logic hints visible in the design
- Holiday-based browsing (chips) is first-class.
- Filters: dates, beds, rooms, floor, size, location; AI search "coming soon".
- Advertiser flow: upload photos → details/amenities → publish.
- Post-deal **25 ₪ symbolic payment** reminder popup.
- Food ordering ("הזמנת אוכל") link in nav — external or future feature?

## Assets — NOT yet downloaded
The design references ~60 images/SVG icons (logo, hero photo, card photo, icons: bed, door, stairs, location, arrows, time-and-date, ai-technology, down-arrow, holiday icons, ₪ icon, heart, close). The temporary MCP download links expire after 7 days and could not be fetched from this environment.
**Export them manually from Figma** (select → Export → SVG for icons/logo, PNG/JPG 2x for photos) into `design/assets/`.

## Not yet extracted
- Mobile frame of the home page, other pages (listing page, add-apartment flow, payment, about, etc.), hover/empty/error states.
- Screenshot PNG of this frame (export manually: select frame → Export PNG 1x/2x → `design/screens/home-desktop.png`).

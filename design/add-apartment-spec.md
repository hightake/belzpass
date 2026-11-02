# BelzPass — Add / view apartment spec (from Figma)

Source: Figma file `6578GNItimABGeHKccRcL6`, frame **הוספת דירה למאגר** (node `835:8300`), desktop width 1280px (footer 1650px, centered).
Extracted: 2026-11-02 via Figma MCP (`get_design_context`). Low-res preview: [`screens/add-apartment-1280-preview.png`](screens/add-apartment-1280-preview.png) (360×1024 — export a full-size PNG manually).

The same layout serves two modes: **add** (empty form, upload placeholders) and **view** (the published apartment). Confirm with the designer whether "view" has any differences.

Tokens, fonts and the nav/footer are identical to [home-spec.md](home-spec.md). New text style seen here:
| Style name | Font | Size / line-height |
|---|---|---|
| הערות (notes) | Fb Booster Regular | 16 / 10 — note: in the home frame "הערות" was Leon 12/18; confirm which is current |

## Layout (top → bottom, RTL)

1. **Top nav** — same as home (120px, `rgba(244,244,244,.9)`).
2. **Background** — full-bleed synagogue photo (1280×1290) behind the upload area.
3. **Main image drop zone** — 1139×510, rounded, checkerboard (transparent) fill, centered text (Fb Booster Medium 40px):
   > לכאן גוררים ומשחררים תמונה ראשית / או / בוחרים קבצים מהתיקייה
4. **Three secondary image slots** — 360×264 each, rounded, checkerboard, in one row (gap ~30px).
5. **Two-column form area** (y≈1070):

   **Right column — card** (555×805, `paper` bg, 1px `ink` border, radius 50px):
   - **Title** field: label "כותרת" (Fb Booster Medium 40px), hint "הקלידו כותרת שמאפיינת את הדירה שלכם" (13px).
   - **Description** field: 4 ruled lines (510px wide), hint "פה תכתבו הסבר קצר על הדירה. כמה שתכתבו ברור ויותר, זה ימשוך יותר שוכרים פוטנציאליים."
   - **Price per period** — 2 columns × 4 rows of toggle-pills (240×62, gold `#B7B275`, rounded on the start side 68px, with a white toggle knob 27×46 and a white inner price box 120×54 containing "5000" + ₪ icon). Periods:
     | Right column | Left column |
     |---|---|
     | חודש תשרי | שבת שובה |
     | ראש השנה | עשי״ת |
     | יום כיפור | שמחת תורה |
     | סוכות | אחר |
     → Each period = on/off toggle + price (₪). This is the core pricing model: **price per holiday period**, plus "אחר" (other).
   - **Phone** — hint "הכנס מספר טלפון ליצירת קשר", dark pill input (Fb Booster 43px, tracking 3px), placeholder "0123456789".
   - **Email** — hint "הכנס כתובת מייל ליצירת קשר", dark pill input, placeholder "...@...".

   **Left column — details** (title "מלאו פה את פרטי הדירה שלכם", Fb Booster Medium 20px):
   - Row 1 — counters with dropdown arrows (icons 71px): dates/availability (time-and-date) · beds (bed, badge "5") · rooms (open-door) · location (pin).
   - Row 2 — floor (stairs + dropdown) · size (arrows) · arrows-16 (?) · AI icon with "בקרוב" badge.
   - Amenities (icon + 13px label, multi-select): **מיזוג · ספה · עריסה (with count dropdown) · מזרונים (with count dropdown)**, then **סוכה · נוף · מרפסת\חצר · מעלית**.
   - Buttons: **שמור** (gold) and **ביטול** (dark), pills, Fb Booster 43px.
6. **Footer** — same `Component 1` as home.

## Data model implications (for Phase 2)
- Listing: title, description, main image + 3 extra images (confirm max count), contact phone, contact email.
- Pricing: per holiday period — חודש תשרי, שבת שובה, ראש השנה, עשי״ת, יום כיפור, שמחת תורה, סוכות, אחר — each with `enabled` + `price` (₪). Should periods be a managed list (admin can add Pesach/Shavuot etc.)? → open question.
- Attributes: beds, rooms, floor, size, location (area/street?), availability dates.
- Amenities (boolean): air conditioning, sofa, view, sukkah, balcony/yard, elevator; (count): cribs, mattresses.
- Privacy: phone + email are shown to searchers — decide whether to show them directly, behind a click, or via a contact form (anti-scraping).

## Open questions
1. Holiday list differs between screens ("שבת סליחות" on the narrow home vs "שבת שובה" here and on the wide home; "תשרי" vs "חודש תשרי"; "עשי״ת" appears only here).
2. "arrows 16" icon in row 2 — what field is it?
3. Is "אחר" a free-text period with its own dates?
4. Max number of images; is the main image required?
5. Does the "view" mode differ (e.g. booking button instead of save)?

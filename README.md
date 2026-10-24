# Fashion
# Fashion+ — Premium Fashion E-Commerce Storefront

A single-file, fully responsive fashion storefront (demo). Pure HTML, CSS and vanilla JavaScript — no build step, no dependencies.

**Live page:** https://claude.ai/artifact/JW3z1n3bM4qZem43KexBoj
**Source file:** `fashion-plus.html`

---

## Quick start

1. Download `fashion-plus.html`.
2. Open it in any modern browser (double-click), or serve the folder:
   ```bash
   python3 -m http.server 8000
   # then open http://localhost:8000/fashion-plus.html
   ```
3. Internet is only needed for Google Fonts (Playfair Display, Cormorant Garamond, Montserrat). The page falls back to Georgia / system sans without it.

---

## Page structure (top to bottom)

| # | Section | Details |
|---|---------|---------|
| 1 | **Header** | Fashion+ wordmark, nav (New In, Women, Men, Accessories, Collections, Sale), icons: search, account, wishlist, bag with count badge, burger menu on mobile |
| 2 | **Hero** | Lavender gradient, large serif **FASHION** heading, "Style Without Limits", description, **Shop Collection** and **Watch Lookbook** buttons, model in arch frame on the right plus an oval secondary photo, 01/02/03 slide dots |
| 3 | **Benefits strip** | Free Shipping, Easy Returns, Premium Quality, Secure Payment (outline icons, separators) |
| 4 | **Collections** | Women and Men banner cards with model photos and circular arrow buttons |
| 5 | **Trending Now** | 5 product cards: Striped Belt Dress ₹2,999, Tailored Blazer ₹2,899, Wide Leg Pants ₹1,899, Classic Handbag ₹2,999, Chunky Sneakers ₹3,499 |
| 6 | **Editorial banner** | "Elegance In Every Detail" with Explore Now button |
| 7 | **Footer** | Wordmark, Privacy Policy, Terms of Service, Customer Care, copyright |

---

## Features

**Working demo interactions**
- Wishlist hearts with active state and toast feedback
- Add to bag with animated cart badge counter
- Search overlay that filters the product list (Esc or click outside to close)
- Mobile burger menu with `aria-expanded`
- Hero slides: clickable 01/02/03 dots, auto-advance every 6 s, eyebrow text and gradient change
- Smooth anchor scrolling
- Colour theme picker (bottom-left): **Purple, Rose, Ocean, Teal**, remembered via `localStorage`

**Demo only (not real):** account sign-in, checkout, payments, lookbook video, View All, Sale and footer links show a toast message instead.

**Motion**
- Page-load entrance on header and hero text
- Slow hero gradient drift, light parallax on hero image
- `IntersectionObserver` scroll reveals with stagger on product cards
- Animated nav underline, icon hover lift, button press feedback
- Fully disabled under `prefers-reduced-motion`

---

## Responsive behaviour

| Width | Behaviour |
|-------|-----------|
| > 900px | Two-column hero, 4-column strip, 2 collection cards side by side, 5 products in one row |
| ≤ 900px | Burger menu, hero text then photos stacked, 2-column strip, collection cards stacked, products scroll horizontally with snap, banner photo on top |
| ≤ 480px | Smaller headline and buttons, colour picker label hidden |

No horizontal page overflow was found when tested at 360px, 390px and 768px.

---

## Design tokens

All colours are CSS custom properties on `:root`, so a theme is just a set of variables.

```css
--p   primary      --dp  dark       --v  accent
--l   lavender     --t1..--t4  tints for gradients
--line  hairlines  --imgf  CSS filter applied to photos
```

Default (Purple): `#542078`, `#29113F`, `#A64DD2`, `#D9A8F0`, background `#FAF7FC`.

**Fonts:** Playfair Display for the hero headline, Cormorant Garamond for editorial headings, Montserrat for navigation, product and body text.

**Radii:** 16–22px cards, fully rounded pill buttons, arch and oval photo frames.

---

## Customisation

**Replace photos.** Images are embedded as data URIs in per-image CSS variables near the end of `<head>`:
```css
.img-a1 { --img: url(your-image.jpg); }   /* hero main arch */
.img-a2 { --img: url(...); }              /* hero oval */
.img-women, .img-men, .img-promo          /* banners */
.img-p0 … .img-p4                         /* five products */
```
Use normal image paths if you host the images yourself.

**Add a theme.** Add a block and a swatch button:
```css
:root[data-theme=forest]{--p:#…;--dp:#…;--v:#…;--l:#…;--t1:#…;--t2:#…;--t3:#…;--t4:#…;--line:#…;--imgf:none}
```
```html
<button data-th="forest" aria-label="Forest theme" aria-pressed="false" style="background:…"></button>
```

**Edit products.** Change the `P` array at the top of the `<script>` block (name and price) and the `.img-pN` photo.

---

## Known limitations

- Current photos are small crops from design reference screenshots, so they look soft on large screens and may carry faint source watermarks. Use high-resolution licensed photography for production.
- The theme picker recolours photos with a CSS hue shift, so skin tones are approximate outside the Purple and Ocean themes.
- There is no backend: cart, wishlist and checkout are simulated in memory.

---

## Prompt to recreate this website

> Build a premium, fully responsive fashion e-commerce storefront called **Fashion+** as a single HTML file (HTML5, CSS3, vanilla JS). Luxury editorial style, deep purple / violet / lavender palette on a light lavender-white background (#FAF7FC; primary #542078, dark #29113F, accent #A64DD2, lavender #D9A8F0). Serif for editorial headings, geometric sans for navigation and product text.
>
> **Sections in order:** (1) header with Fashion+ wordmark, nav (New In, Women, Men, Accessories, Collections, Sale) and icons (search, account, wishlist, bag with badge); (2) hero on a purple gradient with eyebrow "NEW COLLECTION 2026", oversized serif **FASHION**, subtitle "Style Without Limits", short description, buttons "Shop Collection →" and "▷ Watch Lookbook", model photo on the right in an arch frame with a smaller oval photo, and 01/02/03 slide dots; (3) four-item benefits strip (Free Shipping above ₹1499, Easy Returns, Premium Quality, Secure Payment); (4) Women and Men collection cards with model photos and circular arrow buttons; (5) "Trending Now" with five product cards (Striped Belt Dress ₹2,999, Tailored Blazer ₹2,899, Wide Leg Pants ₹1,899, Classic Handbag ₹2,999, Chunky Sneakers ₹3,499), each with a wishlist heart; (6) wide editorial banner "THE PURPLE EDIT — Elegance In Every Detail" with an Explore Now button; (7) rounded purple footer with Privacy Policy, Terms of Service, Customer Care and © 2026 Aureli Studio.
>
> **Interactions:** working wishlist hearts, add-to-bag with animated cart badge, search overlay filtering products, mobile burger menu, auto-advancing hero slides, smooth anchor scrolling, toast messages for demo-only actions, and a colour theme picker (Purple, Rose, Ocean, Teal) driven by CSS variables and remembered in localStorage.
>
> **Motion:** subtle only (250–700ms ease-out): load entrance, slow gradient drift, light hero parallax, IntersectionObserver reveals with stagger, nav underline animation, hover zoom on images, and respect `prefers-reduced-motion`.
>
> **Responsive:** burger menu under 900px; hero text above photos; two-column benefits strip; stacked collection cards; horizontally scrolling product row with scroll snap; no horizontal overflow at 360px.
>
> Use CSS custom properties for colours, semantic HTML, visible focus states and ARIA labels. Make it clear that checkout, sign-in and payments are demo only.

---

© 2026 Aureli Studio. Demo storefront.

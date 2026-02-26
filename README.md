# DYNAMO — Premium Training Facility

A brutalist-inspired, single-page web presence for a high-performance gym in Durban. No templates. No frameworks. Just raw HTML, CSS, and JavaScript engineered to feel like the facility itself: unapologetic, intentional, and built to last.

Live: [Preview live demo here.](https://lefajmofokeng.github.io/Dynamo)

---

## The Concept

Most gym websites look like they were designed by committee. Sterile stock photos. Generic "fitness" stock footage. Endless sliders nobody clicks. Dynamo rejects all of that.

This is a digital storefront for a facility that doesn't cater to casuals. The design language mirrors the physical space: concrete, steel, raw finishes. High contrast. No gradients. No rounded corners softening the edges. Every pixel earns its place.

The experience is meant to feel immediate. Live occupancy data that fluctuates. Infinite tickers announcing amenities. A sign-up flow that captures intent without friction. This isn't a brochure — it's a tool.

---

## Architecture

### Structure

The entire page lives in a single `index.html` file. No build step. No dependencies. No npm install required. You could serve this from a Raspberry Pi in the corner of the gym and it would run flawlessly.

```
DYNAMO/
├── index.html          # everything: structure, styles, behavior
└── README.md           # this file
```

That's it. 1800+ lines of hand-written code. Every section self-contained. Every animation defined in CSS. Every interaction scripted in vanilla JavaScript.

### Technical Decisions

**No frameworks** — React would be overkill for a static presence. No need for virtual DOM when the DOM is right there.

**No external dependencies** — Fonts are pulled from Google Fonts (Bebas Neue, Barlow, Barlow Condensed) but everything else is local. No jQuery. No Bootstrap. No lodash.

**No build tools** — Write, save, refresh. The development cycle is instantaneous. What you see is what ships.

**Fixed positioning for overlays** — The sign-up panel and mobile menu use fixed positioning with backdrop blur. Keeps them detached from document flow, guarantees they appear above everything.

---

## Key Components

### Navigation

The nav bar starts transparent, gains a backdrop blur and background after scrolling past 60px. Logo uses Bebas Neue with heavy letter-spacing — reads as industrial, authoritative. Desktop nav hides on mobile; hamburger takes over.

### Hero Section

Background video from Pexels (drops to poster image if video fails). Overlay gradient ensures text remains readable regardless of video brightness. The "Start Your Journey" CTA opens the sign-up panel directly — no intermediate pages.

### Live Occupancy Bar

Simulated real-time data. Updates every 4 seconds, random walk between 6 and 120 members. Capacity bar changes color based on crowd level:
- <40%: green
- 40-60%: yellow
- 60-80%: orange
- >80%: red

The copy updates accordingly: "Quiet time", "Moderate", "Getting busy", "Very busy". This small touch makes the page feel alive.

### Infinite Tickers

Two tickers run continuously:
1. Amenities ticker below the live bar (free water, protein shop, etc.)
2. Footer marquee repeating "DYNAMO"

Both use CSS animations with `linear infinite`. The content is duplicated to create seamless loops. Pause on hover for readability.

### Split Section

Three-image collage with overlapping positioning. The "D" in the background is massive, low-opacity — subtle branding without shouting. CTA arrow expands on hover, guiding users toward the facility gallery.

### Features Grid

Four-column layout (collapses responsively). Icons are inline SVGs — no font icons, no image requests. Hover state darkens the card slightly, signaling interactivity.

### Gallery Mosaic

Grid layout with one large tile spanning two rows. Overlays appear on hover with gradient backgrounds. Below the mosaic, a scrolling track of additional facility shots duplicates for infinite effect.

### Programs Grid

Each card displays a program number (01–06) as a ghost element in the background. Data attributes hold these numbers, CSS `::before` injects them. Keeps markup clean while allowing visual flair.

### Trainers

Photo cards with gradient overlays fading from transparent to card background. Spec tags outline specialties. Images from Pexels — consistent lighting, professional look without being sterile stock.

### Pricing

Three-column grid with the middle plan highlighted (white background, black text). Feature lists use SVG checkmarks. The "Most Popular" badge is just text with a star — no extra markup needed.

### Testimonials

Slider with manual controls and auto-advance every 6.5 seconds. Four slides, dot indicators, prev/next buttons. The quote mark is a massive glyph set in Bebas Neue — typographic statement.

### Sign-up Flow

Two-column layout on desktop (inspirational image left, form right). Collapses to single column on mobile. Form uses:
- Accordions for personal details and plan selection
- Radio cards for plan choices (styled beyond default radios)
- Real-time summary updates (the accordion headers show current selections)

On submit, form hides and success state appears. No actual data submission — this is a front-end demo.

### Footer

Four-column layout with brand statement, navigation, contact, hours. Social icons are SVGs. Bottom marquee repeats the brand name as a subtle texture.

---

## JavaScript Functionality

### Scroll Effects
- Nav bar styling on scroll
- Intersection Observer for reveal animations (elements fade up when they enter viewport)
- Counter animation when stats section becomes visible

### Mobile Menu
- Hamburger toggles fixed overlay
- Close on escape key or outside click
- Body scroll locked when menu open

### Live Updates
- Occupancy counter cycles every 4 seconds
- Capacity bar width and color update accordingly
- All values recalculated in JavaScript, DOM updated directly

### Form Interactions
- Plan radios update accordion summary text
- Date of birth and goal selection update personal details summary
- Validation on submit (checks name and email, others optional)
- Escape key closes sign-up panel

### Slider
- Manual controls and auto-advance
- Dot indicators update with current slide
- Slide count display (01/04 format)

---

## Responsive Behavior

Breakpoints at 1024px and 640px.

**1024px and below:**
- Desktop nav links hide, hamburger appears
- Split section stacks (image grid below text)
- Features grid becomes 2 columns
- Gallery mosaic reflows (large tile spans full width)
- Programs grid becomes 2 columns
- Trainers grid becomes 2 columns
- Pricing stacks to single column
- Stats grid becomes 2 columns
- Testimonials layout adjusts (smaller photo)
- Footer becomes 2 columns
- Sign-up becomes single column (image hides)

**640px and below:**
- Further stacking
- Features grid becomes 1 column
- Split section hides two of the three images (only primary remains)
- Gallery mosaic becomes single column
- Programs grid becomes 1 column
- Trainers grid becomes 1 column
- Stats grid becomes 1 column
- Testimonials stacks vertically
- Footer becomes 1 column
- Form rows stack
- Mobile menu font size reduces slightly

---

## Design Choices

### Typography
- **Bebas Neue** — headings, logo, large numerals. Condensed, bold, commands attention.
- **Barlow Condensed** — navigation, labels, buttons. Readable at small sizes, maintains the compressed aesthetic.
- **Barlow** — body text. Neutral, highly legible, contrasts with the display faces.

### Color Palette
- `#080808` — true black background
- `#0f0f0f` — slightly lighter for cards
- `#141414` — card backgrounds
- `#242424` — borders, dividers
- `#888` / `#bbb` / `#ddd` — text hierarchy
- `#ffffff` — pure white for primary text and accents

No color beyond grayscale except the live dot (green) and capacity bar (green/yellow/orange/red). Restraint reinforces the industrial vibe.

### Spacing
Consistent padding values: 48px on desktop sections, 20px on tablet, 16px on mobile. Grid gaps of 1px create visible borders between cards. This thin separation reads like concrete panel joints.

### Animation
Easing follows `cubic-bezier(0.16,1,0.3,1)` — starts fast, ends smooth. Transitions are deliberate but not distracting. Hover effects mostly affect color and scale, never position (avoids layout shift).

---

## Performance Considerations

- **No external requests** except fonts and images. Fonts are critical, images load as needed.
- **Images from Unsplash/Pexels** — using their CDN with size parameters (`?w=900&q=80`) reduces payload.
- **Minimal JavaScript** — no heavy computation, no frameworks parsing.
- **CSS animations** — handled by the GPU where possible (transforms, opacity).
- **No web fonts fallback** — system fonts until Google Fonts loads. Acceptable trade-off for design consistency.

---

## Known Quirks

- The video source points to a Pexels download page, not a direct video file. In production, this would be replaced with an actual MP4 URL. Currently falls back to image background.
- Live occupancy data is simulated. Real implementation would pull from an API (member check-ins, turnstile data).
- Form submission shows success but doesn't POST anywhere. Intended as UI prototype, not backend integration.
- Some Pexels images may require attribution depending on license. Current selections are free for commercial use but verification recommended.
- The mobile menu close button sits behind the main content in stacking context — fixed position ensures it's reachable.

---

## Deployment

This is a static site. Deploy anywhere that serves HTML:

```
git clone https://github.com/lejafmofokeng/lejafmofokeng.github.io.git
cd lejafmofokeng.github.io
# edit index.html as needed
git add .
git commit -m "update Dynamo"
git push
```

GitHub Pages serves the content automatically from the root of the repository. No build step, no configuration.

---

## Extending

If this were a real production site:

1. **Replace video source** — host an MP4 file locally or use a CDN.
2. **Connect live occupancy** — fetch from an API endpoint, update via WebSocket or polling.
3. **Form handling** — POST to a serverless function that sends confirmation emails and stores leads.
4. **Image optimization** — run local images through a compressor, use srcset for responsive delivery.
5. **Analytics** — add privacy-focused tracking (Plausible, Simple Analytics) to monitor conversions.
6. **CMS integration** — if trainers or programs change frequently, pull from a headless CMS (Sanity, Contentful).

---

## Credits

- **Fonts**: Google Fonts (Bebas Neue, Barlow, Barlow Condensed)
- **Images**: Unsplash (via Unsplash API), Pexels (via Pexels API)
- **Icons**: Custom SVGs, hand-drawn in Illustrator
- **Inspiration**: Brutalist architecture, industrial design, hardcore training culture

---

## The Point

This isn't just a website. It's a statement. Every line of code, every pixel, every transition was considered with the same intensity that a lifter brings to a PR attempt. The gym doesn't compromise on equipment, on coaching, on atmosphere. The website shouldn't compromise on experience.

Dynamo is digital iron. Heavy. Cold. Unforgiving. Exactly what it needs to be.

---

*Lift heavy. Move well. Stay hard.*

— lejafmofokeng

# Klaviyo Retention Dashboard — Landing Page

Landing page for the Klaviyo Retention Dashboard product. Built as a single HTML file deployed on Cloudflare Workers.

---

## Deploying to Cloudflare Workers

```
landing-page/
├── index.html     ← the page
├── worker.js      ← serves the HTML
├── wrangler.toml  ← Worker config
└── README.md
```

**worker.js**
```js
import html from './index.html';

export default {
  async fetch(request) {
    return new Response(html, {
      headers: { 'Content-Type': 'text/html;charset=UTF-8' },
    });
  },
};
```

**wrangler.toml**
```toml
name = "retention-dashboard-landing"
main = "worker.js"
compatibility_date = "2024-01-01"
```

Deploy:
```bash
wrangler deploy
```

---

## How to Replace Images

All images in `index.html` are currently hotlinked from `conversion.care` as placeholders. Replace each one with your own hosted image URL (Cloudflare R2, S3, Cloudinary, etc.) or a relative path if you're serving assets from the same Worker.

Search for `conversion.care` in `index.html` to find every image that needs replacing.

---

### 1. Your Headshot — Author Badge (Hero)

**Line ~282** and **Line ~726** (FAQ section)

```html
<!-- REPLACE THIS: -->
<img class="author-photo" src="https://www.conversion.care/wp-content/uploads/2024/08/jaka_smid_conversion_designer.png" alt="Steven — Sales Ignition" />

<!-- WITH YOUR PHOTO: -->
<img class="author-photo" src="YOUR-HEADSHOT-URL.jpg" alt="Steven — Sales Ignition" />
```

Same photo is used again in the FAQ section:
```html
<img class="faq-photo" src="https://www.conversion.care/wp-content/uploads/2024/08/jaka_smid-removebg-preview-1-1.png" alt="Steven — Sales Ignition" />
```
Replace with a **transparent PNG background** version of your headshot for best results in the FAQ layout.

**Recommended size:** 400×400px minimum, square crop.

---

### 2. Dashboard Product Screenshot (Product Intro Section)

**Line ~406**

```html
<img class="product-intro__img" src="https://www.conversion.care/wp-content/uploads/2024/08/email-checklist-previeew-1024x621.png" alt="Klaviyo Retention Dashboard Preview" />
```

Replace with a full screenshot of your actual dashboard.

**Recommended size:** 1200×730px (16:10 ratio). PNG or WebP.

---

### 3. Pricing Section Product Mockup

**Line ~519**

```html
<img src="https://www.conversion.care/wp-content/uploads/2024/08/image-33.png" alt="Retention Dashboard" />
```

Replace with a styled mockup of your dashboard (e.g. in a browser frame or device frame). Tools like [Screely](https://screely.com) or [Mockuphone](https://mockuphone.com) work well for this.

**Recommended size:** 800×600px.

---

### 4. Feature Section Screenshots (7 images)

These are the main feature illustrations that appear under each feature description. Replace them one at a time as you have real dashboard screenshots ready.

| Line | Current placeholder | What to replace with |
|------|--------------------|-----------------------|
| ~447 | `automations@2x.png` | Screenshot of your **Unified Revenue View** |
| ~456 | `sale-event@2x.png` | Screenshot of your **Retention KPIs module** |
| ~465 | `newsletter@2x.png` | Screenshot of your **Flow Performance Rankings** |
| ~474 | `popup@2x.png` | Screenshot of your **List Health module** |
| ~483 | `test-creative@2x-1.png` | Screenshot of your **Segment Performance view** |
| ~492 | `delivery@2x-1.png` | Screenshot of your **Campaign Analytics module** |
| ~501 | `priority@2x.png` | Screenshot of your **Winback Tracker** |

**Recommended size:** 1200×750px. Use consistent dimensions across all 7 for a clean look.

---

### 5. Testimonial Screenshots (Social Proof Gallery)

**Lines ~651–657** — 7 screenshot images displayed as a gallery grid above the written testimonials.

```html
<img src="https://www.conversion.care/wp-content/uploads/2024/08/real-twitter-testimonial-1024x574.png" alt="Testimonial screenshot" />
<img src="https://www.conversion.care/wp-content/uploads/2024/08/testimonial1.png" alt="Testimonial" />
<!-- ...5 more -->
```

Replace with real screenshots of:
- Twitter/X posts from customers
- LinkedIn comments
- Email replies
- Slack messages
- Any text-based social proof

**Recommended size:** 800×450px each. Crop to consistent dimensions.

---

### 6. Testimonial Author Photos (4 individual reviews)

**Lines ~668, ~680, ~692, ~704**

```html
<img class="testi-item__photo" src="https://www.conversion.care/wp-content/uploads/2024/08/ela.jpeg" alt="Alex T." />
```

Replace each with the real reviewer's profile photo, or a generic avatar if you don't have one.

**Recommended size:** 100×100px, square crop, circular display.

---

### 7. Platform Logos (Hero)

**Lines ~308–311** — Klaviyo, Shopify, and other integration logos.

```html
<img src="https://www.conversion.care/wp-content/uploads/2024/08/klaviyo.png" alt="Klaviyo" />
<img src="https://www.conversion.care/wp-content/uploads/2024/08/activecampaign.png" alt="Shopify" />
```

These are currently filtered to white (`filter: brightness(10) grayscale(1)` in the CSS) so any logo on a transparent background will work. Replace with official logo files from each platform's brand kit.

- Klaviyo brand assets: [klaviyo.com/brand](https://www.klaviyo.com/brand)
- Shopify brand assets: [shopify.com/brand-assets](https://www.shopify.com/brand-assets)

---

### 8. Payment Method Logos

**Lines ~566 and ~601** — shown below the checkout buttons on the pricing cards.

```html
<img src="https://www.conversion.care/wp-content/uploads/2024/08/image-25-1.png" alt="Accepted payments" />
<img src="https://www.conversion.care/wp-content/uploads/2024/08/image-26-1.png" alt="Secured shopping" />
```

Replace with your own payment/trust badge image. If Spiffy handles this on their checkout page, you can remove these entirely or use a simple "Secured by SSL" badge.

---

### 9. Guarantee Badge

**Line ~628**

```html
<img class="guarantee-card__img" src="https://www.conversion.care/wp-content/uploads/2024/08/image-27-3.png" alt="Money-back guarantee" />
```

Replace with your own 14-day money-back guarantee badge. You can generate a clean one at [Canva](https://canva.com) or similar.

---

## Image Hosting Options

| Option | Best for | Notes |
|--------|----------|-------|
| **Cloudflare R2** | Best fit — same ecosystem | Free egress, pairs perfectly with Workers |
| **Cloudinary** | If you need resizing/optimization | Free tier is generous |
| **GitHub raw** | Quick and easy for small projects | Use `raw.githubusercontent.com` URLs |
| **Same Worker (KV or inline)** | Fully self-contained deployment | Base64 encode small images directly in HTML |

For R2, upload your images and make them public, then your URLs will look like:
```
https://pub-YOURHASH.r2.dev/your-image.png
```

---

## Quick Find & Replace

To swap all placeholder images at once, run this in your terminal from the `landing-page/` folder:

```bash
# Example: replace the author photo
sed -i 's|https://www.conversion.care/wp-content/uploads/2024/08/jaka_smid_conversion_designer.png|YOUR-NEW-URL.jpg|g' index.html
```

Or just open `index.html` in VS Code and use **Find & Replace** (`Cmd+H`) — search for `conversion.care` to see every image that still needs replacing.

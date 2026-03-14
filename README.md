# Dumpster Drop KC — Static Site

Plain HTML/CSS static site for dumpsterdropkc.com, designed to replace the Docket-hosted WordPress site.

## File Structure

```
site/
├── index.html          # Home page
├── about.html          # About page
├── dumpsters.html      # Dumpster sizes, pricing, prohibited items
├── service-areas.html  # List of served cities
├── contact.html        # Contact info + form
├── styles.css          # All styles (shared across pages)
├── images/             # You need to add these (see below)
│   ├── dumpster-10yd.jpg
│   ├── dumpster-15yd.jpg
│   ├── dumpster-20yd.jpg
│   ├── flex-dumpster.jpg
│   ├── owners.jpg       # John & Blyth photo (from About page)
│   └── logo.png         # If you want to use the logo image
└── README.md
```

## Migration Checklist

### 1. Download Images from Current Site
Before canceling Docket hosting, download these images from dumpsterdropkc.com:

- `wp-content/uploads/sites/232/2023/05/IMG_0096-1024x768.jpg` → save as `images/dumpster-10yd.jpg`
- `wp-content/uploads/sites/232/2023/05/IMG_0099-2-1024x768.jpg` → save as `images/dumpster-15yd.jpg`
- `wp-content/uploads/sites/232/2023/05/IMG_0024-1024x768.jpg` → save as `images/dumpster-20yd.jpg`
- `wp-content/uploads/sites/232/2023/05/Untitled-design-5-e1684351831220-1024x768.png` → save as `images/flex-dumpster.jpg`
- `wp-content/uploads/sites/232/2023/05/IMG_0002-768x1024.jpg` → save as `images/owners.jpg`
- `wp-content/uploads/sites/232/2023/05/Dumpster-Drop_Logo_Color-Version-1024x576.png` → save as `images/logo.png`

### 2. Set Up Contact Form
The contact form uses Formspree as a placeholder. To activate it:

1. Go to https://formspree.io and create a free account
2. Create a new form — you'll get an endpoint like `https://formspree.io/f/xyzabc123`
3. In `contact.html`, replace `YOUR_FORM_ID` with your actual form ID

Alternative: If you'd rather not use a third party, you can remove the form
and just rely on phone/email/text, which is how most of the orders come in anyway.

### 3. Deploy to Cloudflare Pages

1. Create a GitHub repo (can be private)
2. Push all site files to the repo
3. Go to https://dash.cloudflare.com → Pages → Create a project
4. Connect your GitHub repo
5. Build settings:
   - Framework preset: None
   - Build command: (leave blank)
   - Build output directory: `/` (or `.` — the root, since there's no build step)
6. Deploy

### 4. Connect Your Domain

**If domain is already on Cloudflare DNS:**
- In Cloudflare Pages project settings → Custom domains → Add `dumpsterdropkc.com`
- Cloudflare auto-creates the DNS record

**If domain is at another registrar:**
- Option A (recommended): Transfer domain to Cloudflare Registrar, then do the above
- Option B: Add a CNAME record pointing `dumpsterdropkc.com` to `your-project.pages.dev`
  (Note: CNAME at apex requires the registrar to support CNAME flattening — Cloudflare does this natively)

### 5. Verify DocketShop Integration
The "Book Now" buttons link to:
```
https://embed.survcart.com?type=landing&co=13ut0EZG4WG3hWWyNAr7&wsid=N8kKZLtywSlGoTr9LDem&sel=ojN9nrIqokP8r1iL5Cd7
```
Confirm with Docket support that this embed URL continues to work after
you cancel their website hosting plan. The `wsid` parameter may be tied
to their hosted site. If it breaks, you'll need a new DocketShop embed
URL from Docket — they should provide one since you're still using their
software for operations.

### 6. Cancel Docket Website Hosting
Only after everything above is confirmed working:
- Cancel the $100/mo Docket website hosting plan
- Keep Docket's core software subscription (dispatch, billing, etc.)

## Ongoing Costs
- Domain renewal: ~$10-12/year
- Cloudflare Pages hosting: Free
- Formspree (if using): Free up to 50 submissions/month
- **Total: ~$10-12/year** (vs $1,200/year for Docket hosting)

## Editing the Site
It's just HTML files. Open any file in a text editor, change the content, commit and push to GitHub. Cloudflare auto-deploys on push.

To update pricing: edit the `dumpster-card__price-value` elements in both `index.html` and `dumpsters.html`.

To add a service area: add a `<div class="area-tag">City Name</div>` to `service-areas.html`.

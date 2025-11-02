# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Static website for Pavlina Hlavata's psychology practice. This replaces her current WordPress site with a simple, fast, and maintainable static site hosted on GitHub Pages.

**Business Owner**: Pavlina Hlavata, Psychologist

## Tech Stack

- **Plain HTML5, CSS3, vanilla JavaScript** (no build tools)
- **Responsive design** using CSS Grid/Flexbox
- **Web3Forms** for contact form functionality
- **GitHub Pages** for hosting
- **Python http.server** for local testing

## Development Commands

### Local Testing
```bash
# Serve the site locally on port 8000
python3 -m http.server 8000

# Or use Python 2
python -m SimpleHTTPServer 8000

# Then visit: http://localhost:8000
```

### Deployment
```bash
# Commit and push to main branch
git add .
git commit -m "Update site"
git push origin main

# GitHub Pages will automatically deploy from the main branch
```

## Site Structure

Single-page website (`index.html`) with the following sections:

1. **Header** (Sticky with Smart Behavior)
   - Title: "Psychologické poradenství / Pavlína Hlavatá"
   - Subtitle with service details and approach (visible when at top)
   - Light blue background (#d4e4f7)
   - When scrolled down: subtitle fades out, only title remains visible
   - JavaScript handles scroll detection and CSS transition

2. **Hero Section**
   - Full-width autumn leaves background image
   - Large heading: "Psychologické poradenství"
   - Left-aligned text with strong shadow for readability

3. **About Section** (O mně)
   - Two-column layout: text (left) + portrait photo (right)
   - Biography and qualifications
   - Portrait image: `portrait.webp`

4. **Contact Section - First** (Kontaktujte mě)
   - **Center-aligned** content
   - Email prominently displayed in **bold** and larger font
   - Contact form placeholder (for Web3Forms)
   - Located BEFORE the image gallery bar

5. **Image Gallery Bar**
   - Horizontal strip of 5 images
   - Height: 250px (50% less cropping than original 150px)
   - Order: sky → flower → rocks → leaf → beach
   - Files in `smol_images/` (mix of .jpg and .jpeg extensions)

6. **Pricing Section** (Ceník)
   - Service pricing information
   - 500 Kč for 50-55 min consultation
   - Payment methods and insurance note
   - Located AFTER the image gallery bar

7. **Footer - Contact Info**
   - Smaller, condensed contact information
   - Dark blue background (primary color)
   - White text
   - Address and email details
   - Copyright notice

## File Structure

```
/
├── index.html              # Main single-page website
├── styles.css             # All styling (responsive design)
├── portrait.webp          # Portrait photo for About section
├── autumn-leaves.jpg      # Hero section background
├── smol_images/           # Image gallery bar
│   ├── sky.jpg
│   ├── flower.jpg
│   ├── rocks.jpg
│   ├── leaf.jpg
│   └── beach.jpg
├── CLAUDE.md              # This file
└── README-IMAGES.md       # Image sourcing guide
```

## Design Details

### Typography & Alignment
- Most headers and section titles are **left-aligned**
- First contact section is **center-aligned** with bold email
- Header title has line breaks: "Psychologické poradenství" on first line, "Pavlína Hlavatá" on second
- Subtitle text has line breaks for better readability

### Color Scheme
- Primary: `#4a6fa5` (blue)
- Secondary: `#7fa99b` (green)
- Header background: `#d4e4f7` (light blue)
- Text: `#2c3e50` (dark) and `#555` (light)
- Background: White and `#f8f9fa` (light gray)

### Sticky Header with Smart Behavior
- Header stays fixed at top when scrolling
- Light blue background color
- Has shadow for depth (`box-shadow`)
- Uses `position: sticky` with `z-index: 1000`
- **Dynamic behavior**: When scrolled past 50px, subtitle fades out (opacity + max-height transition)
- JavaScript in HTML detects scroll position and toggles `.scrolled` class

### Image Gallery
- 5 images displayed horizontally
- Equal width (20% each)
- Height: 250px (increased from 150px for less cropping)
- Uses `flex` layout with `object-fit: cover`
- Order: sky → flower → rocks → leaf → beach
- File extensions: sky.jpeg, flower.jpg, rocks.jpeg, leaf.jpg, beach.jpeg

### Contact Sections
- **First contact section**: Center-aligned, prominent bold email, before image bar
- **Footer contact section**: Smaller, condensed info, dark blue background, after pricing

## Resources

### Stock Images
Free sources for nature/rocks imagery:
- **Unsplash** (unsplash.com) - High quality, no attribution required
- **Pexels** (pexels.com) - Great nature photos
- **Pixabay** (pixabay.com) - Large collection, free commercial use

### Contact Form
Using **Formspree** (formspree.io):
- Form endpoint: `https://formspree.io/f/mwpwykkd`
- Free tier: 50 submissions/month
- No backend required (works with static sites)
- Submissions sent to: hlavata.pavlina1@gmail.com
- Form fields: Name (Jméno), Email, Phone (Telefon), Message (Zpráva)
- Auto-redirects back to contact section after submission
- Email subject: "Nová zpráva z kontaktního formuláře"

**First-time setup:**
- First submission requires email confirmation
- Check hlavata.pavlina1@gmail.com for confirmation link
- After confirmation, all submissions work automatically

## GitHub Pages Configuration

### Initial Setup
Repository settings required:
1. Go to **Settings** → **Pages**
2. Source: **Deploy from branch**
3. Branch: **main**
4. Folder: **/ (root)**
5. Click **Save**

The site will initially be available at: `https://[username].github.io/paja-webpage/`

### Custom Domain Setup (pavlinahlavata.eu)

**Step 1: GitHub Pages Configuration**
1. Go to repository **Settings** → **Pages**
2. Under "Custom domain", enter: `pavlinahlavata.eu`
3. Check "Enforce HTTPS" (after DNS propagates)
4. GitHub will create a `CNAME` file in your repository

**Step 2: DNS Configuration at Webglobe**
Configure the following DNS records at your Webglobe hosting panel:

```
Record Type: A
Host: @
Value: 185.199.108.153
TTL: 3600

Record Type: A
Host: @
Value: 185.199.109.153
TTL: 3600

Record Type: A
Host: @
Value: 185.199.110.153
TTL: 3600

Record Type: A
Host: @
Value: 185.199.111.153
TTL: 3600

Record Type: CNAME
Host: www
Value: [your-github-username].github.io
TTL: 3600
```

**Step 3: Wait for DNS Propagation**
- DNS changes can take 24-48 hours to propagate
- Check status: `dig pavlinahlavata.eu` or use https://dnschecker.org

**Step 4: Verify and Enable HTTPS**
- Once DNS propagates, return to GitHub Pages settings
- Check "Enforce HTTPS" if not already enabled
- GitHub will automatically provision SSL certificate

## Design Principles

- Clean, professional design appropriate for healthcare
- Fast loading times
- Mobile-first responsive design
- Accessibility compliant
- Easy content updates (no complex build process)
- Nature-themed imagery (rocks, calming natural scenes)

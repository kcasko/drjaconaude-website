# Deployment Guide for Dr. Jaco Naude Website

This guide will help you deploy the website to Cloudflare Pages with Decap CMS for easy content management.

## Overview

- **Hosting**: Cloudflare Pages (FREE)
- **CMS**: Decap CMS (FREE) - visual editor for blog posts
- **Payments**: Gumroad (FREE - they take 10% on sales)
- **Booking**: Calendly (FREE tier)

**Total Monthly Cost: R0**

---

## Step 1: Set Up GitHub Repository

1. Go to [github.com](https://github.com) and create a free account (or log in)
2. Click the "+" icon and select "New repository"
3. Name it `drjaconaude-website` (or similar)
4. Keep it **Public** (required for free Cloudflare Pages)
5. Click "Create repository"
6. Upload all the website files to this repository

### To upload files:
- Click "uploading an existing file" link
- Drag and drop all files from this folder
- Click "Commit changes"

---

## Step 2: Set Up Cloudflare Pages

1. Go to [pages.cloudflare.com](https://pages.cloudflare.com)
2. Sign up for a free account (or log in)
3. Click "Create a project"
4. Select "Connect to Git"
5. Authorize Cloudflare to access your GitHub
6. Select the repository you created (`drjaconaude-website`)
7. Configure your build:
   - **Project name**: `drjaconaude` (this becomes your subdomain)
   - **Production branch**: `main`
   - **Build command**: (leave empty - it's a static site)
   - **Build output directory**: `/` (root)
8. Click "Save and Deploy"

Your site will be live at: `https://drjaconaude.pages.dev`

---

## Step 3: Connect Custom Domain

1. In Cloudflare Pages, go to your project
2. Click "Custom domains"
3. Click "Set up a custom domain"
4. Enter: `drjaconaude.co.za`
5. Follow the DNS instructions provided

If your domain is already on Cloudflare DNS, it will configure automatically.

---

## Step 4: Set Up Decap CMS (Content Editor)

Decap CMS requires authentication. The easiest free method is using Netlify Identity with Git Gateway:

### Option A: Use Netlify Identity (Recommended)

1. Go to [netlify.com](https://netlify.com) and create free account
2. Create a new site from Git (same GitHub repo)
3. Go to Site Settings > Identity > Enable Identity
4. Under Registration, select "Invite only"
5. Go to Services > Git Gateway > Enable Git Gateway
6. Invite yourself (and family members who will edit content)

Then update `admin/config.yml`:
```yaml
backend:
  name: git-gateway
  branch: main
```

Add this script to your site's `<head>`:
```html
<script src="https://identity.netlify.com/v1/netlify-identity-widget.js"></script>
```

### Option B: Use GitHub Backend (Alternative)

Update `admin/config.yml`:
```yaml
backend:
  name: github
  repo: YOUR-USERNAME/drjaconaude-website
  branch: main
```

This requires logging in with GitHub to edit content.

---

## Step 5: Set Up Gumroad (Audiobook Sales)

1. Go to [gumroad.com](https://gumroad.com)
2. Create a free account
3. Click "New product"
4. Select "Digital product"
5. Upload audiobook file
6. Set price (in USD - Gumroad converts for SA customers)
7. Publish

To embed on website:
- Copy embed code from Gumroad
- Paste into `audiobooks.html` where indicated

---

## Step 6: Set Up Calendly (Booking)

1. Go to [calendly.com](https://calendly.com)
2. Create a free account
3. Set up event types:
   - "Initial Consultation" (60 min)
   - "Follow-up Session" (50 min)
4. Set your availability
5. Copy embed code

To add to website:
1. Open `contact.html`
2. Find the `calendly-placeholder` div
3. Replace it with your Calendly embed code:

```html
<div class="calendly-inline-widget"
     data-url="https://calendly.com/YOUR-USERNAME"
     style="min-width:320px;height:630px;">
</div>
<script type="text/javascript" src="https://assets.calendly.com/assets/external/widget.js" async></script>
```

---

## Step 7: Add Photos

Replace placeholder images:

1. Add photo of Dr. Naude to `images/dr-naude.jpg`
2. Add another photo to `images/dr-naude-about.jpg`
3. Add any blog post images to `images/uploads/`

Recommended image sizes:
- Main photo: 800x1000px
- Blog images: 1200x675px (16:9 ratio)
- Audiobook covers: 800x800px (square)

---

## Managing Content

### To write a blog post:

1. Go to `https://drjaconaude.co.za/admin/`
2. Log in with your credentials
3. Click "Blog Posts"
4. Click "New Blog Post"
5. Write your post using the visual editor
6. Click "Publish"

The post will automatically appear on the blog page.

### To add an audiobook:

1. First, add the product on Gumroad
2. Go to the CMS admin
3. Click "Audiobooks"
4. Click "New Audiobook"
5. Fill in details and Gumroad link
6. Publish

---

## Updating the Website

To make changes to the design or pages:

1. Edit the HTML/CSS files
2. Commit and push to GitHub
3. Cloudflare Pages automatically rebuilds

---

## Troubleshooting

### Site not updating?
- Check Cloudflare Pages deployments for errors
- Clear browser cache
- Wait a few minutes for DNS propagation

### CMS login not working?
- Make sure Identity is enabled on Netlify
- Check you've been invited
- Try the password reset flow

### Images not showing?
- Check file paths are correct
- Ensure images are uploaded to the right folder
- Check file extensions match (case-sensitive)

---

## Support

If you need help:
- Cloudflare Pages docs: https://developers.cloudflare.com/pages/
- Decap CMS docs: https://decapcms.org/docs/
- Gumroad help: https://help.gumroad.com/
- Calendly help: https://help.calendly.com/

---

## Quick Reference

| Service | URL | Cost |
|---------|-----|------|
| Website | drjaconaude.co.za | R0/month |
| Hosting | Cloudflare Pages | R0/month |
| CMS | Decap CMS | R0/month |
| Sales | Gumroad | 10% per sale |
| Booking | Calendly | R0/month |

**Total: R0/month** (only pay when you sell!)

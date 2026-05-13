# Golden Jackets Poland — Chapter Leader Guide

Welcome Dawid! Here's everything you need to manage the Poland chapter.

---

## 1. Website Access

**Repository:** https://github.com/goldenjackets-community/golden-jackets-poland

You have write access. Any change you push to `master` branch deploys automatically in ~1 minute.

---

## 2. How to Edit the Site

### Option A: Edit directly on GitHub (easiest)

1. Go to the repo: https://github.com/goldenjackets-community/golden-jackets-poland
2. Click the file you want to edit (e.g. `index.html`)
3. Click the **pencil icon** (Edit this file)
4. Make your changes
5. Click **"Commit changes"** at the bottom
6. Wait ~1 minute — site updates automatically

### Option B: Clone locally (for bigger changes)

```bash
git clone https://github.com/goldenjackets-community/golden-jackets-poland.git
cd golden-jackets-poland
# make changes
git add .
git commit -m "description of change"
git push origin master
```

---

## 3. Common Tasks

### Translate text to Polish

The site has a translation system built-in. In `index.html`, find the translations object near the bottom:

```javascript
// Polish translations
'Welcome to ': 'Witamy w ',
'Members': 'Członkowie',
```

Add or edit translations there. The site switches language automatically based on the toggle.

### Add a new member

1. Go to **goldenjackets.pl/admin.html** (you need admin access)
2. Use the **Create User** tool to add their Lounge access
3. To add their card on the site, edit `index.html` via GitHub and copy an existing member card block

### Remove a member

1. Go to **goldenjackets.pl/admin.html**
2. Use the **Delete User** tool to remove their Lounge access

### Change site text/content

Edit `index.html` directly. The site is a single HTML file with inline CSS and JS.

### Update the ticker/banner

Find the `<div class="ticker-content">` section and update the stats:

```html
<span>🏆 X Members</span>
<span>📜 12+ Certifications</span>
<span>📍 X States</span>
```

---

## 4. Members Lounge

**URL:** https://goldenjackets.pl/members.html

Your login:
- Email: drabekdawid@gmail.com
- Temp password: GJ-Poland-2026! (change on first login)

The Lounge is for verified Golden Jacket members only.

---

## 5. What NOT to change

To keep consistency across all chapters:

- ❌ Don't change the color scheme (dark background + gold accents)
- ❌ Don't remove the Golden Jackets logo/branding
- ❌ Don't modify `config.js` (admin settings)
- ❌ Don't change the `.github/workflows/` folder (deployment pipeline)
- ❌ Don't alter the Cognito/auth integration in `members.html`

---

## 6. What you CAN freely change

- ✅ Translate all text to Polish
- ✅ Add/remove members
- ✅ Update member photos and info
- ✅ Change descriptions, about text, FAQ
- ✅ Add Polish-specific content (events, meetups, links)
- ✅ Update partner logos (with approval)
- ✅ Add blog posts or news section

---

## 7. Deployment Pipeline

Every push to `master` triggers:

1. **S3 Sync** — uploads files to the hosting bucket
2. **CloudFront Invalidation** — clears CDN cache
3. **Smoke Test** — verifies site is online (HTTP 200)

You can check deploy status at:
https://github.com/goldenjackets-community/golden-jackets-poland/actions

If a deploy fails, check the Actions log for errors.

---

## 8. Need Help?

- Ping Ricardo (Founder) for structural changes, infra, or access issues
- For content/translation — you have full autonomy
- If something breaks — don't panic, every commit is in git history and can be reverted

---

## Quick Reference

| Task | Where |
|------|-------|
| Edit site content | GitHub repo → edit file → commit |
| Check deploy status | GitHub Actions tab |
| Access Lounge | goldenjackets.pl/members.html |
| View live site | goldenjackets.pl |
| Report issues | Message Ricardo |

---

Welcome to Golden Jackets! 🇵🇱🐝

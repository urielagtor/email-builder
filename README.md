# Email Builder — GitHub Pages

Zero-login, zero-setup for your team. You configure it once in `config.js`, push it, and everyone on your team just opens the URL.

---

## Repo structure

```
your-repo/
├── index.html              ← The app (never edit this)
├── config.js               ← ✏️  Edit this once with your repo details
├── templates.json          ← ✏️  Add/remove templates here
└── templates/
    ├── give-a-hoot-day.html
    ├── general-announcement.html
    └── ...your templates...
```

---

## Setup (one-time, done by you)

### 1. Edit `config.js`

Open `config.js` and update the branding:

```js
const EMAIL_BUILDER_CONFIG = {
  appName: "Email Builder",
  orgName: "Christian Fellowship Club · Oregon Tech",
  templatesIndex: "templates.json", // leave as-is
};
```

That's it — no GitHub credentials, no tokens. Everything loads via relative URLs since the app and templates live in the same repo.

### 2. Push to GitHub

Push all files to your repo.

### 3. Enable GitHub Pages

- Go to **Settings → Pages**
- Source: **Deploy from branch → main → / (root)**
- Save. Live at `https://yourusername.github.io/your-repo/`

### 4. Share the URL

Send the URL to your team. No login. No setup. Done.

---

## Your team's workflow

1. Open the GitHub Pages URL
2. Click a template in the left sidebar
3. Fill in the fields on the right (rich text editors + image uploads)
4. Click **Render Preview** to see the finished email
5. Click **Export HTML** → Copy or Download
6. Paste into your email platform (Mailchimp, Constant Contact, etc.)

---

## Managing templates

### Adding a new template

1. Create your `.html` file in `templates/` with `{{placeholders}}`
2. Add an entry to `templates.json`:

```json
{
  "id": "my-new-template",
  "name": "My New Template",
  "description": "Short description shown in sidebar",
  "file": "templates/my-new-template.html"
}
```

3. Push. It appears immediately for everyone.

### Placeholder syntax

| In your `.html` file | Creates in the builder |
|---|---|
| `{{field_name}}` | Rich text editor (bold, italic, color, links) |
| `{{image:field_name}}` | Image upload (embedded as base64) |

Field names auto-become labels. Underscores become spaces: `{{first_name}}` → "first name".

### Removing a template

Remove its entry from `templates.json`. The `.html` file can stay or be deleted.

---

## Notes

- **Images** are embedded as base64 data URLs in the exported HTML — no hosting needed, works across all email clients
- **No accounts** — your team just opens the URL, period
- **Always fresh** — templates are fetched with cache-busting, so changes you push appear immediately
- **Read-only source view** — team members can see the raw HTML but can't accidentally break templates; edits happen in GitHub

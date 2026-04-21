# Email Template Builder — GitHub Pages

A static, zero-backend email builder hosted on GitHub Pages. Templates live as `.html` files in your repo and are fetched at runtime.

---

## Repo structure

```
your-repo/
├── index.html            ← The builder app (this file)
├── templates.json        ← Index of all available templates
└── templates/
    ├── welcome.html
    ├── newsletter.html
    └── any-other.html
```

---

## Setup

### 1. Create your GitHub repo

Create a new public GitHub repo (e.g. `email-templates`).

### 2. Push these files

Push `index.html`, `templates.json`, and your `templates/` folder to the `main` branch.

### 3. Enable GitHub Pages

- Go to **Settings → Pages**
- Set source to: **Deploy from a branch → main → / (root)**
- Save. Your site will be live at `https://yourusername.github.io/your-repo/`

### 4. Configure the app

When you first open the site, a config modal appears. Enter:
- **GitHub Username** — your GitHub username or org
- **Repository Name** — the repo name
- **Branch** — `main` (or whatever branch you use)
- **Path to templates.json** — `templates.json` (default)

Config is saved to `localStorage` — your team members each configure it once.

---

## Managing templates

### templates.json

This is the index file the app fetches. Add an entry for each template:

```json
[
  {
    "id": "welcome",
    "name": "Welcome Email",
    "description": "Sent to new users on signup",
    "file": "templates/welcome.html"
  },
  {
    "id": "newsletter",
    "name": "Monthly Newsletter",
    "description": "General newsletter with header image",
    "file": "templates/newsletter.html"
  }
]
```

**Fields:**
| Field | Required | Description |
|---|---|---|
| `id` | ✅ | Unique identifier (no spaces) |
| `name` | ✅ | Display name shown in sidebar |
| `description` | ❌ | Short description shown in sidebar |
| `file` | ✅ | Path to the `.html` file (relative to repo root) |

To add a template: add the `.html` file + add an entry to `templates.json` + push.
To remove a template: remove the entry from `templates.json` (file can stay or be deleted).

---

## Placeholder syntax

In your template `.html` files, use these placeholders:

| Syntax | What it creates |
|---|---|
| `{{field_name}}` | A rich text editor (bold, italic, color, links) |
| `{{image:field_name}}` | An image upload field |

Field names become labels in the UI automatically. Use `_` for spaces: `{{first_name}}` → "first name".

### Example template

```html
<!DOCTYPE html>
<html>
<body style="font-family:Georgia,serif;background:#f4f4f4;margin:0;padding:40px 0;">
  <table width="600" align="center" style="background:#fff;padding:40px;">
    <tr>
      <td>
        <img src="{{image:header_image}}" width="600" style="display:block;width:100%;">
        <h1>Hello, {{first_name}}!</h1>
        <div>{{body_content}}</div>
        <a href="{{cta_url}}" style="background:#e63946;color:#fff;padding:14px 32px;text-decoration:none;display:inline-block;margin-top:24px;">
          {{cta_label}}
        </a>
      </td>
    </tr>
  </table>
</body>
</html>
```

---

## How team members use it

1. Open the GitHub Pages URL
2. First visit: enter the repo config (saved forever in their browser)
3. Pick a template from the left sidebar
4. Fill in text fields (rich text editor) and upload images
5. Click **Render Preview** to see the result
6. Click **Export HTML** → copy or download the finished email

---

## Notes

- Images are embedded as **base64 data URLs** in the exported HTML — no external hosting needed, works in all email clients
- The repo config is stored in `localStorage` per browser — each team member sets it up once
- Templates are fetched fresh every time (cache-busted) — push changes to the repo and they appear immediately on next load
- No build step, no npm, no dependencies to install

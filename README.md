# TiP Lab Website

北見工業大学 テキスト情報処理研究室（TiP Lab）のウェブサイトです。  
Website for the Text Information Processing Laboratory, Kitami Institute of Technology.

---

## For Students: How to Update the Website

You only need to know **Markdown** (basically plain text with a few symbols). No need to learn any CMS, page builder, or framework.

### Setup (one time only)

1. Install Hugo: https://gohugo.io/installation/
   - Mac: `brew install hugo`
   - Windows: `choco install hugo-extended` or download from the website
2. Clone this repository:
   ```
   git clone <repository-url>
   cd tip-lab-site
   ```
3. Run the local preview:
   ```
   hugo server
   ```
4. Open `http://localhost:1313` in your browser — the site updates live as you edit files.

---

## Common Tasks

### Add a news post

Create a new file in `content/ja/news/` (and `content/en/news/` for English):

```
content/ja/news/2026-07-15-paper-accepted.md
```

File contents:
```markdown
---
title: "IP&Mに論文が採択されました"
date: 2026-07-15
---

プタシンスキ教授の論文がInformation Processing & Management誌に採択されました。
テーマは多言語有害情報検出に関するものです。
```

That's it. Save the file, commit, push.

### Update lab members

Edit **one file**: `data/members.yaml`

To add a new student:
```yaml
masters:
  - name_ja: "山田太郎"
    name_en: "Taro Yamada"
    year: "M1"
    photo: "yamada.jpg"    # put the photo in static/images/members/
    active: true
```

When someone graduates, change `active: true` to `active: false`. Don't delete the entry — it serves as a historical record.

### Add a publication

Edit **one file**: `data/publications.yaml`

Add new entries at the **top** of the file:
```yaml
- title: "Your Paper Title"
  authors: "Author1, Author2, Author3"
  venue: "Journal Name, Vol.X, No.Y, pp.ZZ-ZZ"
  year: 2026
  type: journal    # journal | conference | book | invited | patent | other
  doi: "10.xxxx/xxxxx"
```

### Edit a page's content

All content is in the `content/` folder:
```
content/
├── ja/              ← Japanese pages
│   ├── _index.md    ← Homepage text
│   ├── about.md     ← Lab introduction
│   ├── contact.md   ← Contact info
│   ├── international.md ← Info for international students
│   ├── research/    ← Research area pages
│   ├── news/        ← News posts
│   ├── members/     ← (managed via data/members.yaml)
│   └── publications/← (managed via data/publications.yaml)
└── en/              ← English pages (same structure)
```

Open the `.md` file in any text editor, change the text, save. The content uses Markdown:

```markdown
## This is a heading

This is a paragraph. **This is bold.** *This is italic.*

- This is a bullet point
- Another bullet point

[This is a link](https://example.com)
```

### Add an image

1. Put the image file in `static/images/` (e.g., `static/images/new-photo.jpg`)
2. Reference it in your Markdown: `![Description](/images/new-photo.jpg)`

---

## Deploying to the Server

After making changes:

```bash
# 1. Build the site
hugo

# 2. The built site is in the public/ folder
# 3. Upload public/ to the university server
rsync -avz public/ user@server:/path/to/webroot/
```

Or if CI/CD is set up, just:
```bash
git add .
git commit -m "Add news post about paper acceptance"
git push
```

---

## File Structure Reference

```
tip-lab-site/
├── content/           ← EDIT HERE (all page content)
│   ├── ja/            ← Japanese
│   └── en/            ← English
├── data/              ← EDIT HERE (structured data)
│   ├── members.yaml   ← Lab members
│   ├── publications.yaml ← Publication list
│   └── highlights.yaml   ← Homepage stats
├── static/            ← EDIT HERE (images, PDFs, downloads)
│   ├── css/
│   ├── images/
│   └── downloads/
├── layouts/           ← DON'T TOUCH (unless changing design)
├── hugo.toml          ← Site configuration
└── README.md          ← This file
```

**Rule of thumb:** Students only edit files in `content/`, `data/`, and `static/`. Everything in `layouts/` controls the design and should only be changed by someone who understands HTML templates.

---

## Markdown Quick Reference

| What you type | What you get |
|---|---|
| `# Heading 1` | Big heading |
| `## Heading 2` | Medium heading |
| `**bold text**` | **bold text** |
| `*italic text*` | *italic text* |
| `[link text](url)` | Clickable link |
| `![alt text](image.jpg)` | Image |
| `- item` | Bullet list |
| `1. item` | Numbered list |

---

## Need Help?

- Hugo documentation: https://gohugo.io/documentation/
- Markdown guide: https://www.markdownguide.org/
- Ask a lab member who has done it before

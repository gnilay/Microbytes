# Agency website

A single-page static site: plain HTML and CSS, no JavaScript, no build step, no dependencies.

```
website/
├── index.html              # the whole page: nav, hero, About, Services, Selected Work, Blog, Contact, footer
├── styles.css              # all styling; colours are variables at the top
├── blog/
│   └── post-template.html  # copy this for each new blog post
└── README.md
```

## 1. Fill in the placeholders

Every value that was "XXXX" in the deck is a `{{PLACEHOLDER}}`. Find-and-replace them across all files:

| Placeholder | What to put |
|---|---|
| `{{COMPANY_NAME}}` | Agency name |
| `{{EMAIL}}` | e.g. `hello@yourdomain.in` |
| `{{PHONE}}` | e.g. `+91-9876543210` (used in `tel:` links too, so keep it dialable) |
| `{{FORMSPREE_ENDPOINT}}` | Your Formspree form URL, e.g. `https://formspree.io/f/abcdwxyz` |
| `{{LINKEDIN_URL}}` | Company LinkedIn page |
| `{{RESEARCHGATE_URL}}` | ResearchGate profile |
| `{{YEAR}}` | Copyright year |

To list anything still unfilled:

```sh
grep -rn "{{" .
```

The `{{POST_*}}` and `{{AUTHOR_NAME}}` placeholders in `blog/post-template.html` are for each new post, not site-wide.

## 2. Set up the contact form (Formspree)

1. Create a free account at https://formspree.io and add a new form.
2. Copy its endpoint (`https://formspree.io/f/xxxxxxx`) into `{{FORMSPREE_ENDPOINT}}` in `index.html`.
3. Submit the form once from the live site and confirm the email Formspree sends you.

The form sends `name`, `email`, `organization` and `message`. A hidden `_gotcha` field catches spam bots.

## 3. Run it locally

Open `index.html` in a browser. That's it.

To serve it over HTTP instead (closer to production), from this folder run either:

```sh
python3 -m http.server 8000
# then open http://localhost:8000
```

## 4. Deploy

### GitHub Pages

1. Create a GitHub repository and push the contents of this folder to it (so `index.html` is at the repo root).
2. In the repo go to **Settings → Pages**, set **Source** to "Deploy from a branch", pick `main` and `/ (root)`, and save.
3. The site appears at `https://<username>.github.io/<repo>/` within a minute or two.
4. Custom domain: enter it under **Settings → Pages → Custom domain** and add the DNS records GitHub shows you.

### Netlify

- **Drag and drop:** log in at https://app.netlify.com, open **Sites**, and drop this folder onto the page.
- **From GitHub:** **Add new site → Import an existing project**, pick the repo, leave the build command empty and set the publish directory to `/` (or to `website` if this folder is inside a larger repo).

Custom domains are under **Domain management** in the site settings.

## 5. Adding a blog post

1. Copy `blog/post-template.html` to a new file, e.g. `blog/plain-language-patient-materials.html`.
2. Fill in the `{{POST_*}}` placeholders and write the body in `<p>` paragraphs (add `<h2>`, `<ul>`, etc. as needed).
3. In the Blog section of `index.html`, wrap the matching card's title in a link:

   ```html
   <h3><a href="blog/plain-language-patient-materials.html">Plain Language in Patient Materials</a></h3>
   ```

## Changing the look

Colours, radius and shadow are CSS variables at the top of `styles.css`. Change `--teal` and `--teal-dark` to switch the accent colour. The font is the visitor's system font, so nothing is downloaded.

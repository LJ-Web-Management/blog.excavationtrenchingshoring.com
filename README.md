# blog.excavationtrenchingshoring.com

Blog for [excavationtrenchingshoring.com](https://excavationtrenchingshoring.com), with Word-document-to-blog-post publishing. Deployed via GitHub Pages.

## Structure

```
index.html            - blog home page (search/sort/pagination over posts.json)
posts.json             - generated index of all posts (title, slug, date, excerpt, image)
posts/                 - generated post HTML pages, one per post
assets/css/style.css   - site styling
assets/js/main.js      - home page rendering (search, sort, pagination)
assets/img/            - logo + per-post images (assets/img/posts/)
scripts/convert.js     - converts uploaded documents into blog posts
uploads/                - drop a .docx, .txt, or .zip here to publish a post
```

## Publishing a post

Add a file to `uploads/` on the `main` branch (via the GitHub web UI's "Add file" or a normal push) and push:

- `.docx` - a Word document. The first heading/paragraph becomes the title; the rest becomes the post body.
- `.txt` - a plain text file, same rules.
- `.zip` - a zip containing one `.docx`/`.txt` plus (optionally) one image file, which becomes the post's featured image.

Pushing a file under `uploads/*.docx`, `uploads/*.txt`, or `uploads/*.zip` triggers the **Convert Word Docs to Blog Posts** workflow, which:

1. Converts the document into `posts/<slug>.html`.
2. Adds an entry to `posts.json`.
3. Moves the source file into `uploads/processed/`.
4. Commits and pushes the result back to `main`.

That push then triggers the **Deploy to GitHub Pages** workflow, which republishes the site.

## Custom domain

A `CNAME` file pointing at `blog.excavationtrenchingshoring.com` is already committed. Once DNS for that subdomain is pointed at GitHub Pages (a `CNAME` record to `lj-web-management.github.io`), GitHub will automatically serve the site there and provision HTTPS. Until then, the site is reachable at the default `github.io` Pages URL.

## Local preview

```
npx serve .
```

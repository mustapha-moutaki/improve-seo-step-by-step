# 🚀 Website SEO & Performance Optimization Guide

A beginner-friendly guide to improving a modern React website for better SEO, speed, and Google Lighthouse scores.

This guide explains the steps taken to improve a portfolio website from:

**Before:**

- Performance: 76
- SEO: 77

**After:**

- Performance: 93
- Accessibility: 96
- Best Practices: 100
- SEO: 92

---

## 1. Create robots.txt

### Why?

Search engines like Google look for:

```
https://yourdomain.com/robots.txt
```

This file tells crawlers what they can access and where your sitemap exists.

Without it, Lighthouse may show:

```
robots.txt is not valid
```

### Create the file

For React + Vite:

Create:

```
public/robots.txt
```

Not inside `src`.

Structure:

```
project
│
├── public
│   └── robots.txt
│
├── src
│
└── package.json
```

Content:

```txt
User-agent: *
Allow: /

Sitemap: https://yourdomain.com/sitemap.xml
```

After deployment test:

```
https://yourdomain.com/robots.txt
```

---

## 2. Create sitemap.xml

### Why?

A sitemap helps Google discover your pages.

Example location:

```
public/sitemap.xml
```

Example content:

```xml
<?xml version="1.0" encoding="UTF-8"?>

<urlset xmlns="http://www.sitemaps.org/schemas/sitemap/0.9">

<url>
    <loc>https://yourdomain.com/</loc>
    <priority>1.0</priority>
    <changefreq>weekly</changefreq>
</url>

<url>
    <loc>https://yourdomain.com/blog</loc>
    <priority>0.8</priority>
</url>

</urlset>
```

Submit it in:

**Google Search Console → Sitemaps → Add sitemap**

---

## 3. Improve HTML metadata

Before:

```html
<title>My Website</title>
```

After:

```html
<title>
  Mustapha Moutaki — Full Stack Engineer
</title>

<meta
  name="description"
  content="Full Stack Engineer portfolio specializing in React, JavaScript and modern web development"
/>
```

### Why?

Google uses:

- Title
- Description

to understand your page.

---

## 4. Add Canonical URL

**Problem:**

Google may see multiple URLs as duplicates.

**Solution:**

```html
<link
  rel="canonical"
  href="https://yourdomain.com/"
/>
```

Every important page should have its own canonical URL.

---

## 5. Add Open Graph Metadata

Improves sharing previews.

Add:

```html
<meta property="og:title"
  content="Full Stack Engineer Portfolio"
/>

<meta property="og:description"
  content="Modern web development projects"
/>

<meta property="og:image"
  content="https://yourdomain.com/image.png"
/>

<meta property="og:url"
  content="https://yourdomain.com"
/>

<meta property="og:type"
  content="website"
/>
```

---

## 6. Add Robots Meta

Allow indexing:

```html
<meta
  name="robots"
  content="index,follow"
/>
```

---

## 7. Add Structured Data (JSON-LD)

### Why?

Helps Google understand your website.

Example for a developer:

```html
<script type="application/ld+json">
{
 "@context":"https://schema.org",
 "@type":"Person",
 "name":"Your Name",
 "jobTitle":"Full Stack Engineer",
 "url":"https://yourdomain.com"
}
</script>
```

**Important:**

Do NOT put JSON directly in HTML.

Wrong:

```
{
"name":"test"
}
```

Correct:

```html
<script type="application/ld+json">
{
"name":"test"
}
</script>
```

---

## 8. Dynamic SEO in React

For React applications, use:

```
react-helmet-async
```

Install:

```bash
npm install react-helmet-async
```

Example:

```jsx
<Helmet>
  <title>
    React Performance Guide
  </title>

  <meta
    name="description"
    content="Learn React optimization"
  />
</Helmet>
```

Now every page can have:

- Different title
- Different description
- Different URL

---

## 9. Fix Crawlable Links

Bad:

```jsx
<button onClick={()=>navigate('/projects')}>
  Projects
</button>
```

Google cannot crawl it.

Good:

```jsx
<a href="/projects">
  Projects
</a>
```

or React Router:

```jsx
<Link to="/projects">
  Projects
</Link>
```

---

## 10. Improve Link Text

Bad:

```jsx
<a href="/blog">
  Read more
</a>
```

Google does not know what "Read more" means.

Better:

```jsx
<a href="/blog/java-21">
  Read more about Java 21 Virtual Threads
</a>
```

---

## 11. Optimize Images

Large images hurt:

- LCP
- Performance

Instead of:

```
image.png
```

Use:

```
image.webp
```

or Cloudinary:

Before:

```
image/upload/photo.png
```

After:

```
image/upload/f_auto,q_auto,w_600/photo.png
```

Meaning:

- `f_auto` = automatic format
- `q_auto` = automatic compression
- `w_600` = resize width

---

## 12. Optimize LCP Image

The first important image should NOT use lazy loading.

Bad:

```jsx
<img
  loading="lazy"
/>
```

For the hero image:

Good:

```jsx
<img
  src="image.webp"
  fetchPriority="high"
  alt="Profile"
/>
```

---

## 13. Reduce JavaScript

Large JS bundles slow React apps.

Use lazy loading:

```jsx
const Blog =
  lazy(()=>import('./Blog'))
```

Instead of loading every page immediately.

---

## 14. Performance Checklist

**Before:**

- ❌ Large PNG images
- ❌ Missing robots.txt
- ❌ Non-crawlable buttons
- ❌ Generic "Read more" links
- ❌ No structured data
- ❌ Same metadata everywhere

**After:**

- ✅ robots.txt
- ✅ sitemap.xml
- ✅ optimized images
- ✅ dynamic SEO
- ✅ JSON-LD
- ✅ crawlable links
- ✅ optimized LCP
- ✅ smaller payload

---

## Final Lighthouse Result

**Target:**

- Performance: 90+
- SEO: 90+
- Accessibility: 90+
- Best Practices: 100

**Remember:**

A perfect Lighthouse score does not guarantee Google #1.

Real SEO also needs:

- Quality content
- Blog articles
- Internal linking
- Backlinks
- Regular updates

Technical SEO gets Google to understand your website.
Content makes Google rank it.

---

## 15. Bonus: Useful Additions

A few extra checks worth knowing about that build on the steps above:

### Verify in Google Search Console

After adding `robots.txt`, the canonical tag, and `sitemap.xml`, confirm everything is actually being read correctly:

- **URL Inspection tool** → check that a page is indexed and the canonical Google chose matches yours.
- **Sitemaps report** → confirms your sitemap was fetched and how many URLs were discovered vs indexed.
- **Page Indexing report** → flags pages excluded due to duplicate canonicals, noindex tags, or crawl errors.

### Preview Open Graph tags before deploying

Typos in `og:image` or `og:url` are easy to miss. Use a free checker like Meta's Sharing Debugger or opengraph.xyz to preview exactly how a link will look when shared on social platforms, before pushing to production.

### Core Web Vitals to watch beyond LCP

Lighthouse performance scores roll up several metrics worth tracking individually:

- **CLS (Cumulative Layout Shift)** — avoid layout jumps by always setting explicit `width`/`height` (or `aspect-ratio`) on images and embeds.
- **INP (Interaction to Next Paint)** — replaces FID as Google's responsiveness metric; heavy event handlers or large re-renders on click/tap can hurt this even if LCP looks great.
- **TBT (Total Blocking Time)** — a lab proxy for INP; code-splitting (step 13) directly helps here too.

### Font loading

Custom fonts can silently hurt both LCP and CLS. Two quick wins:

```html
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin />
```

```css
@font-face {
  font-family: "YourFont";
  src: url("/fonts/yourfont.woff2") format("woff2");
  font-display: swap;
}
```

`font-display: swap` prevents invisible text while the font loads, and `font-display: optional` can avoid layout shift entirely if a brief flash of fallback font is acceptable.

### robots.txt + sitemap submission isn't "set and forget"

Re-submit the sitemap in Search Console whenever you add a meaningful number of new pages (e.g. new blog posts), since Google doesn't always re-crawl it on its own schedule.

---

*Made with ❤️ while optimizing a React portfolio website.*

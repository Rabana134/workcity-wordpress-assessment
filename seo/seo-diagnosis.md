# SEO Technical Troubleshooting – Workcity Indexing Issue

A new Workcity brand website is not indexing even after submitting the sitemap in Google Search Console. This document provides a complete, senior-level technical SEO troubleshooting workflow to diagnose and resolve the issue.

---

## 1. Crawlability Tests

### 1.1 Google Search Console URL Inspection
- Enter the URL in "URL Inspection"
- Check crawl status, last crawl date, and whether Googlebot can access the page
- Look for errors like "Crawled – currently not indexed" or "Discovered – not indexed"

### 1.2 `site:` Operator Test
Search:
```
site:workcity.africa
```
If zero results appear, Google has not indexed any pages.

### 1.3 Live Test
Use "Test Live URL" in Search Console to verify real-time accessibility.

### 1.4 Check Response Codes
Use httpstatus.io, Screaming Frog, or curl to ensure pages return:
- `200 OK`

Not:
- `404 Not found`
- `500 server errors`
- Redirect loops
- `403 Forbidden`

---

## 2. Robots.txt Audit

### 2.1 Ensure Nothing Is Blocking Crawling
Visit:
```
https://workcity.africa/robots.txt
```
Make sure it does NOT contain:
```
Disallow: /
```

### 2.2 Sitemap Declaration
Your robots.txt should include:
```
Sitemap: https://workcity.africa/sitemap.xml
```

---

## 3. Meta Robots & No-Index Audit

### 3.1 Check Meta Tags in the HTML
Ensure none of these exist:

```html
<meta name="robots" content="noindex">
<meta name="robots" content="noindex,nofollow">
```

### 3.2 Check SEO Plugin Settings

Plugins that commonly block indexing:
- RankMath
- Yoast SEO
- Maintenance/Coming Soon plugins

Verify that global noindex isn't turned on.

### 3.3 Check HTTP Headers

Ensure headers do not contain:
```
X-Robots-Tag: noindex
```

---

## 4. Canonical Issues

### 4.1 Verify Canonicals

Ensure canonical URLs point to the correct version:
```html
<link rel="canonical" href="https://workcity.africa/page-url/">
```

### 4.2 Avoid Duplicate URL Versions

Check for:
- http vs https
- www vs non-www
- Trailing slash inconsistencies
- Parameterized duplicates like `?ref=`

---

## 5. Sitemap Structure Issues

### 5.1 Validate XML Sitemap

Submit:
```
https://workcity.africa/sitemap.xml
```

Check:
- All URLs load correctly
- No URLs return 301/302 redirects
- No errors inside the XML structure

### 5.2 Avoid Multiple Sitemaps

Using more than one sitemap provider (Yoast + RankMath + XML Sitemap plugin) causes confusion. Use only one.

### 5.3 Ensure New Pages Are Included

In Yoast or RankMath:
- Make sure pages/posts are marked as "Include in search results"

---

## 6. Page Speed & Crawl Budget Issues

### 6.1 Mobile Page Speed

Use PageSpeed Insights to evaluate:
- LCP (Largest Contentful Paint)
- CLS (Cumulative Layout Shift)
- FID (First Input Delay)

Extremely slow pages may delay indexing.

### 6.2 Remove Heavy Assets

Reduce:
- Unoptimized images
- Large JavaScript files
- Sliders
- Video backgrounds

### 6.3 Enable Caching

Recommended plugins:
- LiteSpeed Cache
- WP Super Cache
- W3 Total Cache

Faster pages get crawled more often.

---

## 7. Search Console Debugging Steps

### 7.1 Coverage Report

Check for:
- Crawled – not indexed
- Duplicate without user-selected canonical
- Alternate page with canonical tag
- Soft 404s

### 7.2 Manual Resubmission

Use "Request Indexing" in URL Inspection after fixing issues.

### 7.3 Server Log Review

Look for:
- Googlebot requests
- 403 or 500 errors
- Crawl blocks

### 7.4 Check for Penalties

Navigate to: **Search Console → Security & Manual Actions → Manual Actions**

Ensure Workcity did not receive any penalty.

---

## 8. Additional Considerations

### 8.1 Domain Age
New domains sometimes take longer to index.

### 8.2 Lack of Backlinks
Pages without external links may not get crawled quickly.

### 8.3 Poor Internal Linking
Ensure every important page is linked from:
- Homepage
- Menu
- Footer
- Other internal pages

### 8.4 Hreflang & International Targeting
If multilingual, ensure correct hreflang usage.

---

## 9. Final Checklist

- [ ] robots.txt allows crawling
- [ ] No accidental noindex tags
- [ ] No X-Robots-Tag blocking
- [ ] Canonicals correct
- [ ] Sitemap valid & submitted
- [ ] URLs return 200 status
- [ ] Page loads fast
- [ ] Internal links exist
- [ ] Plugins not blocking indexing
- [ ] External links/backlinks exist
- [ ] Search Console clear of errors

---

Following this troubleshooting workflow ensures that Workcity pages become crawlable, indexable, and visible in Google Search within the shortest possible time.
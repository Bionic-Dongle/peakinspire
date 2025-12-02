# PeakInspire Content Management System
**SEO-Optimized Static Site with Claude Project Integration**

---

## Directory Structure

```
PeakInspire/
├── content/                    # All blog posts organized by category
│   ├── health/                # health.peakinspire.com posts
│   ├── fitness/               # fitness.peakinspire.com posts
│   ├── wealth/                # wealth.peakinspire.com posts
│   ├── clarity/               # clarity.peakinspire.com posts
│   ├── local/                 # local.peakinspire.com posts
│   ├── systems/               # systems.peakinspire.com posts
│   └── content-index.json     # Master index of all posts (for Claude Project)
├── Templates/                  # HTML templates
│   └── seo-post-template.html # SEO-complete post template
├── Images/                     # Site images
├── global.css                  # Global styles
├── card.css                    # Card/post styles
└── index.html                  # Homepage

```

---

## File Naming Convention

**Format:** `YYYY-MM-DD-slug-title.html`

**Examples:**
- `2025-12-02-fixing-knee-pain-after-50.html`
- `2025-12-03-melbourne-hidden-coffee-gems.html`
- `2025-12-05-rebuilding-wealth-at-55.html`

**Why this format:**
- **Chronological sorting** - Files sort by date automatically
- **SEO-friendly** - Descriptive URLs
- **Easy to find** - Scan by date or topic
- **No conflicts** - Date prevents duplicate titles

---

## Creating a New Post

### 1. Daily Workflow (Bullet Points → Published Post)

**In Claude Project:**
```
Me: "Health post today - bullet points:
- Tried glucosamine for 2 weeks
- Joint pain reduced 40%
- Morning stiffness gone
- Cost $25/month
- Side effects: none
- Recommend brand XYZ"

Claude: [Refines into full article with:]
- SEO-optimized title
- Meta description
- Keywords
- Internal links to related posts
- Structured content
- Saves to content/health/2025-12-02-glucosamine-results.html
- Updates content-index.json
```

### 2. Template Placeholders

Replace these in `seo-post-template.html`:

| Placeholder | Example | Description |
|------------|---------|-------------|
| `{{ARTICLE_TITLE}}` | "Glucosamine After 50: My 2-Week Results" | Main headline |
| `{{META_DESCRIPTION}}` | "I tested glucosamine for 2 weeks. Here's what happened to my knee pain, morning stiffness, and mobility. Real results, no BS." | 150-160 chars |
| `{{KEYWORDS}}` | "glucosamine, joint pain relief, knee pain after 50, supplements for men" | Comma-separated |
| `{{CATEGORY_NAME}}` | "Health & Vitality" | Full category name |
| `{{SUBDOMAIN}}` | "health.peakinspire.com" | Category subdomain |
| `{{CANONICAL_URL}}` | "https://health.peakinspire.com/2025-12-02-glucosamine-results" | Full post URL |
| `{{OG_IMAGE_URL}}` | "https://health.peakinspire.com/images/glucosamine-og.jpg" | Social share image |
| `{{PUBLISH_DATE_ISO}}` | "2025-12-02T09:00:00+11:00" | ISO 8601 format |
| `{{MODIFIED_DATE_ISO}}` | "2025-12-02T09:00:00+11:00" | ISO 8601 format |
| `{{PUBLISH_DATE_HUMAN}}` | "December 2, 2025" | Readable format |
| `{{MODIFIED_DATE_HUMAN}}` | "December 2, 2025" | Readable format |
| `{{TAGS}}` | "joint pain, supplements, health" | For article:tag schema |
| `{{ARTICLE_CONTENT}}` | `<p>Two weeks ago...</p>` | Full HTML content |
| `{{INTERNAL_LINKS}}` | `<li><a href="...">Related post</a></li>` | Links to related posts |

### 3. SEO Elements Included

✅ **Meta Tags:**
- Title, description, keywords
- Author, canonical URL
- Open Graph (Facebook sharing)
- Twitter Cards

✅ **Schema.org Structured Data:**
- Article schema (tells Google it's a blog post)
- Breadcrumb schema (navigation path)
- Author/publisher info
- Dates and categories

✅ **Semantic HTML:**
- Proper heading hierarchy (H1 → H2 → H3)
- `<article>` tags with microdata
- `<time>` tags for dates
- Breadcrumb navigation

✅ **Internal Linking:**
- Related articles section (auto-suggested by Claude)
- Category navigation
- Breadcrumb links

---

## Content Index System

`content/content-index.json` tracks ALL posts for Claude Project context.

**Structure:**
```json
{
  "categories": {
    "health": {
      "posts": [
        {
          "title": "Glucosamine After 50: My 2-Week Results",
          "slug": "2025-12-02-glucosamine-results",
          "url": "https://health.peakinspire.com/2025-12-02-glucosamine-results",
          "date": "2025-12-02",
          "keywords": ["glucosamine", "joint pain", "supplements"],
          "internal_links_to": ["knee-pain-solutions", "supplements-worth-buying"],
          "internal_links_from": []
        }
      ]
    }
  },
  "internal_links": {
    "glucosamine": ["2025-12-02-glucosamine-results"],
    "joint pain": ["2025-12-02-glucosamine-results", "2025-11-15-knee-pain-solutions"]
  }
}
```

**Claude uses this to:**
- Suggest internal links while writing
- Avoid duplicate topics
- Build topic clusters
- Track keyword usage
- Generate related posts sections

---

## Claude Project Setup

### Custom Instructions for Claude Project

```
PROJECT: PeakInspire Life Documentation CMS
ROOT PATH: C:\Users\chipp\Desktop\version control\PeakInspire - Copy\

WRITING STYLE:
- Direct, conversational Melbourne bloke in late 50s
- Honest, slightly irreverent, zero fluff
- Personal experience > theory
- Short paragraphs, easy scanning

INPUT FORMAT: 
Raw bullet points from daily life (voice notes, quick text)

OUTPUT FORMAT:
1. SEO-optimized blog post HTML (using seo-post-template.html)
2. All meta tags, schema, Open Graph filled in
3. Internal links suggested based on content-index.json
4. Saved to appropriate content/{category}/ folder
5. content-index.json updated with new post

WORKFLOW:
1. User dumps bullet points + indicates category
2. I refine into 400-800 word post
3. I suggest 2-3 internal links from existing posts
4. I generate all SEO metadata
5. I save post with proper filename (YYYY-MM-DD-slug.html)
6. I update content-index.json
7. I confirm: "Post published to {category}.peakinspire.com/{slug}"

CONTEXT FILES TO LOAD:
- content/content-index.json (always check for existing posts)
- Templates/seo-post-template.html (base template)
- Current category index page (for linking)

NEVER:
- Sanitize the voice (keep it real)
- Skip SEO elements (they're non-negotiable)
- Create posts without updating index
- Guess internal links (check index first)
```

### Example Interaction

```
You: "Health category - tried new back brace today:
- Reduced lower back pain 60%
- Wore for 4 hours
- Cost $45
- Breathable material
- Recommend for gardening/DIY"

Claude: 
✅ Created: content/health/2025-12-02-back-brace-review.html
📝 Title: "This $45 Back Brace Saved My Weekend Gardening"
🔗 Internal links: 
   - /health/2025-11-20-lower-back-pain-solutions
   - /health/2025-10-15-diy-safety-tips-after-50
📊 Keywords: back brace, lower back pain, gardening safety, pain relief
🌐 URL: https://health.peakinspire.com/2025-12-02-back-brace-review
✅ content-index.json updated

Post ready for deployment. Want to review before publishing?
```

---

## Deployment Workflow

### Option 1: Vercel (Recommended)

1. **Initial Setup:**
   - Push to GitHub: `git push origin main`
   - Connect GitHub repo to Vercel dashboard
   - Add domain: peakinspire.com
   - Configure subdomains in Vercel

2. **Daily Publishing:**
   - Claude creates post in `content/{category}/`
   - You review/edit if needed
   - `git add . && git commit -m "New post: {title}"`
   - `git push origin main`
   - Vercel auto-deploys in 30 seconds

### Option 2: A2 Hosting

1. Upload via FTP/cPanel File Manager
2. Manual placement in category folders
3. Update sitemap.xml manually

---

## SEO Checklist (Automated by Template)

✅ Title tag (unique, descriptive, <60 chars)
✅ Meta description (compelling, <160 chars)
✅ H1 tag (matches title)
✅ Heading hierarchy (H1 → H2 → H3)
✅ Alt text on images
✅ Internal links (2-5 per post)
✅ Canonical URL
✅ Schema.org markup (Article + Breadcrumb)
✅ Open Graph tags (social sharing)
✅ Mobile-responsive (inherited from global.css)
✅ Fast loading (static HTML)
✅ HTTPS (Vercel auto, or Let's Encrypt on A2)

---

## Sitemap Generation

After every 5-10 posts, update `sitemap.xml`:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<urlset xmlns="http://www.sitemaps.org/schemas/sitemap/0.9">
  <url>
    <loc>https://peakinspire.com/</loc>
    <lastmod>2025-12-02</lastmod>
    <priority>1.0</priority>
  </url>
  <url>
    <loc>https://health.peakinspire.com/2025-12-02-glucosamine-results</loc>
    <lastmod>2025-12-02</lastmod>
    <priority>0.8</priority>
  </url>
</urlset>
```

Submit to Google Search Console.

---

## robots.txt

Already created at root:

```
User-agent: *
Allow: /
Sitemap: https://peakinspire.com/sitemap.xml
```

---

## Internal Linking Strategy

**Claude automatically suggests links based on:**

1. **Keyword matching** - If new post mentions "joint pain", suggest posts tagged with "joint pain"
2. **Category relevance** - Prioritize same-category posts
3. **Recency** - Mix older and newer posts (avoid only linking to recent)
4. **Depth** - Aim for 2-5 internal links per post
5. **Anchor text** - Natural, keyword-rich (e.g., "my glucosamine experiment" not "click here")

**Example in practice:**

New post about "Morning Mobility Routine" might link to:
- "Glucosamine Results" (keyword: joint pain)
- "Stretching After 50" (category: health, topic: flexibility)
- "My Daily Health Stack" (category: health, topic: supplements)

---

## Success Metrics

**Track these in Google Search Console / Analytics:**

- Organic traffic growth
- Average time on page (target: 2+ minutes)
- Bounce rate (target: <60%)
- Internal link click-through rate
- Pages indexed by Google
- Keyword rankings (monitor your primary topics)

---

## Maintenance Schedule

**Daily:**
- Create 1 post (bullet points → refined → published)

**Weekly:**
- Review internal linking opportunities
- Update older posts with new links
- Check broken links

**Monthly:**
- Update sitemap.xml
- Review keyword performance
- Add image alt text if missing

---

## Next Steps

1. ✅ **Created:** Content structure, templates, index system
2. ⏳ **TODO:** Set up Claude Project with custom instructions
3. ⏳ **TODO:** Create first test post to verify workflow
4. ⏳ **TODO:** Deploy to Vercel
5. ⏳ **TODO:** Submit sitemap to Google Search Console
6. ⏳ **TODO:** Start daily documentation habit

---

## Questions?

This system is designed for:
- **Speed** - Bullet points → published in minutes
- **SEO** - Every technical requirement baked in
- **Context** - Claude knows all your content for smart linking
- **Simplicity** - No CMS complexity, just files and Git

The perfectionism blocker is removed. Just document life, Claude handles the rest.

# GitHub Copilot Instructions - Uriel Ofir's Personal Website

## Project Context
This is Uriel Ofir's personal website - a Docsy-based Hugo static site showcasing his work, projects, blog posts, podcasts, videos, and personal journey. Uriel is the founder of Ma'akaf (Israeli open-source community) and a passionate JavaScript developer. Follow Hugo and Docsy best practices when generating code.

## Hugo Configuration (hugo.yaml)

### Main Configuration Structure
```yaml
baseURL: "/"
title: "Uriel Ofir"
languageCode: "en-us"
defaultContentLanguage: "en"

# Hugo Configuration
enableRobotsTXT: true
enableGitInfo: true
enableMissingTranslationPlaceholders: true

# Theme
theme: ["docsy"]
# For local development with workspace
# workspace: docsy.work

# Content and Language Configuration
contentDir: "content/en"
defaultContentLanguageInSubdir: false

# Taxonomies
taxonomies:
  tag: tags
  category: categories

# Permalink structure
permalinks:
  blog: /:section/:year/:month/:day/:slug/

# Image processing
imaging:
  resampleFilter: CatmullRom
  quality: 75
  anchor: smart

# Markup Configuration
markup:
  goldmark:
    parser:
      attribute:
        block: true
    renderer:
      unsafe: true
  highlight:
    style: tango
    # guessSyntax: true for auto-detection

# Language Configuration
languages:
  en:
    languageName: "English"
    title: "Uriel Ofir"
    params:
      description: "Uriel Ofir's personal website, showcasing his work, projects, and interests."
      ui:
        showLightDarkModeMenu: true

# Output formats
outputs:
  section: [HTML, print, RSS]

# Docsy Theme Parameters
params:
  # GitHub Configuration
  github_repo: "https://github.com/UrielOfir/personal-website"
  github_branch: "main"
  
  # Personal Website Configuration
  privacy_policy: "https://policies.google.com/privacy"
  version_menu: "Releases"
  archived_version: false
  version: "0.0"
  
  # Google Analytics
  google_analytics: "G-5BMKYN51XV"
  
  # Taxonomy Configuration
  taxonomy:
    taxonomyCloud: [tags, categories]
    taxonomyCloudTitle: [Tag Cloud, Categories]
    taxonomyPageHeader: [tags, categories]
  
  # UI Configuration
  ui:
    breadcrumb_disable: false
    navbar_logo: true
    navbar_translucent_over_cover_disable: false
    sidebar_menu_compact: false
    sidebar_search_disable: false
    feedback:
      enable: true
      'yes': >-
        Glad to hear it! Please <a href="https://github.com/UrielOfir/personal-website/issues/new">tell us how we can improve</a>.
      'no': >-
        Sorry to hear that. Please <a href="https://github.com/UrielOfir/personal-website/issues/new">tell us how we can improve</a>.
    readingtime:
      enable: false
    
  # Social Links - Uriel's Personal Profiles
  links:
    user:
      - name: "YouTube"
        url: "https://www.youtube.com/@UrielOfir"
        icon: "fa-brands fa-youtube"
        desc: "My YouTube channel"
      - name: "LinkedIn"
        url: "https://www.linkedin.com/in/uriel-ofir/"
        icon: "fa-brands fa-linkedin"
        desc: "Connect with me on LinkedIn"
      - name: "TikTok"
        url: "https://www.tiktok.com/@urielofir"
        icon: "fa-brands fa-tiktok"
        desc: "My TikTok profile"
      - name: "Telegram"
        url: "https://t.me/thinking_together_israel"
        icon: "fa-brands fa-telegram"
        desc: "Join our Telegram channel"
    developer:
      - name: "GitHub"
        url: "https://github.com/UrielOfir/personal-website"
        icon: "fa-brands fa-github"
        desc: "Development takes place here!"
      - name: "Facebook"
        url: "https://www.facebook.com/urielofir86"
        icon: "fa-brands fa-facebook"
        desc: "My Facebook profile"
      - name: "X (Twitter)"
        url: "https://x.com/OfirUriel"
        icon: "fa-brands fa-x-twitter"
        desc: "My X profile"
      - name: "Instagram"
        url: "https://www.instagram.com/uriel__ofir/"
        icon: "fa-brands fa-instagram"
        desc: "My Instagram profile"

# Google Analytics configuration
services:
  googleAnalytics:
    id: G-5BMKYN51XV

# Module Configuration (for Hugo Modules)
module:
  hugoVersion:
    extended: true
    min: 0.110.0
  imports:
    - path: "github.com/google/docsy"
      disable: false
```

### Configuration Best Practices
- Use proper `baseURL` configuration ("/" for development, full URL for production)
- Configure content structure with proper permalink patterns
- Enable Git info for content versioning and last modified dates
- Set up proper taxonomy structure for blog posts (tags and categories)
- Configure image processing for optimal performance
- Set up Google Analytics integration
- Maintain social media links and contact information

### Environment-Specific Configuration
**config/production/hugo.yaml:**
```yaml
baseURL: "https://urielofir.dev"  # Replace with your actual domain
enableRobotsTXT: true
canonifyURLs: true

params:
  ui:
    feedback:
      enable: true
  google_analytics: "G-5BMKYN51XV"
```

**config/development/hugo.yaml:**
```yaml
baseURL: "/"
enableRobotsTXT: false
disableKinds: ["sitemap", "robotsTXT"]

markup:
  goldmark:
    renderer:
      unsafe: true
  highlight:
    noClasses: false
```

## Hugo/Docsy Specific Guidelines

### Content Structure
- Use proper Hugo front matter in YAML format
- Follow Docsy content organization patterns
- Generate content in appropriate sections (`content/en/blog/`, `content/en/about/`, `content/en/podcasts-and-videos/`, `content/en/technical/`)
- Use Hugo's page bundles for complex content with images and resources
- Support both Hebrew and English content with proper language organization

### Front Matter Standards
```yaml
---
title: "Page Title"
linkTitle: "Short Title"
weight: 10
description: >
  Brief description of the page content
---
```

### Shortcode Usage
- Prefer Docsy built-in shortcodes over custom HTML
- Use `{{< alert >}}`, `{{< pageinfo >}}`, `{{< tabpane >}}` appropriately
- Generate responsive image shortcodes: `{{< imgproc >}}`
- Use code highlighting: `{{< highlight lang >}}`

### Layout and Templating

**Hugo Template Patterns:**
```go
{{ range .Pages }}
  <article class="card">
    <h2><a href="{{ .RelPermalink }}">{{ .Title }}</a></h2>
    <p>{{ .Summary }}</p>
  </article>
{{ end }}
```

**Partial Templates:**
- Create reusable partials in `layouts/partials/`
- Use semantic HTML5 elements
- Include proper ARIA attributes for accessibility
- Follow Docsy's CSS class conventions

### Content Guidelines
- Write in Markdown with proper heading hierarchy (H1 → H6)
- Use Hugo's built-in image processing
- Implement proper cross-references with `{{< ref >}}` and `{{< relref >}}`
- Include proper meta descriptions and SEO tags

### Styling and Assets
- Use Hugo Pipes for asset processing
- Follow Docsy's SCSS structure in `assets/scss/`
- Implement responsive design patterns
- Use Bootstrap 4/5 classes (Docsy's base framework)

### Multilingual Support
- Structure content with language codes (`content/en/` for English content)
- Support Hebrew blog posts in dedicated subdirectories  
- Use proper language configuration in front matter
- Implement i18n strings in `i18n/` directory for interface translations
- Generate language-aware navigation and permalinks

### Performance and SEO
- Optimize images with Hugo's image processing
- Generate proper structured data (JSON-LD)
- Implement lazy loading for images
- Use Hugo's minification and bundling
- Generate proper sitemap and robots.txt

### Quality Checklist for Hugo/Docsy
Before suggesting code, ensure it:
- [ ] Uses proper Hugo syntax and functions
- [ ] Follows Docsy theme conventions
- [ ] Includes responsive design
- [ ] Has proper front matter
- [ ] Uses semantic HTML
- [ ] Includes accessibility features
- [ ] Optimizes for performance
- [ ] Works with Hugo's build process
- [ ] Follows content structure guidelines
- [ ] Includes proper navigation integration
- [ ] Respects hugo.yaml configuration settings

## Common Hugo Functions to Use
- `{{ .Title }}`, `{{ .Content }}`, `{{ .Summary }}`
- `{{ range .Pages }}`, `{{ with .Params.param }}`
- `{{ partial "name" . }}`, `{{ block "name" . }}`
- `{{ .RelPermalink }}`, `{{ .Permalink }}`
- `{{ dateFormat "2006-01-02" .Date }}`
- `{{ .Site.BaseURL }}`, `{{ .Site.Params.param }}`
- `{{ .Site.Language.Lang }}`, `{{ i18n "key" }}`
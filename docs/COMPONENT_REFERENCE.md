# Component Reference Guide

## Jekyll Layout Components

### Presentation Layout
**File:** `_layouts/presentation.html`

**Purpose:** Main layout for multi-slide presentations with full Reveal.js integration.

**Properties:**
- **Theme Support:** Dynamic theme switching via `site.solarized.theme`
- **Content Injection:** Uses `{{ content }}` for slide content
- **Automatic Includes:** Integrates head and script components

**Usage:**
```yaml
---
layout: presentation
---
```

**Output Structure:**
```html
<!DOCTYPE html>
<html class="dark|light">
  <head>{% include head.html %}</head>
  <body>
    <div class="reveal">
      <div class="slides">
        {{ content }}
      </div>
    </div>
    {% include script.html %}
  </body>
</html>
```

**Customization Points:**
- Override `_includes/head.html` for custom head content
- Override `_includes/script.html` for custom JavaScript
- Modify HTML classes via `site.solarized.theme` configuration

---

### Slide Layout
**File:** `_layouts/slide.html`

**Purpose:** Simplified layout for individual slide viewing and testing.

**Properties:**
- **Lightweight:** Minimal HTML structure
- **Standalone:** Self-contained slide rendering
- **Development-Friendly:** Ideal for slide prototyping

**Usage:**
```yaml
---
layout: slide
title: "Individual Slide"
---
```

**Output Structure:**
```html
<!DOCTYPE html>
<html>
  <head>{% include head.html %}</head>
  <body>
    <div class="reveal">
      <div class="step">
        {{ content }}
      </div>
    </div>
  </body>
</html>
```

**Use Cases:**
- Single slide development
- Slide preview and testing
- Embedded slide components

---

### Print Layout
**File:** `_layouts/print.html`

**Purpose:** Print-optimized layout for PDF generation and physical printing.

**Properties:**
- **Print-Optimized:** Removes interactive elements
- **Static Rendering:** No JavaScript dependencies
- **PDF Compatible:** Works with print-pdf URL parameter

**Usage:**
```yaml
---
layout: print
---
```

**Output Structure:**
```html
<!DOCTYPE html>
<html>
  <head>{% include head.html %}</head>
  <body>
    <div class="reveal">
      {{ content }}
    </div>
  </body>
</html>
```

**Print Generation:**
```bash
# Generate PDF
curl "http://localhost:4000/?print-pdf" > presentation.html
# Convert to PDF using headless browser
```

---

## Jekyll Include Components

### Head Component
**File:** `_includes/head.html`

**Purpose:** Manages HTML head section with dynamic title generation and asset loading.

**Features:**
- **Dynamic Titles:** Context-aware title generation
- **Reveal.js Assets:** Automatic CSS loading
- **Print Support:** Dynamic print CSS injection
- **Responsive Meta:** Mobile-optimized viewport

**Title Generation Logic:**
```liquid
{% if post.title %}
  {{ post.title }} | {{ page.title }}
{% else %}
  {{ site.title }}
{% endif %}
```

**Asset Loading:**
- `reveal.css` - Core Reveal.js styles
- `reset.css` - CSS reset
- `moon.css` - Default theme
- `monokai.css` - Syntax highlighting

**Print Detection:**
```javascript
var link = document.createElement('link');
link.rel = 'stylesheet';
link.type = 'text/css';
link.href = window.location.search.match(/print-pdf/gi) ? 
  'css/print/pdf.css' : 
  'node_modules/reveal.js/css/print/paper.css';
document.getElementsByTagName('head')[0].appendChild(link);
```

**Customization:**
```html
<!-- Custom head include -->
<meta name="author" content="{{ site.author }}">
<meta name="description" content="{{ site.description }}">
<link rel="stylesheet" href="assets/css/custom.css">
```

---

### Script Component
**File:** `_includes/script.html`

**Purpose:** Handles Reveal.js initialization and plugin configuration.

**Plugin Dependencies:**
- **Markdown Support:** `marked.js` + `markdown.js`
- **Syntax Highlighting:** `highlight.js`
- **Speaker Notes:** `notes.js`

**Initialization Configuration:**
```javascript
Reveal.initialize({
  hash: true,  // URL hash navigation
  dependencies: [
    { src: 'node_modules/reveal.js/plugin/markdown/marked.js' },
    { src: 'node_modules/reveal.js/plugin/markdown/markdown.js' },
    { src: 'node_modules/reveal.js/plugin/highlight/highlight.js' },
    { src: 'node_modules/reveal.js/plugin/notes/notes.js', async: true }
  ]
});
```

**Extension Points:**
```javascript
// Add custom plugins
Reveal.initialize({
  dependencies: [
    // ... existing plugins
    { src: 'assets/js/plugins/custom-plugin.js', async: true },
    { src: 'assets/js/plugins/math.js', condition: function() { 
      return !!document.querySelector('[data-math]'); 
    }}
  ]
});
```

**Event Handling:**
```javascript
// Custom event listeners
Reveal.addEventListener('slidechanged', function(event) {
  console.log('Current slide:', event.currentSlide);
});
```

---

### Slide Component
**File:** `_includes/slide.html`

**Purpose:** Renders individual slide content with advanced configuration options.

**Template Logic:**
```liquid
<section {% if post.slide-id %}id="{{post.slide-id}}"{%endif %} 
         class="step{%if post.classes | size %}{% for class in post.classes %} {{class}}{% endfor %}{% else %} slide{% endif %}" 
         {% unless site.simple-slideshow %}{% for attr in post.data %} data-{{attr[0]}}="{{attr[1]}}"{% endfor %}{% endunless %}>
  {% if post.title != "" %}<h1>{{ post.title }}</h1>{% endif %}
  {{ post.content }}
</section>
```

**Configuration Options:**

**Slide ID:**
```yaml
slide-id: "unique-identifier"
```
Output: `<section id="unique-identifier">`

**CSS Classes:**
```yaml
classes:
  - "title-slide"
  - "centered"
  - "dark-background"
```
Output: `<section class="step title-slide centered dark-background">`

**Data Attributes:**
```yaml
data:
  background-color: "#ff0000"
  transition: "zoom"
  x: "1000"
  y: "500"
  rotate: "45"
  scale: "2"
```
Output: `<section data-background-color="#ff0000" data-transition="zoom" data-x="1000">`

**Conditional Rendering:**
- Title renders only if `post.title` is not empty
- Data attributes only render unless `site.simple-slideshow` is true
- Classes default to "slide" if no custom classes specified

---

## Build Script Components

### Setup Script
**File:** `script/setup`

**Purpose:** Environment initialization and dependency management.

**Functions:**

**Homebrew Detection (macOS):**
```bash
if [ -f "Brewfile" ] && [ "$(uname -s)" = "Darwin" ]; then
  brew bundle check >/dev/null 2>&1 || {
    echo "==> Installing Homebrew dependencies…"
    brew bundle
  }
fi
```

**Ruby Version Management:**
```bash
if [ -f ".ruby-version" ] && [ -z "$(rbenv version-name 2>/dev/null)" ]; then
  echo "==> Installing Ruby…"
  rbenv install --skip-existing
  which bundle >/dev/null 2>&1 || {
    gem install bundler
    rbenv rehash
  }
fi
```

**Gem Installation:**
```bash
if [ -f "Gemfile" ]; then
  echo "==> Installing gem dependencies…"
  bundle install --no-cache --quiet --without production
fi
```

**Submodule Initialization:**
```bash
git submodule update --init
```

**Usage:**
```bash
./script/setup
```

**Error Handling:**
- Uses `set -e` for immediate exit on error
- Conditional checks prevent unnecessary operations
- Descriptive output for each operation

---

### Server Script
**File:** `script/server`

**Purpose:** Development server management with Jekyll serve wrapper.

**Functionality:**
```bash
#!/bin/sh
set -e
bundle exec jekyll serve "$@"
```

**Usage Examples:**
```bash
./script/server                    # Default: localhost:4000
./script/server --port 4001        # Custom port
./script/server --incremental      # Faster rebuilds
./script/server --livereload       # Auto-refresh
./script/server --drafts           # Include draft posts
./script/server --host 0.0.0.0     # External access
```

**Features:**
- Passes all arguments to Jekyll serve
- Automatic reloading on file changes
- Development-optimized settings
- Error propagation with `set -e`

---

### CI Build Script
**File:** `script/cibuild`

**Purpose:** Continuous integration build and validation.

**Build Process:**
```bash
#!/bin/sh
set -e
bundle exec jekyll build --baseurl "."
htmlproofer _site/index.html --empty-alt-ignore
```

**Validation Steps:**
1. **Jekyll Build:** Generate static site with relative baseurl
2. **HTML Validation:** Check markup with HTMLProofer
3. **Link Checking:** Verify internal and external links
4. **Image Validation:** Ensure images load correctly

**HTMLProofer Options:**
- `--empty-alt-ignore`: Skip empty alt attribute warnings
- `--check-html`: Validate HTML markup
- `--check-img-http`: Verify image URLs

**Exit Codes:**
- `0`: Build and validation successful
- `1`: Build failed or validation errors found

**CI Integration:**
```yaml
# GitHub Actions example
- name: Build and test
  run: ./script/cibuild
```

---

### Stage Script
**File:** `script/stage`

**Purpose:** Staging environment deployment automation.

**Configuration:**
```bash
account='training-staging'
repo=${1:-"caption-this"}  # Default or parameter
```

**Deployment Process:**

**1. Build with Staging Config:**
```bash
DISABLE_WHITELIST=1 bundle exec jekyll build --baseurl "/${account}/${repo}"
```

**2. Temporary Git Repository:**
```bash
cd _site && 
git init && 
git remote add staging https://ghe.io/${account}/${repo}.git && 
git add . && 
git commit -m "Staging latest changes"
```

**3. Deploy to GitHub Pages:**
```bash
git push staging master:gh-pages --force && 
git remote rm staging
```

**4. Open Staging Site:**
```bash
open https://pages.ghe.io/${account}/${repo}/
```

**Usage:**
```bash
./script/stage                     # Deploy to default repo
./script/stage my-presentation     # Deploy to specific repo
```

**Requirements:**
- GitHub Enterprise Server access
- Git credentials configured
- Write access to staging repository

---

## Configuration Components

### Jekyll Configuration
**File:** `_config.yml`

**Core Settings:**
```yaml
# Site identity
title: "Presentation Title"
author: "Author Name"
description: "Presentation description"

# Build settings
markdown: kramdown
highlighter: rouge
plugins:
  - jemoji

# Permalink structure
permalink: "/:title"
```

**Reveal.js Integration:**
```yaml
reveal:
  controls: false
  progress: true
  history: true
  center: true
  transition: "linear"
  width: 1000
  height: 920
  margin: 0.1
```

**Theme Configuration:**
```yaml
solarized:
  theme: "dark"  # or "light"

slideNumber:
  format: "c/t"
```

**Build Exclusions:**
```yaml
exclude:
  - "Gemfile"
  - "Gemfile.lock"
  - "vendor"
  - "reveal.js/test"
  - "reveal.js/README.md"
```

### Package Configuration
**File:** `package-lock.json`

**Dependencies:**
```json
{
  "requires": true,
  "lockfileVersion": 1,
  "dependencies": {
    "reveal.js": {
      "version": "3.9.2",
      "resolved": "https://registry.npmjs.org/reveal.js/-/reveal.js-3.9.2.tgz",
      "integrity": "sha512-Dvv2oA9FrtOHE2DWj5js8pMRfwq++Wmvsn1EyAdYLC80lBjTphns+tPsB652Bnvep9AVviuVS/b4XoVY9rXHLA=="
    }
  }
}
```

**Usage:**
- Locks Reveal.js version for consistency
- Ensures reproducible builds
- Compatible with npm/yarn workflows

---

## Content Components

### Post Structure
**Location:** `_posts/YYYY-MM-DD-title.md`

**Front Matter Schema:**
```yaml
---
layout: slide                 # Required
title: "Slide Title"          # Required
slide-id: "custom-id"         # Optional
classes:                      # Optional array
  - "class-name"
data:                         # Optional object
  attribute: "value"
---
```

**Content Processing:**
- **Markdown:** Standard GitHub Flavored Markdown
- **Liquid:** Jekyll templating available
- **HTML:** Direct HTML insertion supported
- **Fragments:** Reveal.js fragment syntax

**Example Post:**
```markdown
---
layout: slide
title: "Advanced Features"
slide-id: "features"
classes:
  - "feature-slide"
data:
  background-color: "#2c3e50"
  transition: "zoom"
---

## Key Features

- Performance <!-- .element: class="fragment fade-in" -->
- Security <!-- .element: class="fragment fade-in" -->
- Scalability <!-- .element: class="fragment fade-in" -->

Note: These are the three pillars of our architecture.
```

### Index Structure
**File:** `index.html`

**Template Logic:**
```liquid
---
layout: presentation
---

{% for post in site.posts reversed %}
  {% include slide.html %}
  <div class="page-break"></div>
{% endfor %}

{% unless site.simple-slideshow %}
{% if site.overview %}
<section id="overview" class="step" 
  {% for attr in site.overview-data %} 
    data-{{attr[0]}}="{{attr[1]}}"
  {% endfor %}>
</section>
{% endif %}
{% endunless %}
```

**Features:**
- **Post Iteration:** Processes all posts in reverse chronological order
- **Slide Inclusion:** Uses slide component for rendering
- **Page Breaks:** Adds print-friendly page breaks
- **Overview Support:** Optional overview slide generation

This component reference provides detailed documentation for every major component in the Jekyll slideshow framework, including their properties, methods, configuration options, and usage patterns.
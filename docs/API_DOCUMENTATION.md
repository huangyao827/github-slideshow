# GitHub Slideshow - Comprehensive API Documentation

## Table of Contents

1. [Overview](#overview)
2. [Configuration API](#configuration-api)
3. [Layout Components](#layout-components)
4. [Include Components](#include-components)
5. [Build Scripts API](#build-scripts-api)
6. [Content Creation API](#content-creation-api)
7. [Customization Guide](#customization-guide)
8. [Deployment API](#deployment-api)
9. [Examples and Usage](#examples-and-usage)

---

## Overview

The GitHub Slideshow is a Jekyll-based presentation framework built on top of [Reveal.js](https://github.com/hakimel/reveal.js/). It provides a simple way to create beautiful, interactive slideshow presentations using Markdown and Jekyll's templating system.

### Core Features

- **Markdown-based slides**: Write slides using simple Markdown syntax
- **Multiple layout options**: Presentation, slide, and print layouts
- **Reveal.js integration**: Full access to Reveal.js features and plugins
- **Responsive design**: Works on desktop and mobile devices
- **Print support**: Generate PDF exports of presentations
- **Theme customization**: Built-in theme support with Solarized variants
- **Progressive enhancement**: Graceful degradation for accessibility

---

## Configuration API

The slideshow can be configured through `_config.yml`. All configuration options are documented below.

### Site Configuration

```yaml
# Basic site settings
title: "My Presentation"           # Site title (required)
author: "Your Name"                # Author name (optional)
description: "Presentation description"  # Site description (optional)

# Jekyll settings
timezone: "Europe/Berlin"          # Timezone for date handling
baseurl: "/my-presentation"        # Base URL path (optional)
```

### Reveal.js Configuration

Configure Reveal.js behavior through the `reveal` section:

```yaml
reveal:
  # Display controls in the bottom right corner
  controls: false                  # boolean (default: false)
  
  # Display a presentation progress bar
  progress: true                   # boolean (default: true)
  
  # Push each slide change to the browser history
  history: true                    # boolean (default: true)
  
  # Enable keyboard shortcuts for navigation
  keyboard: true                   # boolean (default: true)
  
  # Enable the slide overview mode
  overview: true                   # boolean (default: true)
  
  # Vertical centering of slides
  center: true                     # boolean (default: true)
  
  # Enables touch navigation on devices with touch input
  touch: true                      # boolean (default: true)
  
  # Loop the presentation
  loop: false                      # boolean (default: false)
  
  # Turns fragments on and off globally
  fragments: true                  # boolean (default: true)
  
  # Transition style
  transition: "linear"             # string: default/cube/page/concave/zoom/linear/fade/none
  
  # Transition style for full page slide backgrounds
  backgroundTransition: "slide"    # string: default/none/slide/concave/convex/zoom
  
  # Presentation dimensions
  width: 1000                      # number (default: 1000)
  height: 920                      # number (default: 920)
  margin: 0.1                      # number (default: 0.1)
  minScale: 0.2                    # number (default: 0.2)
  maxScale: 1.5                    # number (default: 1.5)
```

### Slide Number Configuration

```yaml
slideNumber:
  format: "c/t"                    # string: "h.v" | "h/v" | "c" | "c/t" | "none"
```

Format options:
- `"h.v"`: horizontal . vertical slide number
- `"h/v"`: horizontal / vertical slide number  
- `"c"`: flattened slide number
- `"c/t"`: flattened slide number / total slides
- `"none"`: don't show slide numbers

### Theme Configuration

```yaml
solarized:
  theme: "dark"                    # string: "dark" | "light"
```

---

## Layout Components

### 1. Presentation Layout (`_layouts/presentation.html`)

The main layout for multi-slide presentations.

**Usage:**
```yaml
---
layout: presentation
---
```

**Features:**
- Includes all necessary HTML structure for Reveal.js
- Automatically includes head and script components
- Supports dark/light theme switching
- Responsive viewport configuration

**HTML Structure:**
```html
<!DOCTYPE html>
<html class="{{theme}}">
<head>
  <!-- Head includes -->
</head>
<body>
  <div class="reveal">
    <div class="slides">
      {{ content }}
    </div>
  </div>
  <!-- Script includes -->
</body>
</html>
```

### 2. Slide Layout (`_layouts/slide.html`)

Individual slide layout for single slide views.

**Usage:**
```yaml
---
layout: slide
title: "Slide Title"
---
```

**Features:**
- Simplified HTML structure for single slides
- Includes head component for styling
- Suitable for standalone slide previews

### 3. Print Layout (`_layouts/print.html`)

Optimized layout for printing and PDF generation.

**Usage:**
```yaml
---
layout: print
---
```

**Features:**
- Print-optimized CSS loading
- Simplified structure without JavaScript
- PDF export compatibility

---

## Include Components

### 1. Head Component (`_includes/head.html`)

Manages all HTML head elements including CSS, metadata, and print functionality.

**Automatic Includes:**
- Meta charset and viewport configuration
- Reveal.js CSS files
- Theme CSS (Moon theme by default)
- Syntax highlighting CSS (Monokai)
- Print/PDF export functionality

**Dynamic Title Generation:**
```liquid
{% if post.title %}{{ post.title }} | {{ page.title }}{% else %}{{ site.title }}{% endif %}
```

**Print Detection Script:**
Automatically detects print mode and loads appropriate CSS:
```javascript
var link = document.createElement('link');
link.rel = 'stylesheet';
link.type = 'text/css';
link.href = window.location.search.match(/print-pdf/gi) ? 
  'css/print/pdf.css' : 
  'node_modules/reveal.js/css/print/paper.css';
document.getElementsByTagName('head')[0].appendChild(link);
```

### 2. Script Component (`_includes/script.html`)

Handles Reveal.js initialization and plugin loading.

**Included Plugins:**
- Markdown parser (marked.js)
- Markdown processor (markdown.js)
- Syntax highlighting (highlight.js)
- Speaker notes (notes.js)

**Initialization:**
```javascript
Reveal.initialize({
  hash: true,
  dependencies: [
    { src: 'node_modules/reveal.js/plugin/markdown/marked.js' },
    { src: 'node_modules/reveal.js/plugin/markdown/markdown.js' },
    { src: 'node_modules/reveal.js/plugin/highlight/highlight.js' },
    { src: 'node_modules/reveal.js/plugin/notes/notes.js', async: true }
  ]
});
```

### 3. Slide Component (`_includes/slide.html`)

Renders individual slide content with advanced customization options.

**Usage in templates:**
```liquid
{% include slide.html %}
```

**Features:**
- Dynamic ID assignment via `slide-id` front matter
- CSS class customization via `classes` front matter
- Data attribute support for Reveal.js animations
- Automatic title rendering

**HTML Output:**
```html
<section id="{{post.slide-id}}" 
         class="step {{custom-classes}}" 
         data-{{attribute}}="{{value}}">
  <h1>{{ post.title }}</h1>
  {{ post.content }}
</section>
```

**Front Matter Options:**
```yaml
---
slide-id: "unique-slide-id"       # Custom slide ID
classes:                          # Array of CSS classes
  - "custom-class"
  - "another-class"
data:                            # Custom data attributes
  x: "1000"
  y: "500"
  rotate: "90"
---
```

---

## Build Scripts API

### 1. Setup Script (`script/setup`)

Initializes the development environment.

**Usage:**
```bash
./script/setup
```

**Functions:**
- Installs Homebrew dependencies (macOS only)
- Installs Ruby version via rbenv
- Installs gem dependencies via Bundler
- Updates git submodules
- Configures development environment

**Requirements:**
- Unix-like operating system
- Git
- Ruby (managed by rbenv recommended)

### 2. Server Script (`script/server`)

Starts the development server.

**Usage:**
```bash
./script/server [jekyll-options]
```

**Examples:**
```bash
./script/server                   # Start with default settings
./script/server --port 4001       # Start on custom port
./script/server --incremental     # Enable incremental builds
```

**Features:**
- Runs Jekyll development server
- Supports all Jekyll serve options
- Auto-reload on file changes
- Live preview at http://localhost:4000

### 3. CI Build Script (`script/cibuild`)

Builds and validates the site for continuous integration.

**Usage:**
```bash
./script/cibuild
```

**Functions:**
- Builds Jekyll site with baseurl "."
- Validates HTML using HTMLProofer
- Checks for broken links and images
- Ensures accessibility standards

**Exit Codes:**
- `0`: Build successful
- `1`: Build or validation failed

### 4. Stage Script (`script/stage`)

Deploys to staging environment.

**Usage:**
```bash
./script/stage [repository-name]
```

**Functions:**
- Builds site with staging baseurl
- Creates temporary Git repository
- Pushes to staging remote
- Opens staging URL in browser

**Requirements:**
- Git access to staging repository
- GitHub Enterprise Server access

---

## Content Creation API

### Slide Post Structure

Create slides as Markdown files in the `_posts` directory with specific naming convention:

**File Naming:**
```
YYYY-MM-DD-slide-name.md
```

**Example:**
```
_posts/0000-01-02-introduction.md
```

### Front Matter API

```yaml
---
layout: slide                     # Required: slide layout
title: "Slide Title"              # Required: slide title
slide-id: "intro"                 # Optional: custom HTML id
classes:                          # Optional: CSS classes array
  - "title-slide"
  - "centered"
data:                            # Optional: Reveal.js data attributes
  background-color: "#ff0000"
  transition: "zoom"
  autoslide: "5000"
---
```

### Advanced Front Matter Options

**Background Customization:**
```yaml
data:
  background-image: "url('image.jpg')"
  background-size: "cover"
  background-position: "center"
  background-repeat: "no-repeat"
  background-color: "#ffffff"
```

**Transition Effects:**
```yaml
data:
  transition: "slide"              # slide, fade, none, etc.
  transition-speed: "fast"         # default, fast, slow
```

**Animation and Timing:**
```yaml
data:
  autoslide: "3000"               # Auto-advance after 3 seconds
  preload: "2"                    # Preload 2 slides ahead
```

### Content Formatting

**Reveal.js Fragments:**
```markdown
- First point <!-- .element: class="fragment" -->
- Second point <!-- .element: class="fragment fade-in" -->
- Third point <!-- .element: class="fragment highlight-red" -->
```

**Speaker Notes:**
```markdown
Note: These are speaker notes that won't appear on the slide
```

**Code Highlighting:**
```markdown
```javascript
function example() {
  return "Hello, World!";
}
```

**Math Equations:**
```markdown
$$E = mc^2$$

Inline math: $a^2 + b^2 = c^2$
```

---

## Customization Guide

### Theme Customization

**Override Default Styles:**
Create `assets/css/custom.scss`:
```scss
---
---

// Custom variables
$primary-color: #007acc;
$secondary-color: #ff6b6b;

// Custom styles
.reveal {
  .slides {
    h1 {
      color: $primary-color;
      text-shadow: 2px 2px 4px rgba(0,0,0,0.3);
    }
  }
}
```

**Custom Themes:**
1. Create theme CSS in `assets/css/themes/`
2. Update `_includes/head.html` to include your theme
3. Add theme selection to `_config.yml`

### Plugin Integration

**Add Custom Reveal.js Plugins:**
1. Place plugin files in `assets/js/plugins/`
2. Update `_includes/script.html`:
```javascript
Reveal.initialize({
  dependencies: [
    // ... existing plugins
    { src: 'assets/js/plugins/your-plugin.js', async: true }
  ]
});
```

### Layout Customization

**Create Custom Layouts:**
```html
<!-- _layouts/custom.html -->
---
layout: presentation
---

<div class="custom-wrapper">
  {{ content }}
</div>
```

**Override Includes:**
Create files in `_includes/` with the same name to override defaults.

---

## Deployment API

### GitHub Pages Deployment

**Automatic Deployment:**
1. Enable GitHub Pages in repository settings
2. Set source to "GitHub Actions" or "Deploy from branch"
3. Push to main branch triggers automatic build

**Manual Deployment:**
```bash
# Build and deploy
bundle exec jekyll build
# Upload _site directory to your web server
```

### Custom Domain Setup

**Configure Custom Domain:**
1. Add `CNAME` file to repository root:
```
your-domain.com
```

2. Update DNS records:
```
CNAME www your-username.github.io
A @ 185.199.108.153
A @ 185.199.109.153
A @ 185.199.110.153
A @ 185.199.111.153
```

### Environment-Specific Configuration

**Production Configuration:**
```yaml
# _config.yml
url: "https://your-domain.com"
baseurl: ""

# Production-only settings
google_analytics: "UA-XXXXXXXX-X"
```

**Development Configuration:**
```yaml
# _config_dev.yml
url: "http://localhost:4000"
baseurl: ""

# Development-only settings
livereload: true
incremental: true
```

---

## Examples and Usage

### Basic Presentation Setup

1. **Initialize Repository:**
```bash
git clone https://github.com/your-username/slideshow-repo.git
cd slideshow-repo
./script/setup
```

2. **Create First Slide:**
```markdown
<!-- _posts/0000-01-01-welcome.md -->
---
layout: slide
title: "Welcome to My Presentation"
classes:
  - "title-slide"
---

## Getting Started

This is my first slide!

Note: Remember to speak slowly and clearly.
```

3. **Start Development Server:**
```bash
./script/server
```

### Advanced Slide Examples

**Slide with Custom Background:**
```markdown
---
layout: slide
title: "Beautiful Backgrounds"
data:
  background-image: "url('assets/images/sunset.jpg')"
  background-size: "cover"
---

# Content over background
```

**Interactive Slide with Fragments:**
```markdown
---
layout: slide
title: "Step-by-Step Reveal"
---

## Process Overview

1. Planning <!-- .element: class="fragment fade-in-then-semi-out" -->
2. Development <!-- .element: class="fragment fade-in-then-semi-out" -->
3. Testing <!-- .element: class="fragment fade-in-then-semi-out" -->
4. Deployment <!-- .element: class="fragment fade-in" -->
```

**Code Presentation Slide:**
```markdown
---
layout: slide
title: "Code Examples"
---

## JavaScript Function

```javascript
function createSlideshow(config) {
  const reveal = new Reveal(config);
  reveal.initialize();
  return reveal;
}
```

<!-- .element: class="fragment" -->
```

### Full Presentation Example

```yaml
# _config.yml
title: "Web Development Best Practices"
author: "Jane Developer"
description: "A comprehensive guide to modern web development"

reveal:
  transition: "slide"
  progress: true
  controls: false
  center: true
```

```markdown
<!-- _posts/0000-01-01-intro.md -->
---
layout: slide
title: "Web Development Best Practices"
classes:
  - "title-slide"
data:
  background-color: "#2c3e50"
---

# Web Development Best Practices

**Building Better Applications**

*Jane Developer - Senior Frontend Engineer*

Note: Welcome everyone to today's presentation on web development best practices.
```

```markdown
<!-- _posts/0000-01-02-agenda.md -->
---
layout: slide
title: "Today's Agenda"
---

## What We'll Cover

- Performance Optimization <!-- .element: class="fragment" -->
- Security Best Practices <!-- .element: class="fragment" -->
- Testing Strategies <!-- .element: class="fragment" -->
- Deployment Workflows <!-- .element: class="fragment" -->

Note: We'll spend about 15 minutes on each topic with time for questions.
```

### Integration Examples

**Google Analytics Integration:**
```html
<!-- _includes/analytics.html -->
{% if site.google_analytics %}
<script async src="https://www.googletagmanager.com/gtag/js?id={{ site.google_analytics }}"></script>
<script>
  window.dataLayer = window.dataLayer || [];
  function gtag(){dataLayer.push(arguments);}
  gtag('js', new Date());
  gtag('config', '{{ site.google_analytics }}');
</script>
{% endif %}
```

**Social Media Integration:**
```html
<!-- _includes/social.html -->
<div class="social-share">
  <a href="https://twitter.com/intent/tweet?text={{ page.title | url_encode }}&url={{ site.url }}{{ page.url }}" 
     target="_blank" rel="noopener">
    Share on Twitter
  </a>
</div>
```

---

## API Reference Summary

### Configuration Methods
- `site.title` - Presentation title
- `site.author` - Author name
- `site.reveal.*` - Reveal.js configuration
- `site.solarized.theme` - Theme selection

### Layout Methods
- `presentation` - Full slideshow layout
- `slide` - Individual slide layout  
- `print` - Print-optimized layout

### Include Methods
- `{% include head.html %}` - HTML head section
- `{% include script.html %}` - JavaScript initialization
- `{% include slide.html %}` - Slide rendering

### Build Methods
- `./script/setup` - Environment setup
- `./script/server` - Development server
- `./script/cibuild` - CI/CD build
- `./script/stage` - Staging deployment

### Content Methods
- Front matter configuration
- Markdown content processing
- Fragment and animation support
- Speaker notes integration

This documentation provides comprehensive coverage of all public APIs, functions, and components in the GitHub Slideshow framework. Each section includes practical examples and usage instructions to help users effectively utilize the system.
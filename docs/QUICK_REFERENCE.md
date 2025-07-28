# Quick Reference Guide

## Command Line Reference

### Setup and Development
```bash
./script/setup              # Initialize development environment
./script/server              # Start development server (localhost:4000)
./script/server --port 4001  # Start on custom port
./script/cibuild             # Build and validate for CI
./script/stage [repo]        # Deploy to staging environment
```

### Jekyll Commands
```bash
bundle exec jekyll serve     # Start development server
bundle exec jekyll build     # Build static site
bundle exec jekyll clean     # Clean build artifacts
bundle exec jekyll doctor    # Check site health
```

---

## Configuration Reference

### Site Configuration (`_config.yml`)
```yaml
# Basic Settings
title: "Presentation Title"
author: "Author Name"
description: "Description"
baseurl: "/path"
url: "https://domain.com"

# Reveal.js Settings
reveal:
  controls: false            # Show navigation controls
  progress: true             # Show progress bar
  history: true              # Browser history
  center: true               # Vertical centering
  transition: "linear"       # Transition effect
  width: 1000               # Presentation width
  height: 920               # Presentation height

# Theme Settings
solarized:
  theme: "dark"             # "dark" | "light"

slideNumber:
  format: "c/t"             # "h.v" | "h/v" | "c" | "c/t" | "none"
```

### Transition Options
- `none` - No transition
- `fade` - Fade in/out
- `slide` - Slide horizontally
- `convex` - Convex transition
- `concave` - Concave transition
- `zoom` - Zoom in/out
- `linear` - Linear slide

---

## Front Matter Reference

### Basic Slide Front Matter
```yaml
---
layout: slide               # Required
title: "Slide Title"        # Required
slide-id: "unique-id"       # Optional HTML ID
classes:                    # Optional CSS classes
  - "title-slide"
  - "centered"
data:                       # Optional data attributes
  background-color: "#ff0000"
  transition: "zoom"
---
```

### Layout Options
- `presentation` - Full slideshow layout
- `slide` - Individual slide layout
- `print` - Print-optimized layout

### Data Attributes
```yaml
data:
  # Backgrounds
  background-color: "#color"
  background-image: "url('image.jpg')"
  background-size: "cover"
  background-position: "center"
  background-repeat: "no-repeat"
  background-video: "video.mp4"
  background-video-loop: true
  background-video-muted: true
  
  # Transitions
  transition: "slide"
  transition-speed: "fast"
  
  # Positioning (for custom navigation)
  x: "1000"
  y: "500"
  rotate: "45"
  scale: "2"
  
  # Timing
  autoslide: "5000"
```

---

## Fragment Reference

### Fragment Classes
```markdown
<!-- Basic fragments -->
- Item 1 <!-- .element: class="fragment" -->
- Item 2 <!-- .element: class="fragment fade-in" -->
- Item 3 <!-- .element: class="fragment fade-out" -->

<!-- Directional fades -->
- fade-up <!-- .element: class="fragment fade-up" -->
- fade-down <!-- .element: class="fragment fade-down" -->
- fade-left <!-- .element: class="fragment fade-left" -->
- fade-right <!-- .element: class="fragment fade-right" -->

<!-- Transform effects -->
- grow <!-- .element: class="fragment grow" -->
- shrink <!-- .element: class="fragment shrink" -->
- strike <!-- .element: class="fragment strike" -->

<!-- Highlights -->
- highlight-red <!-- .element: class="fragment highlight-red" -->
- highlight-green <!-- .element: class="fragment highlight-green" -->
- highlight-blue <!-- .element: class="fragment highlight-blue" -->

<!-- Sequential reveals -->
- fade-in-then-out <!-- .element: class="fragment fade-in-then-out" -->
- fade-in-then-semi-out <!-- .element: class="fragment fade-in-then-semi-out" -->
```

### Fragment Timing
```markdown
<!-- Control fragment order -->
- First <!-- .element: class="fragment" data-fragment-index="1" -->
- Second <!-- .element: class="fragment" data-fragment-index="2" -->
- Third <!-- .element: class="fragment" data-fragment-index="3" -->
```

---

## Content Formatting Reference

### Markdown Syntax
```markdown
# Heading 1
## Heading 2
### Heading 3

**Bold text**
*Italic text*
`Inline code`

- Bullet point
- Another point
  - Nested point

1. Numbered list
2. Second item

[Link text](https://example.com)

![Image alt](path/to/image.jpg)
```

### Code Blocks
````markdown
```javascript
function example() {
  return "Hello, World!";
}
```

```python
def example():
    return "Hello, World!"
```

```bash
./script/setup
```
````

### Math Notation (with MathJax)
```markdown
Inline math: \\(a^2 + b^2 = c^2\\)

Block math:
\\[E = mc^2\\]

\\[\int_{-\infty}^{\infty} e^{-x^2} dx = \sqrt{\pi}\\]
```

### Speaker Notes
```markdown
Content visible on slide

Note: This is a speaker note that won't appear on the slide.
Multiple lines are supported.
```

---

## File Structure Reference

### Required Files
```
_config.yml                 # Jekyll configuration
index.html                  # Main presentation file
_layouts/
  presentation.html         # Slideshow layout
  slide.html               # Individual slide layout
  print.html               # Print layout
_includes/
  head.html                # HTML head section
  script.html              # JavaScript initialization
  slide.html               # Slide component
_posts/
  YYYY-MM-DD-title.md      # Slide content files
```

### Optional Files
```
_sass/                     # Custom Sass files
assets/
  css/                     # Custom CSS
  js/                      # Custom JavaScript
  images/                  # Image assets
  videos/                  # Video assets
script/
  setup                    # Environment setup
  server                   # Development server
  cibuild                  # CI build
  stage                    # Staging deployment
```

---

## Naming Conventions

### Post Files
```
_posts/0000-01-01-intro.md     # Introduction slide
_posts/0000-01-02-agenda.md    # Agenda slide
_posts/0000-01-03-content.md   # Content slide
_posts/0000-01-04-conclusion.md # Conclusion slide
```

### Asset Organization
```
assets/
  images/
    slides/              # Slide-specific images
    backgrounds/         # Background images
    icons/              # Icon assets
  css/
    themes/             # Custom themes
    components/         # Component styles
  js/
    plugins/            # Custom plugins
    components/         # Component scripts
```

---

## CSS Class Reference

### Built-in Classes
```css
.reveal                    /* Main presentation container */
.slides                   /* Slides container */
.step                     /* Individual slide */
.slide                    /* Default slide class */
.fragment                 /* Fragment animation base */
.present                  /* Currently visible slide */
.past                     /* Previous slides */
.future                   /* Upcoming slides */
```

### Custom Classes (Examples)
```css
.title-slide              /* Title slide styling */
.centered                 /* Center-aligned content */
.code-slide               /* Code-focused slides */
.image-slide              /* Image-heavy slides */
.dark-background          /* Dark background variant */
.light-background         /* Light background variant */
```

---

## JavaScript API Reference

### Reveal.js Methods
```javascript
// Navigation
Reveal.next()             // Next slide
Reveal.prev()             // Previous slide
Reveal.slide(h, v)        // Go to specific slide
Reveal.left()             // Navigate left
Reveal.right()            // Navigate right
Reveal.up()               // Navigate up
Reveal.down()             // Navigate down

// State
Reveal.isFirstSlide()     // Check if first slide
Reveal.isLastSlide()      // Check if last slide
Reveal.getSlide(h, v)     // Get slide element
Reveal.getCurrentSlide()  // Get current slide
Reveal.getIndices()       // Get current indices

// Events
Reveal.addEventListener('slidechanged', function(event) {
  // Handle slide change
});

Reveal.addEventListener('fragmentshown', function(event) {
  // Handle fragment shown
});

Reveal.addEventListener('fragmenthidden', function(event) {
  // Handle fragment hidden
});
```

### Custom Event Handlers
```javascript
// Keyboard shortcuts
document.addEventListener('keydown', function(event) {
  switch(event.key) {
    case 'Home': Reveal.slide(0); break;
    case 'End': Reveal.slide(Reveal.getTotalSlides() - 1); break;
  }
});

// Slide-specific logic
Reveal.addEventListener('slidechanged', function(event) {
  var slideId = event.currentSlide.id;
  if (slideId === 'demo-slide') {
    // Initialize demo
  }
});
```

---

## Build and Deployment Reference

### GitHub Pages Deployment
```yaml
# .github/workflows/deploy.yml
name: Deploy
on:
  push:
    branches: [ main ]
jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
    - uses: actions/checkout@v3
    - uses: ruby/setup-ruby@v1
      with:
        ruby-version: '3.0'
        bundler-cache: true
    - run: bundle install
    - run: ./script/cibuild
    - uses: peaceiris/actions-gh-pages@v3
      with:
        github_token: ${{ secrets.GITHUB_TOKEN }}
        publish_dir: ./_site
```

### Environment Variables
```bash
# Development
JEKYLL_ENV=development
DISABLE_WHITELIST=1

# Production
JEKYLL_ENV=production
```

### Custom Domain Setup
```
# CNAME file
your-domain.com

# DNS Records
A       @    185.199.108.153
A       @    185.199.109.153
A       @    185.199.110.153
A       @    185.199.111.153
CNAME   www  username.github.io
```

---

## Troubleshooting Quick Fixes

### Common Issues
```bash
# Permission errors
chmod +x script/setup script/server script/cibuild script/stage

# Bundle issues
bundle install --force
bundle update

# Node modules issues
rm -rf node_modules package-lock.json
npm install

# Jekyll cache issues
bundle exec jekyll clean
rm -rf _site .jekyll-cache

# Gem version conflicts
bundle exec gem update
bundle update
```

### Debug Mode
```yaml
# _config.yml
liquid:
  error_mode: warn
  strict_filters: false
  strict_variables: false

# Enable verbose output
incremental: false
livereload: true
```

---

## Performance Optimization

### Image Optimization
```markdown
<!-- WebP format -->
![Chart](assets/images/chart.webp)

<!-- Responsive images -->
<picture>
  <source media="(min-width: 800px)" srcset="large.webp">
  <source media="(min-width: 400px)" srcset="medium.webp">
  <img src="small.webp" alt="Description" loading="lazy">
</picture>

<!-- Lazy loading -->
![Chart](chart.jpg){: loading="lazy"}
```

### Asset Compression
```yaml
# _config.yml
sass:
  style: compressed

plugins:
  - jekyll-minifier

jekyll-minifier:
  compress_css: true
  compress_javascript: true
  compress_json: true
```

---

## Accessibility Features

### ARIA Labels
```html
<section aria-label="Slide: Introduction" role="region">
  <h1 id="intro-title">Introduction</h1>
  <div aria-describedby="intro-title">
    Content...
  </div>
</section>
```

### Keyboard Navigation
```javascript
// Enhanced keyboard support
document.addEventListener('keydown', function(event) {
  if (event.ctrlKey || event.metaKey) return;
  
  switch(event.key) {
    case 'Home': Reveal.slide(0); break;
    case 'End': Reveal.slide(Reveal.getTotalSlides() - 1); break;
    case 'PageUp': Reveal.prev(); break;
    case 'PageDown': Reveal.next(); break;
  }
});
```

### High Contrast Mode
```css
@media (prefers-contrast: high) {
  .reveal {
    --background-color: #000000;
    --text-color: #ffffff;
    --link-color: #ffff00;
  }
}
```

This quick reference provides all the essential information needed to work efficiently with the GitHub Slideshow framework.
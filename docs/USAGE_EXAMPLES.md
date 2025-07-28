# Usage Examples and Tutorials

## Quick Start Guide

### 1. Basic Presentation Setup

**Initialize Project:**
```bash
# Clone or create new repository
git clone https://github.com/your-username/slideshow-repo.git
cd slideshow-repo

# Setup development environment
./script/setup

# Start development server
./script/server
```

**Create Your First Slide:**
```markdown
<!-- _posts/0000-01-01-welcome.md -->
---
layout: slide
title: "Welcome to My Presentation"
---

# Hello World!

This is my first slide using the GitHub Slideshow framework.

Note: Press 'S' to view speaker notes in a separate window.
```

**View Your Presentation:**
Open http://localhost:4000 in your browser.

---

## Content Creation Examples

### Basic Slide Structures

**Title Slide:**
```markdown
<!-- _posts/0000-01-01-title.md -->
---
layout: slide
title: "Presentation Title"
classes:
  - "title-slide"
data:
  background-color: "#2c3e50"
---

# Modern Web Development

## Building Better Applications

**John Smith** - Senior Developer  
*TechCorp Inc.*

*March 15, 2024*

Note: Welcome everyone to today's presentation on modern web development practices.
```

**Content Slide with Bullet Points:**
```markdown
<!-- _posts/0000-01-02-agenda.md -->
---
layout: slide
title: "Today's Agenda"
---

## What We'll Cover

- **Performance Optimization**
  - Bundle size reduction
  - Lazy loading strategies
- **Security Best Practices**
  - Input validation
  - Authentication patterns
- **Testing Strategies**
  - Unit testing
  - Integration testing
- **Deployment Workflows**
  - CI/CD pipelines
  - Environment management

Note: We'll spend approximately 15 minutes on each topic, with time for questions at the end.
```

**Code Example Slide:**
```markdown
<!-- _posts/0000-01-03-code-example.md -->
---
layout: slide
title: "JavaScript Best Practices"
---

## Modern JavaScript Function

```javascript
// ES6+ Arrow Function with Destructuring
const processUserData = ({ name, email, role = 'user' }) => {
  // Input validation
  if (!name || !email) {
    throw new Error('Name and email are required');
  }
  
  // Data processing
  return {
    id: generateUUID(),
    name: name.trim(),
    email: email.toLowerCase(),
    role,
    createdAt: new Date().toISOString()
  };
};

// Usage example
const userData = processUserData({
  name: 'John Doe',
  email: 'JOHN@EXAMPLE.COM'
});
```

Note: This example demonstrates modern JavaScript patterns including destructuring, default parameters, and proper error handling.
```

---

## Advanced Slide Techniques

### Fragment Animations

**Sequential Reveal:**
```markdown
<!-- _posts/0000-01-04-fragments.md -->
---
layout: slide
title: "Progressive Disclosure"
---

## Development Process

1. Planning & Analysis <!-- .element: class="fragment fade-in-then-semi-out" data-fragment-index="1" -->
2. Design & Prototyping <!-- .element: class="fragment fade-in-then-semi-out" data-fragment-index="2" -->
3. Development & Testing <!-- .element: class="fragment fade-in-then-semi-out" data-fragment-index="3" -->
4. Deployment & Monitoring <!-- .element: class="fragment fade-in" data-fragment-index="4" -->

<!-- .element: class="fragment fade-in" data-fragment-index="5" -->
### Success Metrics
- User satisfaction: 95%+ <!-- .element: class="fragment highlight-green" data-fragment-index="6" -->
- Performance: <2s load time <!-- .element: class="fragment highlight-blue" data-fragment-index="7" -->
- Uptime: 99.9% availability <!-- .element: class="fragment highlight-red" data-fragment-index="8" -->

Note: Each step builds on the previous one, and the metrics show our target outcomes.
```

**Advanced Fragment Effects:**
```markdown
<!-- _posts/0000-01-05-advanced-fragments.md -->
---
layout: slide
title: "Animation Showcase"
---

## Available Fragment Effects

- fade-in <!-- .element: class="fragment fade-in" -->
- fade-out <!-- .element: class="fragment fade-out" -->
- fade-up <!-- .element: class="fragment fade-up" -->
- fade-down <!-- .element: class="fragment fade-down" -->
- fade-left <!-- .element: class="fragment fade-left" -->
- fade-right <!-- .element: class="fragment fade-right" -->
- grow <!-- .element: class="fragment grow" -->
- shrink <!-- .element: class="fragment shrink" -->
- strike <!-- .element: class="fragment strike" -->
- highlight-red <!-- .element: class="fragment highlight-red" -->
- highlight-green <!-- .element: class="fragment highlight-green" -->
- highlight-blue <!-- .element: class="fragment highlight-blue" -->

Note: Fragments can be combined and controlled with data-fragment-index for precise timing.
```

### Background Customization

**Image Background:**
```markdown
<!-- _posts/0000-01-06-image-bg.md -->
---
layout: slide
title: "Visual Impact"
data:
  background-image: "url('assets/images/city-skyline.jpg')"
  background-size: "cover"
  background-position: "center"
  background-opacity: "0.7"
---

<div style="background: rgba(0,0,0,0.7); padding: 2rem; border-radius: 10px;">

# Data-Driven Decisions

## Transform Your Business with Analytics

</div>

Note: Using semi-transparent overlays ensures text readability over background images.
```

**Gradient Background:**
```markdown
<!-- _posts/0000-01-07-gradient-bg.md -->
---
layout: slide
title: "Modern Design"
data:
  background: "linear-gradient(45deg, #667eea 0%, #764ba2 100%)"
---

# Beautiful Presentations

Made simple with modern CSS gradients

Note: CSS gradients can create sophisticated visual effects without additional image assets.
```

**Video Background:**
```markdown
<!-- _posts/0000-01-08-video-bg.md -->
---
layout: slide
title: "Dynamic Content"
data:
  background-video: "assets/videos/code-typing.mp4"
  background-video-loop: true
  background-video-muted: true
---

# Live Coding Session

Watch development in action

Note: Video backgrounds should be subtle and not distract from the content.
```

---

## Interactive Features

### Speaker Notes

**Detailed Speaker Notes:**
```markdown
<!-- _posts/0000-01-09-speaker-notes.md -->
---
layout: slide
title: "Complex Topic Explanation"
---

## Microservices Architecture

Benefits:
- Scalability
- Flexibility
- Technology diversity

Challenges:
- Network complexity
- Data consistency
- Monitoring overhead

Note: 
**Introduction (30 seconds):**
Start by asking who has experience with microservices. This helps gauge the audience's background knowledge.

**Benefits Section (2 minutes):**
- Scalability: Explain how individual services can be scaled independently based on demand
- Flexibility: Discuss how teams can work independently and deploy separately
- Technology diversity: Show how different services can use different tech stacks

**Challenges Section (2 minutes):**
- Network complexity: Emphasize the importance of service discovery and load balancing
- Data consistency: Discuss eventual consistency vs. strong consistency trade-offs
- Monitoring: Explain the need for distributed tracing and centralized logging

**Questions (1 minute):**
Ask if anyone has specific challenges they'd like to discuss.

**Transition:**
"Now let's look at a practical implementation example..."
```

### Slide Transitions

**Custom Transitions:**
```markdown
<!-- _posts/0000-01-10-transitions.md -->
---
layout: slide
title: "Smooth Animations"
data:
  transition: "convex"
  transition-speed: "slow"
---

# Seamless Flow

This slide uses a convex transition effect

Note: Available transitions: none, fade, slide, convex, concave, zoom
```

**Per-Slide Timing:**
```markdown
<!-- _posts/0000-01-11-timing.md -->
---
layout: slide
title: "Auto-Advance"
data:
  autoslide: "5000"
  transition: "fade"
---

# Automatic Progression

This slide will advance automatically after 5 seconds

Note: Use auto-slide sparingly and only for slides without complex content.
```

---

## Theme Customization

### Custom CSS

**Create Custom Theme:**
```scss
/* assets/css/custom.scss */
---
---

// Variables
$primary-color: #3498db;
$secondary-color: #e74c3c;
$background-color: #2c3e50;
$text-color: #ecf0f1;

// Global styles
.reveal {
  font-family: 'Roboto', sans-serif;
  
  .slides {
    h1, h2, h3 {
      color: $primary-color;
      text-shadow: 2px 2px 4px rgba(0,0,0,0.3);
    }
    
    code {
      background: rgba(255,255,255,0.1);
      padding: 0.2em 0.4em;
      border-radius: 3px;
    }
    
    .fragment {
      &.highlight-blue {
        color: $primary-color;
      }
      
      &.highlight-red {
        color: $secondary-color;
      }
    }
  }
}

// Custom slide classes
.title-slide {
  h1 {
    font-size: 3.5em;
    margin-bottom: 0.5em;
  }
  
  background: linear-gradient(135deg, $primary-color, $secondary-color);
}

.code-slide {
  .hljs {
    font-size: 0.8em;
    line-height: 1.4;
  }
}

.centered {
  text-align: center;
  
  * {
    margin: 0 auto;
  }
}
```

**Include Custom CSS:**
```html
<!-- _includes/head.html -->
<meta charset="utf-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">

<title>{% if post.title %}{{ post.title }} | {{ page.title }}{% else %}{{ site.title }}{% endif %}</title>

<!-- Reveal.js CSS -->
<link rel="stylesheet" href="{{ site.baseurl }}/node_modules/reveal.js/css/reveal.css">
<link rel="stylesheet" href="{{site.baseurl}}/node_modules/reveal.js/css/theme/moon.css">
<link rel="stylesheet" href="{{site.baseurl}}/node_modules/reveal.js/lib/css/monokai.css">

<!-- Custom CSS -->
<link rel="stylesheet" href="{{ site.baseurl }}/assets/css/custom.css">

<!-- Print and PDF exports -->
<script>
  var link = document.createElement( 'link' );
  link.rel = 'stylesheet';
  link.type = 'text/css';
  link.href = window.location.search.match( /print-pdf/gi ) ? 'css/print/pdf.css' : 'node_modules/reveal.js/css/print/paper.css';
  document.getElementsByTagName( 'head' )[0].appendChild( link );
</script>
```

---

## Plugin Integration

### Math Support

**MathJax Integration:**
```html
<!-- _includes/script.html -->
<script src="{{ site.baseurl }}/node_modules/reveal.js/js/reveal.js"></script>

<script>
  Reveal.initialize({
    hash: true,
    math: {
      mathjax: 'https://cdn.jsdelivr.net/gh/mathjax/mathjax@2.7.8/MathJax.js',
      config: 'TeX-AMS_HTML-full',
      tex2jax: {
        inlineMath: [['\\(','\\)']],
        displayMath: [['\\[','\\]']],
        balanceBraces: true,
        processEscapes: false,
        processRefs: true,
        processEnvironments: true,
        preview: 'TeX',
        skipTags: ['script','noscript','style','textarea','pre','code'],
        ignoreClass: 'tex2jax_ignore',
        processClass: 'tex2jax_process'
      }
    },
    dependencies: [
      { src: 'node_modules/reveal.js/plugin/markdown/marked.js' },
      { src: 'node_modules/reveal.js/plugin/markdown/markdown.js' },
      { src: 'node_modules/reveal.js/plugin/highlight/highlight.js' },
      { src: 'node_modules/reveal.js/plugin/notes/notes.js', async: true },
      { src: 'node_modules/reveal.js/plugin/math/math.js', async: true }
    ]
  });
</script>
```

**Math Content Example:**
```markdown
<!-- _posts/0000-01-12-math.md -->
---
layout: slide
title: "Mathematical Concepts"
---

## Fundamental Equations

**Einstein's Mass-Energy Equivalence:**
\\[E = mc^2\\]

**Pythagorean Theorem:**
\\[a^2 + b^2 = c^2\\]

**Quadratic Formula:**
\\[x = \frac{-b \pm \sqrt{b^2 - 4ac}}{2a}\\]

Inline math example: The area of a circle is \\(A = \pi r^2\\).

Note: Math rendering requires MathJax plugin to be loaded.
```

### Chart Integration

**Chart.js Integration:**
```html
<!-- _includes/chart.html -->
<canvas id="{{ include.id }}" width="{{ include.width | default: 400 }}" height="{{ include.height | default: 300 }}"></canvas>

<script>
document.addEventListener('DOMContentLoaded', function() {
  var ctx = document.getElementById('{{ include.id }}').getContext('2d');
  var chart = new Chart(ctx, {{ include.config }});
});
</script>
```

**Chart Usage:**
```markdown
<!-- _posts/0000-01-13-charts.md -->
---
layout: slide
title: "Data Visualization"
---

## Performance Metrics

{% include chart.html id="performance-chart" config='{
  "type": "line",
  "data": {
    "labels": ["Jan", "Feb", "Mar", "Apr", "May"],
    "datasets": [{
      "label": "Response Time (ms)",
      "data": [120, 95, 87, 92, 78],
      "borderColor": "#3498db",
      "backgroundColor": "rgba(52, 152, 219, 0.1)"
    }]
  },
  "options": {
    "responsive": true,
    "scales": {
      "y": {
        "beginAtZero": true
      }
    }
  }
}' %}

Note: Interactive charts help communicate data trends more effectively than static images.
```

---

## Advanced Configuration

### Multi-Section Presentations

**Vertical Slides:**
```markdown
<!-- _posts/0000-01-14-section-1.md -->
---
layout: slide
title: "Section 1: Overview"
data:
  x: "0"
  y: "0"
---

# Frontend Technologies

Horizontal navigation for different topics

---

<!-- _posts/0000-01-15-section-1-details.md -->
---
layout: slide
title: "Frontend Details"
data:
  x: "0"
  y: "1000"
---

## Frontend Stack

- React / Vue / Angular
- TypeScript
- Webpack / Vite
- Testing Libraries

---

<!-- _posts/0000-01-16-section-2.md -->
---
layout: slide
title: "Section 2: Backend"
data:
  x: "1000"
  y: "0"
---

# Backend Technologies

Next section with vertical sub-slides
```

### Custom Navigation

**Overview Slide:**
```yaml
# _config.yml
overview: true
overview-data:
  x: "2000"
  y: "2000"
  scale: "4"
```

```html
<!-- Custom overview in index.html -->
{% unless site.simple-slideshow %}
{% if site.overview %}
<section id="overview" class="step" 
  {% for attr in site.overview-data %} 
    data-{{attr[0]}}="{{attr[1]}}"
  {% endfor %}>
  
  <h1>Presentation Overview</h1>
  <div class="overview-grid">
    {% for post in site.posts reversed %}
      <div class="overview-item">
        <h3>{{ post.title }}</h3>
        <p>{{ post.excerpt | strip_html | truncate: 100 }}</p>
      </div>
    {% endfor %}
  </div>
</section>
{% endif %}
{% endunless %}
```

---

## Build and Deployment

### GitHub Actions Workflow

```yaml
# .github/workflows/deploy.yml
name: Deploy Slideshow

on:
  push:
    branches: [ main ]
  pull_request:
    branches: [ main ]

jobs:
  build-and-deploy:
    runs-on: ubuntu-latest
    
    steps:
    - uses: actions/checkout@v3
    
    - name: Setup Ruby
      uses: ruby/setup-ruby@v1
      with:
        ruby-version: '3.0'
        bundler-cache: true
    
    - name: Install dependencies
      run: |
        bundle install
        npm install
    
    - name: Build site
      run: ./script/cibuild
    
    - name: Deploy to GitHub Pages
      if: github.ref == 'refs/heads/main'
      uses: peaceiris/actions-gh-pages@v3
      with:
        github_token: ${{ secrets.GITHUB_TOKEN }}
        publish_dir: ./_site
```

### Custom Domain Setup

**CNAME Configuration:**
```
# CNAME file in repository root
presentations.yourcompany.com
```

**DNS Configuration:**
```
# DNS Records
CNAME   www               youruser.github.io
A       @                 185.199.108.153
A       @                 185.199.109.153
A       @                 185.199.110.153
A       @                 185.199.111.153
AAAA    @                 2606:50c0:8000::153
AAAA    @                 2606:50c0:8001::153
AAAA    @                 2606:50c0:8002::153
AAAA    @                 2606:50c0:8003::153
```

### Environment-Specific Builds

**Development Configuration:**
```yaml
# _config_development.yml
url: "http://localhost:4000"
baseurl: ""

# Development-only features
livereload: true
incremental: true
future: true
unpublished: true

# Debug settings
liquid:
  error_mode: warn
  strict_filters: false
  strict_variables: false
```

**Production Configuration:**
```yaml
# _config_production.yml
url: "https://presentations.yourcompany.com"
baseurl: ""

# Production optimizations
compress_html:
  clippings: all
  comments: all
  endings: all
  ignore:
    envs: development

# Analytics
google_analytics: "UA-XXXXXXXX-X"

# Security headers
plugins:
  - jekyll-sitemap
  - jekyll-seo-tag
```

**Build Commands:**
```bash
# Development build
bundle exec jekyll serve --config _config.yml,_config_development.yml

# Production build
bundle exec jekyll build --config _config.yml,_config_production.yml
```

---

## Troubleshooting Common Issues

### Performance Optimization

**Large Image Handling:**
```markdown
<!-- Optimized image loading -->
![Performance Chart](assets/images/chart.webp){: .lazy-load width="800" height="400" loading="lazy"}

<!-- Responsive images -->
<picture>
  <source media="(min-width: 800px)" srcset="assets/images/chart-large.webp">
  <source media="(min-width: 400px)" srcset="assets/images/chart-medium.webp">
  <img src="assets/images/chart-small.webp" alt="Performance Chart" loading="lazy">
</picture>
```

**Asset Optimization:**
```yaml
# _config.yml
sass:
  style: compressed

plugins:
  - jekyll-minifier

jekyll-minifier:
  uglifier_args:
    harmony: true
  compress_css: true
  compress_javascript: true
  compress_json: true
```

### Accessibility Improvements

**Keyboard Navigation:**
```javascript
// Custom keyboard shortcuts
document.addEventListener('keydown', function(event) {
  switch(event.key) {
    case 'Home':
      Reveal.slide(0);
      break;
    case 'End':
      Reveal.slide(Reveal.getTotalSlides() - 1);
      break;
    case 'PageUp':
      Reveal.prev();
      break;
    case 'PageDown':
      Reveal.next();
      break;
  }
});
```

**Screen Reader Support:**
```html
<!-- Enhanced slide markup -->
<section aria-label="Slide {{ forloop.index }}: {{ post.title }}" 
         role="region"
         tabindex="0">
  {% if post.title != "" %}
    <h1 id="slide-{{ forloop.index }}-title">{{ post.title }}</h1>
  {% endif %}
  
  <div aria-describedby="slide-{{ forloop.index }}-title">
    {{ post.content }}
  </div>
</section>
```

This comprehensive usage guide provides practical examples for implementing all the features and APIs available in the GitHub Slideshow framework, from basic setup to advanced customization and deployment scenarios.
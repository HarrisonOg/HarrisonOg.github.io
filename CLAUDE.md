# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a Jekyll-based personal website/blog hosted on GitHub Pages (HarrisonOg.github.io). The site uses the Minima theme and is built using Jekyll 4.4.1.

## Ruby Environment Setup

### Requirements
- Ruby >= 2.7.0 (Jekyll 4.4.1 requirement)
- Bundler 4.0.2
- Current setup uses Ruby 3.3.7 via rbenv

### First-Time Setup
If rbenv is not installed:
```bash
# Install rbenv via Homebrew
brew install rbenv ruby-build

# Initialize rbenv (adds to ~/.zprofile)
rbenv init

# Restart terminal or source profile
source ~/.zprofile

# Install Ruby 3.3.7
rbenv install 3.3.7
```

The project includes a `.ruby-version` file that automatically selects Ruby 3.3.7 when you're in this directory.

## Development Commands

### Local Development
```bash
# Install dependencies
bundle install

# Start local development server with auto-regeneration
bundle exec jekyll serve

# Build the site (outputs to _site/)
bundle exec jekyll build
```

**Important**: Changes to `_config.yml` require restarting the Jekyll server - the config file is not auto-reloaded.

## Site Architecture

### Content Structure
- **Posts**: Stored in `_posts/` with naming convention `YYYY-MM-DD-title.markdown`
  - Posts use `layout: post` front matter
  - Categorized (e.g., `categories: jekyll update`)

- **Pages**: Root-level `.markdown` files with front matter
  - `index.markdown`: Homepage (uses `layout: home`)
  - `about.markdown`: About page (uses `layout: page`)

- **Front Matter**: All content files require YAML front matter at the top with layout, title, and other metadata

### Configuration
- `_config.yml`: Site-wide settings including title, email, description, GitHub username, theme, and plugins
- Theme: Uses the Minima theme (`gem "minima", "~> 2.5"`)
- Plugins: jekyll-feed for RSS generation

### Build Output
- Generated site files are placed in `_site/` directory
- This directory is git-ignored and should not be committed

## Jekyll Specifics

### Code Highlighting
Use Liquid tags for syntax highlighting:
```
{% highlight ruby %}
# code here
{% endhighlight %}
```

### Theme Customization
To override Minima theme defaults, you can create files in the repository that match the theme's structure. See Jekyll documentation on theme overriding.

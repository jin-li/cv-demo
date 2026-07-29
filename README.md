# Jinli CV Demo Site (锦鲤简历演示站点)

This repository demonstrates how to use the [jinli-cv](https://github.com/jin-li/jinli-cv) (a.k.a. 锦鲤简历) Hugo theme to create a beautiful, printable CV/resume website with multi-language support.

**Live Demo:** [https://jinli-cv-demo.netlify.app/](https://jinli-cv-demo.netlify.app/)

## Overview

This repo shows how to:
- Use the jinli-cv (锦鲤简历) theme as a Git submodule
- Configure multiple CV versions (different languages/versions)
- Customize content, styling, and deployment
- Deploy to Netlify (or any static hosting)

The actual CV content and configuration comes from the theme's `exampleSite/` directory, which is served directly from the theme submodule.

## Repository Structure

```
cv-demo/
├── themes/
│   └── jinli-cv/          # jinli-cv (锦鲤简历) theme (git submodule)
│       ├── exampleSite/   # <- This is what gets served
│       │   ├── config.toml
│       │   ├── content/
│       │   ├── data/
│       │   └── static/
│       └── ...            # theme source
├── netlify.toml           # Netlify build configuration
├── .gitmodules            # Submodule definition
└── README.md              # This file
```

## 🚀 How It Works

This repository doesn't contain its own content. Instead:
1. The `jinli-cv` theme is included as a Git submodule
2. Netlify builds the site from `themes/jinli-cv/exampleSite/` (specified in `netlify.toml`)
3. The theme's example site provides a complete, working CV demo with:
   - Default CV (homepage)
   - German version (`/cv-de/`)
   - Chinese version (`/cv-zh/`)
   - Sample data for all sections (Experience, Projects, Publications, etc.)

## 🔧 Customizing for Your Own CV

To create your own personalized CV site based on this demo:

### Option 1: Fork and Customize (Recommended)
1. **Fork** this repository to your GitHub account
2. **Customize the content:**
   - Edit `themes/jinli-cv/exampleSite/data/content.yaml` (default CV)
   - Modify/add language versions in `themes/jinli-cv/exampleSite/data/cv-*/`
   - Replace `themes/jinli-cv/exampleSite/static/img/avatar.png` with your photo
   - Adjust colors, fonts, and layout in `themes/jinli-cv/exampleSite/config.toml`
3. **Push to GitHub** - Netlify will automatically rebuild and deploy your changes

### Option 2: Create Your Own Repository
1. Create a new repository
2. Add the jinli-cv (锦鲤简历) theme as a submodule:
   ```bash
   hugo new site my-cv-site
   cd my-cv-site
   git init
   git submodule add https://github.com/jin-li/jinli-cv.git themes/jinli-cv
   cp -r themes/jinli-cv/exampleSite/* .
   ```
3. Create the theme symlink:
   ```bash
   mkdir -p themes
   ln -s ../../.. themes/jinli-cv
   ```
4. Customize the content (same as Option 1)
5. Add `netlify.toml` (see below)
6. Push to GitHub and connect to Netlify

## 🛠️ Local Development

To preview changes locally:

### Using the theme's exampleSite (recommended for testing)
```bash
# Clone jinli-cv (锦鲤简历) theme
git clone https://github.com/jin-li/jinli-cv.git
cd jinli-cv/exampleSite

# Create symlink to theme (needed for local dev)
mkdir -p themes
ln -s ../.. themes/jinli-cv

# Start development server
hugo server -D
```
Visit http://localhost:1313/

### Using your own repository
```bash
hugo server -D
```

## ⚙️ Netlify Deployment

This repository is configured for automatic deployment to Netlify via `netlify.toml`:

```toml
[build]
  base = "themes/jinli-cv/exampleSite"
  command = "hugo"
  publish = "public"

[build.environment]
  HUGO_VERSION = "0.146.5"
```

**Important:** The `base` setting tells Netlify to run the build command from within the theme's exampleSite directory, where the actual `config.toml`, `content/`, and `data/` directories reside.

### Manual Netlify Setup
If connecting via Netlify UI:
1. **Build command**: `hugo`
2. **Publish directory**: `public`
3. **Build environment variables**: `HUGO_VERSION = 0.146.5`
4. **Important**: Ensure your base directory is set correctly (or leave blank if using `netlify.toml`)

## 📝 Customization Guide

### Content Files
All content is YAML/TOML in the `data/` directory:
- `data/content.yaml` - Default CV (homepage)
- `data/cv-de/config.toml` + `data/cv-de/content.yaml` - German version
- `data/cv-zh/config.toml` + `data/cv-zh/content.yaml` - Chinese version

### Key Sections You Can Customize
- **Personal Info**: Name, title, avatar, contact information
- **Profile**: Professional summary/bio
- **Experience**: Work history with descriptions and badges
- **Education**: Degrees, institutions, relevant coursework
- **Projects**: Personal/professional projects with details and badges
- **Publications**: Research papers, articles, presentations
- **Thesis**: Academic thesis/dissertation details
- **Skills**: Technical skills, languages, etc.
- **Languages**: Language proficiency levels
- **Interests**: Hobbies, personal interests
- **Diplomas**: Certifications, licenses, awards

### Styling & Layout
Modify in `themes/jinli-cv/exampleSite/config.toml`:
- Colors: `colorPrimary`, `colorDark`, `colorLight`, etc.
- Layout: `section_order`, `side_section_order`
- Per-section styling: margins, padding, spacing
- Feature toggles: `showDownload`, `download_button` position

## 🖨️ Print & PDF Export

The CV is optimized for A4 printing:
1. Open your CV in the browser
2. Press `Ctrl+P` (or `Cmd+P` on Mac)
3. Settings:
   - **Paper size**: A4
   - **Margins**: None/Default (0.5cm top/bottom built-in)
   - **Scale**: 100%
   - **Background graphics**: **Enabled** (required for badges/gradients)
4. Click "Save as PDF" or "Print"

## 📄 License

This demo site is provided as-is for educational purposes. The jinli-cv (锦鲤简历) theme is licensed under the MIT License - see the [LICENSE](LICENSE) file and the [jinli-cv repository](https://github.com/jin-li/jinli-cv/blob/main/LICENSE) for details.

## 🙏 Credits

- **Original Theme**: [Almeida CV](https://github.com/ineesalmeida/almeida-cv) by Inês Almeida (MIT License)
- **Current Theme**: [jinli-cv](https://github.com/jin-li/jinli-cv) (锦鲤简历) by Jin Li (MIT License)
- **Demo Data**: Sample data for demonstration purposes only

---

*Last updated: July 2026*
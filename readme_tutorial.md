# Website Update Tutorial

This document provides step-by-step instructions on how to update the website. The website is built with [Hugo](https://gohugo.io/) and uses a modified version of the [PaperMod theme](https://github.com/adityatelange/hugo-PaperMod).

## Prerequisites

Before you begin, ensure you have the following installed:
- [Hugo](https://gohugo.io/installation/) (v0.128.2 or later recommended)
- [Git](https://git-scm.com/downloads) or [GitHub Desktop](https://desktop.github.com/)

## Local Development Workflow

1. **Clone the repository** (if you haven't already):
   ```bash
   git clone https://github.com/yourusername/Khayrul.me.git
   cd Khayrul.me
   ```

2. **Start the local development server**:
   ```bash
   hugo server
   ```
   This will start a local server at http://localhost:1313 where you can preview your changes in real-time.

3. **Make your changes** to the content files (see sections below).

4. **Preview your changes** in the browser at http://localhost:1313.

## Updating Existing Content

### Updating Pages

The main content pages are located in the `content/` directory:

- **CV**: Edit `content/cv/index.md`
- **Contact Information**: Edit `content/contact/index.md`
- **Office Hours**: Edit `content/officehours.md`
- **Location**: Edit `content/location.md`

### Updating Papers

Papers are stored in the `content/papers/` directory, with each paper in its own subdirectory:

1. Navigate to the specific paper directory (e.g., `content/papers/paper1/`)
2. Edit the `index.md` file within that directory
3. Update any associated files (PDFs, images) in the same directory

### Updating Projects

Projects are stored in the `content/projects/` directory, with each project in its own subdirectory:

1. Navigate to the specific project directory (e.g., `content/projects/projects1/`)
2. Edit the `index.md` file within that directory
3. Update any associated files (images, code samples) in the same directory

## Adding New Content

### Adding a New Paper

1. Create a new directory in `content/papers/` (e.g., `content/papers/paper13/`)
2. Create an `index.md` file in this directory with the following structure:
   ```markdown
   ---
   title: "Paper Title"
   date: YYYY-MM-DD
   tags: ["tag1", "tag2"]
   author: ["Author 1", "Author 2"]
   description: "Brief description of the paper"
   summary: "Summary of the paper"
   cover:
       image: "cover-image.jpg"
       alt: "Cover image description"
       relative: true
   ---

   Paper content goes here...
   ```
3. Add any associated files (PDFs, images) to the same directory

### Adding a New Project

1. Create a new directory in `content/projects/` (e.g., `content/projects/projects6/`)
2. Create an `index.md` file in this directory with the following structure:
   ```markdown
   ---
   title: "Project Title"
   date: YYYY-MM-DD
   tags: ["tag1", "tag2"]
   author: ["Author 1", "Author 2"]
   description: "Brief description of the project"
   summary: "Summary of the project"
   cover:
       image: "cover-image.jpg"
       alt: "Cover image description"
       relative: true
   ---

   Project content goes here...
   ```
3. Add any associated files (images, code samples) to the same directory

## Updating Static Files

Static files (images, PDFs, etc.) that are not associated with specific content should be placed in the `static/` directory:

- **CV PDF**: Replace `static/CV.pdf` with your updated CV
- **Profile Picture**: Replace `static/Khayrul.jpg` with your updated photo
- **Favicon**: Update favicon files in the `static/` directory if needed

## Compiling and Deploying

Once you're satisfied with your changes:

1. **Compile the website**:
   ```bash
   hugo
   ```
   This will generate the static website in the `public/` directory.

2. **Commit and push your changes**:
   
   Using Git:
   ```bash
   git add .
   git commit -m "Update website content"
   git push origin main
   ```
   
   Or using GitHub Desktop:
   - Open GitHub Desktop
   - Review your changes
   - Add a commit message
   - Click "Commit to main"
   - Click "Push origin"

3. **Deployment**:
   The website will be automatically built and deployed to GitHub Pages via the GitHub Action configured in `.github/workflows/hugo.yml`.

## Troubleshooting

### Common Issues

1. **Hugo version mismatch**:
   - Check your Hugo version with `hugo version`
   - Update to the recommended version if needed

2. **Missing content**:
   - Ensure your content files have the correct front matter
   - Check that file paths are correct

3. **Deployment failures**:
   - Check the GitHub Actions tab in your repository for error messages
   - Ensure GitHub Pages is properly configured in your repository settings

4. **CSS/styling issues**:
   - Clear your browser cache
   - Check for any custom CSS in `assets/css/`

### Getting Help

If you encounter issues not covered here, refer to:
- [Hugo Documentation](https://gohugo.io/documentation/)
- [PaperMod Documentation](https://github.com/adityatelange/hugo-PaperMod/wiki)
- Open an issue in the GitHub repository

## Advanced Customization

### Modifying Templates

The website templates are located in the `layouts/` directory. Modify these files to change the structure and appearance of the website:

- **Base Template**: `layouts/_default/baseof.html`
- **List Pages**: `layouts/_default/list.html`
- **Single Pages**: `layouts/_default/single.html`
- **Partials** (reusable components): `layouts/partials/`

### Customizing CSS

Custom CSS can be added or modified in the `assets/css/` directory.

# GitHub Articles Integration Setup

This guide explains how to use GitHub as your article storage and automatically sync articles to your website.

## Overview

Instead of storing articles locally, you can:
1. Create a GitHub repository for your articles
2. Upload articles and images to that repo
3. Your website automatically fetches articles from GitHub

**Benefits:**
- ✅ Easy to update (just edit files on GitHub)
- ✅ Version control for your articles
- ✅ Can be public or private
- ✅ No API limitations
- ✅ Images stored alongside articles
- ✅ Works immediately after setup

## Setup Instructions

### Step 1: Create a GitHub Repository

1. Go to [GitHub](https://github.com) and create a new repository
2. Name it something like `my-articles` or `website-articles`
3. Make it **public** (so your website can access it) OR **private** (if you use a GitHub token)
4. Initialize with a README (optional)

### Step 2: Set Up Repository Structure

Create this structure in your repository:

```
your-repo/
├── articles.json          # Main articles file
├── images/                # Folder for article images
│   └── (your images here)
└── README.md
```

### Step 3: Create articles.json

Create a file called `articles.json` in the root of your repository with this structure:

```json
{
  "articles": [
    {
      "id": "my-first-article",
      "title": "My First Article",
      "excerpt": "A brief description of the article...",
      "content": "<p>Full HTML content of your article...</p>",
      "image": "https://raw.githubusercontent.com/YOUR_USERNAME/YOUR_REPO/main/images/article-1.jpg",
      "publishedDate": "2024-01-15T00:00:00Z",
      "linkedInUrl": "https://www.linkedin.com/posts/your-article-url"
    }
  ]
}
```

### Step 4: Upload Images

1. Create an `images/` folder in your repository
2. Upload your article images to this folder
3. Use the raw GitHub URL format for image paths:
   ```
   https://raw.githubusercontent.com/YOUR_USERNAME/YOUR_REPO/main/images/filename.jpg
   ```

### Step 5: Configure Your Website

#### Option A: Environment Variables (Recommended)

Create a `.env.local` file in your website project root:

```env
USE_GITHUB_ARTICLES=true
GITHUB_ARTICLES_REPO=your-username/your-repo-name
GITHUB_ARTICLES_BRANCH=main
GITHUB_ARTICLES_PATH=articles.json
```

#### Option B: Update API Directly

Edit `pages/api/articles.js` and update these constants:

```javascript
const GITHUB_REPO = 'your-username/your-repo-name'
const GITHUB_BRANCH = 'main'
const GITHUB_PATH = 'articles.json'
const USE_GITHUB = true
```

### Step 6: Test

1. Restart your Next.js development server
2. Visit `/articles` on your website
3. Your articles from GitHub should appear!

## Adding New Articles

### Method 1: GitHub Web Interface

1. Go to your articles repository on GitHub
2. Click on `articles.json`
3. Click the pencil icon (✏️) to edit
4. Add a new article to the `articles` array
5. Upload images to the `images/` folder first
6. Commit your changes

### Method 2: GitHub Desktop / Git CLI

1. Clone your articles repository locally
2. Edit `articles.json` and add your article
3. Add images to the `images/` folder
4. Commit and push your changes

### Method 3: Use the Template

Copy the structure from `.github-articles-template/` in this project as a starting point.

## Article Format

Each article should have this structure:

```json
{
  "id": "unique-article-id",
  "title": "Article Title",
  "excerpt": "Brief description (150-200 chars recommended)",
  "content": "<p>Full HTML content...</p>",
  "image": "https://raw.githubusercontent.com/USER/REPO/main/images/image.jpg",
  "publishedDate": "2024-01-15T10:00:00Z",
  "linkedInUrl": "https://www.linkedin.com/posts/..."
}
```

### Field Descriptions

- **id**: Unique identifier (use kebab-case, e.g., "my-article-title")
- **title**: The article headline
- **excerpt**: Short preview text shown on article cards
- **content**: Full article in HTML format (supports `<p>`, `<h2>`, `<strong>`, `<em>`, `<a>`, etc.)
- **image**: Full URL to the image (use raw GitHub URLs)
- **publishedDate**: ISO 8601 format date (YYYY-MM-DDTHH:mm:ssZ)
- **linkedInUrl**: Link to your LinkedIn post

## Image Best Practices

1. **File Size**: Keep images under 1MB for faster loading
2. **Format**: Use JPG for photos, PNG for graphics
3. **Dimensions**: Recommended 1200x630px for article headers
4. **Naming**: Use descriptive names like `ai-implementation-guide.jpg`

## Workflow: Posting a New Article

1. **Post on LinkedIn** - Write and publish your article on LinkedIn
2. **Copy Content** - Copy the article text and any images
3. **Upload to GitHub**:
   - Upload images to `images/` folder
   - Get the raw GitHub URL for each image
   - Add article entry to `articles.json`
4. **Commit** - Save your changes
5. **Website Updates** - Your website will show the new article (may take a few minutes due to caching)

## Using Private Repositories

If you want to keep your articles repository private:

1. Create a GitHub Personal Access Token:
   - Go to GitHub Settings → Developer settings → Personal access tokens
   - Generate a token with `repo` scope
   
2. Update your API endpoint to include authentication:
   ```javascript
   const response = await fetch(rawUrl, {
     headers: {
       'Authorization': `token ${process.env.GITHUB_TOKEN}`,
       'Accept': 'application/json'
     }
   })
   ```

3. Add to `.env.local`:
   ```env
   GITHUB_TOKEN=your_token_here
   ```

## Troubleshooting

### Articles Not Appearing

1. **Check Configuration**: Verify your `GITHUB_ARTICLES_REPO` is correct (format: `username/repo-name`)
2. **Check File Path**: Ensure `GITHUB_ARTICLES_PATH` matches your file location
3. **Check Branch**: Make sure `GITHUB_ARTICLES_BRANCH` is correct (usually `main` or `master`)
4. **Check JSON Syntax**: Validate your `articles.json` file using a JSON validator
5. **Check Console**: Look for errors in your browser console or server logs

### Images Not Loading

1. **Use Raw URLs**: Make sure you're using raw GitHub URLs, not regular GitHub URLs
2. **Check Path**: Verify the image path in your repository matches the URL
3. **File Exists**: Ensure the image file is actually committed to the repository

### Caching Issues

Articles are cached for 5 minutes. If you don't see updates:
- Wait a few minutes
- Hard refresh your browser (Ctrl+F5 or Cmd+Shift+R)
- Clear your browser cache

## Example: Complete Workflow

1. **Create Repository**: `my-articles` on GitHub
2. **Add First Article**:
   ```json
   {
     "articles": [
       {
         "id": "welcome-post",
         "title": "Welcome to My Blog",
         "excerpt": "This is my first article...",
         "content": "<p>Welcome to my blog!</p>",
         "image": "https://raw.githubusercontent.com/username/my-articles/main/images/welcome.jpg",
         "publishedDate": "2024-01-15T10:00:00Z",
         "linkedInUrl": "https://www.linkedin.com/posts/..."
       }
     ]
   }
   ```
3. **Upload Image**: Add `welcome.jpg` to `images/` folder
4. **Configure Website**: Set `GITHUB_ARTICLES_REPO=username/my-articles` in `.env.local`
5. **View Results**: Visit `/articles` on your website

## Next Steps

- Set up a workflow to automatically sync from LinkedIn (see `LINKEDIN_SETUP.md`)
- Consider using GitHub Actions to automate article processing
- Add more metadata fields if needed (tags, categories, etc.)

## Support

If you need help:
1. Check the error messages in your browser console
2. Verify your GitHub repository is accessible
3. Test the raw GitHub URL directly in your browser
4. Check that your JSON is valid


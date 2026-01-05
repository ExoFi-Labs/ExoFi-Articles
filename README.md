# ExoFi Articles

This repository stores articles that are automatically synced to the ExoFi website.

## Repository Structure

```
ExoFi-Articles/
├── articles.json          # Main articles file
├── images/                # Folder for article images
│   └── (your images here)
└── README.md              # This file
```

## Quick Start

1. **Add a new article**: Edit `articles.json` and add your article to the `articles` array
2. **Upload images**: Add images to the `images/` folder
3. **Use raw GitHub URLs**: For images, use this format:
   ```
   https://raw.githubusercontent.com/ExoFi-Labs/ExoFi-Articles/main/images/filename.jpg
   ```

## Article Format

Each article should follow this structure:

```json
{
  "id": "unique-article-id",
  "title": "Article Title",
  "excerpt": "Brief description (150-200 chars recommended)",
  "content": "<p>Full HTML content...</p>",
  "image": "https://raw.githubusercontent.com/ExoFi-Labs/ExoFi-Articles/main/images/image.jpg",
  "publishedDate": "2024-01-15T10:00:00Z",
  "linkedInUrl": "https://www.linkedin.com/posts/..."
}
```

## Field Descriptions

- **id**: Unique identifier (use kebab-case, e.g., "my-article-title")
- **title**: The article headline
- **excerpt**: Short preview text shown on article cards
- **content**: Full article in HTML format (supports `<p>`, `<h2>`, `<strong>`, `<em>`, `<a>`, etc.)
- **image**: Full URL to the image (use raw GitHub URLs)
- **publishedDate**: ISO 8601 format date (YYYY-MM-DDTHH:mm:ssZ)
- **linkedInUrl**: Link to your LinkedIn post

## Adding Articles

### Method 1: GitHub Web Interface

1. Go to this repository on GitHub
2. Click on `articles.json`
3. Click the pencil icon (✏️) to edit
4. Add a new article to the `articles` array
5. Upload images to the `images/` folder first
6. Commit your changes

### Method 2: Git CLI / GitHub Desktop

1. Clone this repository locally
2. Edit `articles.json` and add your article
3. Add images to the `images/` folder
4. Commit and push your changes

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

## Repository Information

- **Repository**: [ExoFi-Labs/ExoFi-Articles](https://github.com/ExoFi-Labs/ExoFi-Articles)
- **Raw JSON URL**: `https://raw.githubusercontent.com/ExoFi-Labs/ExoFi-Articles/main/articles.json`
- **Images Base URL**: `https://raw.githubusercontent.com/ExoFi-Labs/ExoFi-Articles/main/images/`

## Support

For detailed setup instructions, see:
- `GITHUB_SETUP.md` - Complete GitHub integration guide
- `LINKEDIN_SETUP.md` - LinkedIn integration options


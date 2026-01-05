# LinkedIn Articles Integration Setup

This guide explains how to set up automatic syncing of articles from your LinkedIn profile to your website.

## Current Status

The articles page is set up and ready to display articles. However, **LinkedIn's API has significant limitations** for personal profiles, which makes automatic syncing challenging.

## Available Options

### Option 1: GitHub Repository (Recommended - Easy & Flexible) ⭐

Store your articles in a GitHub repository and have your website automatically fetch them. This is the easiest way to manage articles with version control and easy updates.

**See `GITHUB_SETUP.md` for complete instructions.**

**Quick Setup:**
1. Create a GitHub repository for your articles
2. Add `articles.json` with your articles
3. Upload images to an `images/` folder
4. Configure your website to fetch from GitHub
5. Update articles by editing files on GitHub

**Benefits:**
- ✅ Easy to update (just edit on GitHub)
- ✅ Version control for articles
- ✅ Images stored alongside articles
- ✅ No API limitations
- ✅ Works immediately

### Option 2: Manual Sync (Local File)

You can manually add articles to `data/articles.json`:

```json
{
  "articles": [
    {
      "id": "unique-article-id",
      "title": "Your Article Title",
      "excerpt": "Brief description that appears on the article card...",
      "content": "<p>Full HTML content of your article...</p>",
      "image": "/path/to/image.jpg",
      "publishedDate": "2024-01-15T00:00:00Z",
      "linkedInUrl": "https://www.linkedin.com/posts/your-article-url"
    }
  ]
}
```

**Steps:**
1. When you post a new article on LinkedIn, copy the article URL
2. Extract the content, title, and any images
3. Add it to `data/articles.json` in the format above
4. Restart your Next.js server if needed

### Option 3: LinkedIn API Integration (Limited Access)

LinkedIn's API v2 has very restricted access for personal profiles. To use it:

1. **Apply for LinkedIn API Access:**
   - Go to [LinkedIn Developers](https://www.linkedin.com/developers/)
   - Create a new app
   - Request access to the required permissions
   - Note: Personal profile access is often denied unless you're a partner

2. **If Approved:**
   - Get your Client ID and Client Secret
   - Set up OAuth flow
   - Implement the API calls in `scripts/sync-linkedin.js`
   - Set up environment variables for credentials

3. **Update the sync script:**
   - Uncomment and implement the `fetchFromLinkedInAPI()` function
   - Add your API credentials
   - Set up a cron job or scheduled task to run the sync

### Option 4: Third-Party Integration Services

Use automation platforms that can bridge LinkedIn and your website:

#### Zapier Integration:
1. Create a Zapier account
2. Set up a trigger: "New LinkedIn Post"
3. Add an action: "Webhook" that posts to your API endpoint
4. Create an API endpoint in `pages/api/sync-articles.js` to receive webhooks

#### Make.com (formerly Integromat):
Similar to Zapier, can monitor LinkedIn and sync to your site.

### Option 5: RSS Feed (If Available)

Some LinkedIn profiles have RSS feeds. If yours does:

1. Find your LinkedIn RSS feed URL
2. Use a library like `rss-parser` to fetch articles
3. Update `scripts/sync-linkedin.js` to parse RSS
4. Set up a scheduled job to sync periodically

### Option 6: Browser Extension / Manual Tool

Create a browser extension or bookmarklet that:
1. Extracts article content when you're viewing it on LinkedIn
2. Formats it correctly
3. Adds it to your `data/articles.json` file

## Recommended Approach

**Start with Option 1 (GitHub Repository)** because:
- It's immediate and works right away
- Easy to update articles (just edit on GitHub)
- Version control for your content
- Images stored alongside articles
- No API limitations or approval processes
- You have full control over formatting

**Alternative: Option 2 (Local Manual Sync)** if:
- You prefer not to use GitHub
- You want everything in your main project

**For automation, consider Option 4 (Zapier/Make.com)** if:
- You want to automatically sync from LinkedIn
- You post articles frequently
- You're willing to pay for the service

## File Structure

```
├── pages/
│   ├── articles.js          # Articles page
│   └── api/
│       └── articles.js      # API endpoint to fetch articles
├── components/
│   └── Articles.js         # Articles component
├── data/
│   └── articles.json        # Article data storage
├── scripts/
│   └── sync-linkedin.js    # Sync script (for future automation)
└── LINKEDIN_SETUP.md       # This file
```

## Testing

1. Visit `/articles` on your website
2. You should see the example article (or empty state if you removed it)
3. Add a new article to `data/articles.json`
4. Refresh the page to see it appear

## Next Steps

1. **Immediate:** Add your existing LinkedIn articles manually to `data/articles.json`
2. **Short-term:** Set up a workflow to manually add new articles when you post them
3. **Long-term:** Explore automation options (Zapier, Make.com, or custom solution)

## Support

If you need help implementing any of these options, or if LinkedIn's API access changes in the future, you can:
- Update the sync script with new API endpoints
- Modify the article data structure if needed
- Add new features to the articles page

## Notes

- Images should be placed in the `public/` directory and referenced with paths like `/image.jpg`
- Article content supports HTML formatting
- Dates should be in ISO 8601 format (YYYY-MM-DDTHH:mm:ssZ)
- The `linkedInUrl` should point to the actual LinkedIn post/article


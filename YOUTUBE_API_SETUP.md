# YouTube API Setup Guide

This guide will help you set up the YouTube Data API v3 to enable real YouTube search functionality in the app.

## Prerequisites

- A Google account
- Basic knowledge of web development

## Step-by-Step Setup

### 1. Create a Google Cloud Project

1. Go to [Google Cloud Console](https://console.cloud.google.com/)
2. Click "Select a project" at the top of the page
3. Click "New Project"
4. Enter a project name (e.g., "Offline Spotify App")
5. Click "Create"

### 2. Enable YouTube Data API v3

1. In your new project, go to the [API Library](https://console.cloud.google.com/apis/library)
2. Search for "YouTube Data API v3"
3. Click on "YouTube Data API v3"
4. Click "Enable"

### 3. Create API Credentials

1. Go to the [Credentials page](https://console.cloud.google.com/apis/credentials)
2. Click "Create Credentials" → "API Key"
3. Copy the generated API key

### 4. Configure the API Key

1. Open `src/config/youtube.js` in your project
2. Replace `'YOUR_YOUTUBE_API_KEY_HERE'` with your actual API key:

```javascript
export const YOUTUBE_CONFIG = {
  API_KEY: 'AIzaSyYourActualAPIKeyHere', // Replace with your actual API key
  // ... rest of config
};
```

### 5. Restrict the API Key (Recommended)

For security, restrict your API key to only YouTube Data API v3:

1. In the [Credentials page](https://console.cloud.google.com/apis/credentials)
2. Click on your API key
3. Under "Application restrictions", select "HTTP referrers (websites)"
4. Add your domain (for development, you can add `localhost:*`)
5. Under "API restrictions", select "Restrict key"
6. Select "YouTube Data API v3" from the dropdown
7. Click "Save"

## Usage Limits

- **Free Tier**: 10,000 requests per day
- **Paid Tier**: $5 per 1,000 additional requests

For most personal use, the free tier is sufficient.

## Testing the Setup

1. Start the app: `npm start`
2. Go to the search page
3. The API key notice should disappear
4. Try searching for any song - you should get real YouTube results

## Troubleshooting

### "API key not configured" message
- Make sure you've replaced the placeholder in `src/config/youtube.js`
- Check that the API key is correctly copied

### "YouTube API error" messages
- Verify that YouTube Data API v3 is enabled in your Google Cloud project
- Check that your API key has the correct permissions
- Ensure you haven't exceeded your daily quota

### No search results
- Check the browser console for error messages
- Verify your API key restrictions allow requests from your domain
- Try searching for popular terms first

## Security Notes

- Never commit your API key to version control
- Use environment variables in production
- Restrict your API key to specific domains and APIs
- Monitor your API usage in the Google Cloud Console

## Environment Variables (Production)

For production deployment, use environment variables:

1. Create a `.env` file in your project root:
```
REACT_APP_YOUTUBE_API_KEY=your_actual_api_key_here
```

2. Update `src/config/youtube.js`:
```javascript
export const YOUTUBE_CONFIG = {
  API_KEY: process.env.REACT_APP_YOUTUBE_API_KEY || 'YOUR_YOUTUBE_API_KEY_HERE',
  // ... rest of config
};
```

3. Add `.env` to your `.gitignore` file

## Support

If you encounter issues:
1. Check the [YouTube Data API documentation](https://developers.google.com/youtube/v3)
2. Review the [Google Cloud Console](https://console.cloud.google.com/) for quota and error details
3. Check the browser console for detailed error messages 
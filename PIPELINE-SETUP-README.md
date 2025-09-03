# Ragoo! Chrome Extension - Pipeline Configuration Setup

## Overview

The Ragoo! Chrome Extension now uses a JSON configuration file hosted on GitHub to manage the pipeline stages. This allows for easy updates to match your Zoho Recruit pipeline without needing to update the extension code.

## Setup Instructions

### 1. Create a GitHub Repository

1. Create a new public repository on GitHub (or use an existing one)
2. Upload the `pipeline-config.json` file to the repository
3. Make sure the repository is public so the extension can access it

### 2. Update the GitHub URL

1. Open `js/content.js` in your extension folder
2. Find the `PIPELINE_CONFIG` object at the top of the file (around line 8)
3. Update the `GITHUB_URL` with your actual GitHub raw file URL:

```javascript
const PIPELINE_CONFIG = {
	// Update this URL to point to your GitHub hosted JSON file
	GITHUB_URL:
		"https://raw.githubusercontent.com/YOUR-USERNAME/YOUR-REPO/main/pipeline-config.json",
	// ... rest of config
};
```

**Replace:**

- `YOUR-USERNAME` with your GitHub username
- `YOUR-REPO` with your repository name

### 3. Configure Your Pipeline

Edit the `pipeline-config.json` file to match your Zoho Recruit pipeline:

```json
{
	"pipeline": {
		"version": "1.0.0",
		"lastUpdated": "2025-01-25",
		"description": "Zoho Recruit Pipeline Configuration for Ragoo! Extension",
		"stages": [
			{
				"label": "Applied",
				"short": "APL",
				"value": "Applied",
				"background": "#a54444",
				"badgeClass": "apple-blossom"
			}
			// ... add more stages as needed
		]
	}
}
```

### 4. Stage Configuration Options

Each stage object supports the following properties:

- **label**: Display name shown in the dropdown
- **short**: Abbreviated version (used for compact displays)
- **value**: Exact value that matches your Zoho status (must match exactly)
- **background**: Hex color code for the stage background
- **badgeClass**: CSS class name for styling (optional)

### 5. Available Badge Classes

The extension supports these predefined badge classes:

- `apple-blossom` - Reddish color (#a54444)
- `sheen-gold` - Gold color (#d0a72b)
- `darkgreen` - Dark green (#00868c)
- `darkblue` - Dark blue (#1e3a8a)
- `lightgreen` - Light green (#1a936a)
- `red` - Red (#ed0707)
- `yellow` - Yellow (#f59e0b)
- `cadet` - Gray (#6b7280)

### 6. Testing the Configuration

1. Load your extension in Chrome
2. Navigate to any Zoho Recruit page where the dropdown should appear
3. Check the browser console for any error messages
4. If you see "❌ Pipeline configuration error - check the items", verify:
   - Your GitHub URL is correct and accessible
   - The JSON file is valid
   - The repository is public

### 7. Debugging

To manually refresh the pipeline configuration:

1. Open browser developer tools (F12)
2. Go to the Console tab
3. Type: `refreshPipelineConfiguration()`
4. Press Enter

This will clear the cache and reload the configuration from GitHub.

### 8. Cache Management

The extension caches the pipeline configuration for 1 hour to improve performance. The cache is automatically cleared when:

- The cache expires (after 1 hour)
- You call `refreshPipelineConfiguration()`
- The page is refreshed

## Troubleshooting

### Common Issues

1. **"Pipeline configuration error"** message appears:

   - Check that your GitHub URL is correct
   - Verify the repository is public
   - Ensure the JSON file is valid (use a JSON validator)

2. **Dropdown not appearing**:

   - Check browser console for JavaScript errors
   - Verify you're on a supported Zoho Recruit page
   - Try refreshing the page

3. **Wrong status values**:
   - Ensure the "value" field in your JSON exactly matches the status values in Zoho
   - Check capitalization and spacing

### Getting Status Values from Zoho

To find the exact status values used in your Zoho Recruit:

1. Go to Zoho Recruit Setup > Customize > Pipeline
2. Note the exact text of each status
3. Use these exact values in the "value" field of your JSON configuration

## Example GitHub Setup

1. Create repository: `https://github.com/yourusername/ragoo-pipeline`
2. Upload `pipeline-config.json` to the root
3. Get raw URL: `https://raw.githubusercontent.com/yourusername/ragoo-pipeline/main/pipeline-config.json`
4. Update the `GITHUB_URL` in `content.js`

That's it! Your extension will now load the pipeline configuration from GitHub and show error messages if something goes wrong.

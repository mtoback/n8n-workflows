N# AI Cybersecurity Blog Generator - Setup Guide

## Overview

This n8n workflow automatically generates blog posts from RSS feeds about AI and cybersecurity. It runs daily, fetches relevant articles, and uses AI to create comprehensive blog posts.

**Version:** 1.0  
**Created:** October 21, 2025  
**Estimated Cost:** $0.05-0.15 per run

---

## Quick Start

### Step 1: Import the Workflow

1. Open your n8n instance
2. Click the **"+"** button in the top right
3. Select **"Import from File"** or **"Import from URL"**
4. Upload the `ai_blog_generator_workflow.json` file
5. The workflow will appear on your canvas with all nodes and documentation

### Step 2: Required Credentials

You'll need to set up the following credentials in n8n:

#### 1. **AI Model Credentials** (Choose one)
   - **OpenAI**: Get API key from https://platform.openai.com/api-keys
   - **Anthropic Claude**: Get API key from https://console.anthropic.com
   - **Google AI**: Get API key from https://makersuite.google.com
   
   **To configure:**
   - Click on the "Generate Blog Post" node
   - Click "Create New Credential"
   - Enter your API key
   - Save

#### 2. **Google Sheets Credentials**
   - **Option A - OAuth2:** 
     - Click "Create New Credential" in the Google Sheets node
     - Follow Google OAuth flow
     - Grant necessary permissions
   
   - **Option B - Service Account:**
     - Create a service account in Google Cloud Console
     - Download JSON key
     - Upload to n8n credentials
     - Share your Google Sheet with the service account email

#### 3. **Gmail Credentials (OAuth2)**
   - **Setup:**
     - Click on any Gmail node (Send Success Email, Send Failure Email, etc.)
     - Click "Create New Credential"
     - Select "OAuth2 (recommended)"
     - Follow the Google OAuth flow
     - Grant Gmail send permissions
   
   **Note:** Gmail uses OAuth2, which is simpler and more secure than SMTP!
   
   **To configure:**
   - Click on any email node (Send Success Email, Send Failure Email, etc.)
   - Click "Create New Credential" 
   - Follow Google OAuth flow
   - Grant necessary permissions

### Step 3: Configure Google Sheets

1. **Create a new Google Sheet** with these columns:
   ```
   | Date | Source Title | Source URL | Blog Post | Status | Error Message |
   ```

2. **Get the Sheet ID:**
   - Open your Google Sheet
   - Look at the URL: `https://docs.google.com/spreadsheets/d/YOUR_SHEET_ID_HERE/edit`
   - Copy the `YOUR_SHEET_ID_HERE` part

3. **Update the workflow:**
   - Click on the "Save to Google Sheets" node
   - Replace `YOUR_SHEET_ID_HERE` with your actual Sheet ID
   - Update the sheet name if you're not using "Sheet1"

### Step 4: Configure Gmail Notifications

Update the recipient email addresses in these Gmail nodes:
- **Send Success Email**: Change `your-email@domain.com` to your email
- **Send Failure Email**: Change `your-email@domain.com` to your email  
- **Send No Articles Email**: Change `your-email@domain.com` to your email

The Gmail node uses OAuth2, so you don't need to configure any SMTP settings - just authorize your Google account!

### Step 5: Test the Workflow

**IMPORTANT:** Test before activating!

1. Click the **"Test Workflow"** button (not "Execute Workflow")
2. Watch each node execute
3. Check for any errors (red nodes)
4. Verify:
   - âœ… RSS feed returns articles
   - âœ… Filter finds AI-related content
   - âœ… Articles are fetched
   - âœ… AI generates blog posts
   - âœ… Google Sheets is updated
   - âœ… Gmail is received

### Step 6: Activate the Workflow

1. Click the **"Save"** button
2. Toggle the **"Active"** switch in the top right
3. The workflow will now run automatically at 9:00 AM daily

---

##  Configuration Options

### Change the RSS Feed

**Current:** Bleeping Computer  
**To change:**
1. Click the "RSS Feed Read" node
2. Update the URL field
3. See the sticky note for other feed recommendations

**Suggested Feeds:**
- `https://www.bleepingcomputer.com/feed/` (Current)
- `https://krebsonsecurity.com/feed/`
- `https://www.darkreading.com/rss.xml`
- `https://feeds.feedburner.com/TheHackersNews`

### Adjust the Schedule

**Current:** Daily at 9:00 AM  
**To change:**
1. Click the "Schedule Trigger" node
2. Modify the hour/minute settings
3. Or change to a different interval (every 6 hours, etc.)

### Modify Filter Keywords

**Current keywords:**
- AI, artificial intelligence
- machine learning, ML
- neural network
- deep learning
- LLM, large language model

**To add more keywords:**
1. Click the "Filter AI Keywords" node
2. Add additional conditions
3. Use OR logic to match any keyword

### Change Article Limit

**Current:** 3 articles maximum  
**To change:**
1. Click the "Limit Articles" node
2. Update the "Max Items" field
3. Consider cost implications (each article = API call)

### Customize the AI Prompt

**To modify:**
1. Click the "Generate Blog Post" node
2. Edit the "Prompt (User Message)" field
3. Adjust tone, length, or focus areas
4. Test with a manual execution

---

## Troubleshooting

### Problem: No articles being generated

**Solutions:**
- Check if RSS feed is accessible (test the URL in your browser)
- Verify filter keywords aren't too restrictive
- Look at execution log for specific errors
- Try relaxing the filter (fewer keywords)

### Problem: AI generation fails

**Solutions:**
- Verify API credentials are correct and active
- Check API rate limits and usage
- Ensure you have sufficient credits/quota
- Try reducing max_tokens if hitting limits

### Problem: Google Sheets not updating

**Solutions:**
- Verify credentials are still valid
- Check Sheet ID is correct
- Ensure n8n has permission to edit the sheet
- Check if sheet name matches exactly

### Problem: Not receiving Gmail notifications

**Solutions:**
- Verify Gmail OAuth2 credentials are authorized
- Check recipient email address is correct
- Look in spam/junk folder
- Ensure Gmail API is enabled in Google Cloud Console
- Re-authorize the Gmail credential if needed
- Check Gmail send quota hasn't been exceeded

### Problem: RSS feed returns no results

**Solutions:**
- RSS feed might be down temporarily
- Check if feed URL has changed
- Try alternative feeds from the recommendations
- Verify network connectivity in n8n

### Problem: Poor quality blog posts

**Solutions:**
- Adjust the AI prompt for better instructions
- Increase max_tokens for longer responses
- Try a different AI model (GPT-4 vs Claude vs others)
- Provide more context in the prompt

---

## Understanding the Workflow

### Flow Diagram

```
Schedule (9AM daily)
    â†“
RSS Feed Read (Bleeping Computer)
    â†“
Filter (AI keywords)
    â†“
Check if articles found
    â†“                    â†“
Articles Found      No Articles
    â†“                    â†“
Limit (3 max)       Send Info Email
    â†“
Fetch Full Content (HTTP)
    â†“
Extract Text (HTML)
    â†“
Generate Blog (AI)
    â†“
Format Output
    â†“
Save to Google Sheets
    â†“
Aggregate Results
    â†“
Check Success
    â†“                    â†“
Success             Failure
    â†“                    â†“
Success Email      Failure Email
```

### Error Handling

**Every critical node has:**
- `continueOnFail: true` - Workflow continues even if node fails
- Retry logic - Automatically retries on failure
- Error logging - Failures are logged to Google Sheets

**Retry Strategy:**
- RSS Feed: 3 retries, 60 second intervals
- HTTP Request: 3 retries, 30 second intervals
- AI Generation: 2 retries, 60 second intervals
- Google Sheets: 2 retries, 10 second intervals

---

## Cost Estimation

**Per Execution (3 articles):**
- OpenAI GPT-4: ~$0.15
- OpenAI GPT-3.5: ~$0.02
- Anthropic Claude: ~$0.10
- Google Sheets: Free
- Gmail: Free

**Monthly (30 days):**
- GPT-4: ~$4.50
- GPT-3.5: ~$0.60
- Claude: ~$3.00

**To reduce costs:**
- Use GPT-3.5 instead of GPT-4
- Reduce article limit
- Reduce max_tokens in AI node
- Run less frequently (every 2-3 days)

---

## Customization Ideas

### 1. Multiple RSS Feeds
Add multiple RSS Feed Read nodes, all connecting to the Filter node.

### 2. Different AI Models
Create parallel paths using different AI models and compare results.

### 3. Content Quality Check
Add a second AI node to review and score the generated content.

### 4. Auto-Publish to CMS
Replace Google Sheets with WordPress, Ghost, or other CMS nodes.

### 5. Social Media Sharing
Add nodes to post summaries to Twitter, LinkedIn, etc.

### 6. Slack Notifications
Replace Gmail with Slack webhooks for team notifications.

### 7. Content Calendar
Add logic to spread posts throughout the week instead of all at once.

### 8. SEO Optimization
Add a node to generate meta descriptions and keywords.

---

##  Maintenance

### Weekly Tasks
- Check Google Sheets for errors
- Review blog post quality
- Monitor API usage and costs

### Monthly Tasks
- Update filter keywords based on trends
- Review and optimize AI prompts
- Check for new RSS feed sources
- Verify all credentials are still valid

### As Needed
- Adjust article limit based on volume
- Fine-tune filter keywords
- Update AI model or parameters
- Add/remove RSS feeds

---

## Support & Resources

- **n8n Documentation:** https://docs.n8n.io
- **n8n Community:** https://community.n8n.io
- **OpenAI API Docs:** https://platform.openai.com/docs
- **Google Sheets API:** https://developers.google.com/sheets

---

## License & Credits

This workflow is provided as-is for educational and commercial use.

**Created by:** Your Name  
**Date:** October 21, 2025  
**Version:** 1.0

---

## Setup Checklist

Use this checklist to ensure everything is configured:

- [ ] Workflow imported successfully
- [ ] AI model credentials configured
- [ ] Google Sheets credentials configured
- [ ] Gmail credentials configured (OAuth2)
- [ ] Google Sheet created with correct columns
- [ ] Sheet ID updated in workflow
- [ ] Recipient email addresses updated in all Gmail nodes
- [ ] Workflow tested successfully
- [ ] Test Gmail received
- [ ] Google Sheets updated with test data
- [ ] Workflow saved
- [ ] Workflow activated
- [ ] Schedule trigger verified

**Once all items are checked, you're ready to go! ðŸš€**

---

## Version History

**v1.0 (October 21, 2025)**
- Initial release
- Single RSS feed support
- AI blog generation
- Google Sheets output
- Email notifications
- Comprehensive error handling
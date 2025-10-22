# AI Cybersecurity Blog Generator for n8n

**An automated workflow that generates blog posts from RSS feeds using AI**

## ðŸ†• **NEW: Intelligent AI-Powered Classification!**
No more keyword matching! The workflow now uses AI to understand if articles are truly about both AI and cybersecurity. It knows that "Cursor IDE vulnerabilities" is relevant but "SharePoint attacks" is not. See [AI_CLASSIFIER_UPGRADE.md](AI_CLASSIFIER_UPGRADE.md) for details.

---

## ðŸ“¦ What's Included

This package contains everything you need to set up an automated AI-powered blog generator:

### 1. **ai_blog_generator_workflow.json**
The complete n8n workflow file ready to import. Includes:
- âœ… Schedule trigger (daily at 9 AM)
- âœ… RSS feed reader (Bleeping Computer)
- âœ… **ðŸ†• AI-powered article classifier** (intelligent filtering)
- âœ… HTTP article fetcher
- âœ… HTML text extraction
- âœ… AI blog post generation
- âœ… Google Sheets output
- âœ… Gmail notifications (success/failure)
- âœ… Comprehensive error handling
- âœ… 13 documentation sticky notes

### 3. **AI_CLASSIFIER_UPGRADE.md**
Detailed explanation of the new AI-powered classification system:
- How it works
- Examples of what it catches vs filters
- Cost implications
- Configuration options
- Troubleshooting guide

### 2. **SETUP_GUIDE.md**
A detailed step-by-step guide covering:
- Import instructions
- Credential setup (AI, Google Sheets, Email)
- Configuration options
- Testing procedures
- Troubleshooting tips
- Cost estimates
- Customization ideas

---

## ðŸš€ Quick Start (5 Minutes)

1. **Import** the workflow into n8n
2. **Configure** three credentials:
   - AI model (OpenAI/Claude/etc.)
   - Google Sheets
   - Gmail (OAuth2)
3. **Update** your Google Sheet ID
4. **Test** the workflow
5. **Activate** and let it run!

ðŸ“– **Read SETUP_GUIDE.md for detailed instructions**

---

## âœ¨ Key Features

- ðŸ¤– **AI-Powered**: Uses GPT-4, Claude, or other LLMs to generate professional blog posts
- ðŸ§  **Intelligent Filtering**: AI classifier understands context (not just keywords!)
- ðŸ“° **RSS Integration**: Monitors cybersecurity news feeds automatically
- ðŸŽ¯ **Smart Classification**: Knows the difference between SharePoint attacks and Cursor IDE vulnerabilities
- ðŸ’¾ **Google Sheets**: Stores all generated content in an organized spreadsheet
- ðŸ“§ **Gmail Alerts**: Notifies you of successes, failures, and when no articles are found
- ðŸ”„ **Error Recovery**: Automatic retries and graceful failure handling
- ðŸ“Š **Well-Documented**: 13 sticky notes explain every part of the workflow
- ðŸ’° **Cost-Effective**: ~$0.20 per run, ~$6/month

---

## ðŸ“‹ Requirements

- **n8n instance** (cloud or self-hosted)
- **AI API key** (OpenAI, Anthropic, Google AI, etc.)
- **Google account** (for Google Sheets and Gmail)


---

## ðŸŽ¯ What It Does

1. **Every day at 9 AM**, the workflow wakes up
2. **Fetches** the latest articles from Bleeping Computer RSS feed
3. **ðŸ†• AI Classifier analyzes** each article to determine if it's truly about AI + cybersecurity
4. **Limits** to 3 relevant articles (to control costs)
5. **Fetches** the full article content from each URL
6. **Extracts** clean text from the HTML
7. **Sends** to AI with a prompt to generate a blog post
8. **Formats** the output with metadata
9. **Saves** to Google Sheets
10. **Sends** you a Gmail with the results

**Result:** Professional blog posts ready to publish or edit!

---

## ðŸ’¡ Perfect For

- ðŸ” Security bloggers who need content ideas
- ðŸ“ Content creators covering AI security
- ðŸ¢ Companies needing regular security updates
- ðŸ“° Newsletter writers tracking AI threats
- ðŸŽ“ Educators teaching cybersecurity topics
- ðŸ”¬ Researchers monitoring AI security trends

---

## ðŸ”§ Customization

The workflow is fully customizable:

- âœï¸ Change the RSS feed (16 alternatives provided)
- â° Adjust the schedule (hourly, weekly, etc.)
- ðŸ” Modify filter keywords
- ðŸ“ˆ Increase/decrease article limit
- ðŸ¤– Customize AI prompt and tone
- ðŸ“Š Output to WordPress, Notion, or other platforms
- ðŸ“± Send to Slack instead of email

---

## ðŸ“Š Architecture Overview

```
Daily Schedule â†’ RSS Feed â†’ Filter Keywords â†’ Limit to 3
    â†“
Fetch Full Articles â†’ Extract Text â†’ AI Generation
    â†“
Format Output â†’ Google Sheets â†’ Gmail Notification
```

**Error handling at every step ensures you're always notified!**

---

## ðŸ’° Estimated Costs

| Component | Cost |
|-----------|------|
| n8n | Free (self-hosted) or $20/mo (cloud) |
| OpenAI GPT-4 | ~$0.21 per run = ~$6.30/month |
| OpenAI GPT-3.5 | ~$0.03 per run = ~$0.90/month |
| Google Sheets | Free |
| Gmail | Free |

**Note:** Costs include both AI classifier (~$0.02) and blog generator (~$0.05-0.15) per article.

**Recommendation:** Start with GPT-3.5 to test, upgrade to GPT-4 for better quality

---

## ðŸ“– Documentation

The workflow includes **13 sticky notes** that explain:

1. Workflow overview and quick stats
2. RSS feed configuration
3. Content filtering strategy
4. Cost control and article limits
5. Article fetching process
6. AI generation settings
7. Google Sheets output format
8. Error handling approach
9. Email notification settings
10. Troubleshooting guide
11. Error recovery strategy
12. Manual testing instructions
13. Quick reference card

**You'll never be confused about what a node does!**

---

## ðŸ†˜ Need Help?

1. **Read SETUP_GUIDE.md** - Covers 99% of questions
2. **Check the sticky notes** - In-workflow documentation
3. **n8n Community** - https://community.n8n.io
4. **n8n Docs** - https://docs.n8n.io

---

## âœ… Next Steps

1. **Import** `ai_blog_generator_workflow.json` into n8n
2. **Read** `SETUP_GUIDE.md` from top to bottom
3. **Follow** the setup checklist
4. **Test** the workflow
5. **Activate** and enjoy automated blog generation!

---

## ðŸŽ‰ You're Ready!

This is a **production-ready workflow** with:
- âœ… Professional error handling
- âœ… Comprehensive documentation
- âœ… Cost optimization
- âœ… Flexible customization
- âœ… Real-world tested patterns

**Import, configure, and you'll have AI-generated blog posts by tomorrow morning!**

---

**Questions? Start with SETUP_GUIDE.md - it's got everything you need! ðŸ“š**

*Created: October 21, 2025 | Version 1.0*
# TECH-NEWS-RESEARCH-AGENT
# Autonomous Tech News Research and Distribution Agent 🤖📰

## Overview ℹ️

This n8n workflow automates the process of researching, curating, and distributing daily technology news digests. The agent runs on a schedule, fetches articles from multiple tech news sources, uses AI to analyze and select the most relevant stories, and delivers formatted reports via email and Discord.

## How It Works ⚙️

### Workflow Components 🔗

1. **Scheduler** (`Daily Schedule`)
   - Triggers the workflow daily at 8:00 AM

2. **News Sources** (RSS Feed Readers)
   - Hacker News: `https://news.ycombinator.com/rss?utm_source=chatgpt.com`
   - TechCrunch: `https://techcrunch.com/feed/?utm_source=chatgpt.com`
   - The Verge: `https://www.theverge.com/rss/index.xml`

3. **Article Processing Pipeline**
   - **Combine All Articles**: Merges feeds from all three sources
   - **Code in JavaScript**: Formats the first 15 articles into a standardized text format (Title and Link)
   - **Categorize & Summarize**: AI agent that:
     - Analyzes all articles using language models
     - Filters for genuine technology news (ignoring blogs, opinions, tutorials, etc.)
     - Prioritizes AI news, major announcements, product launches, cybersecurity, funding, acquisitions, and open-source releases
     - Selects 2 most important unique stories
     - Generates two reports:
       - **Email Report**: HTML-formatted with detailed summaries (5 bullet points each)
       - **Discord Report**: Markdown-formatted under 1500 characters

4. **Distribution Channels** 📧💬
   - **Email**: Sends formatted HTML report via Gmail
   - **Discord**: Posts to configured channel via webhook

### AI Agent Details 🤖

The workflow uses a LangChain agent with:
- **Language Models**: 
  - Primary: OpenRouter (openai/gpt-oss-120b:free)
  - Alternative: Groq (llama-3.1-8b-instant) - currently disconnected in this version
- **Tools**: Tavily search for additional context when needed
- **Prompt Engineering**: Detailed instructions guide the AI to:
  - Focus exclusively on technology news
  - Apply specific prioritization criteria
  - Avoid duplicate topics
  - Follow exact formatting templates for both output channels

## Features ✨

- **Automated Daily Delivery**: Runs without manual intervention
- **Multi-source Aggregation**: Combines Hacker News, TechCrunch, and The Verge
- **Intelligent Curation**: AI filters noise and highlights truly significant stories
- **Dual-format Output**: Optimized for both email (HTML) and Discord (markdown)
- **Source Attribution**: Preserves original article URLs and titles
- **Character Limits**: Ensures Discord messages stay within platform limits
- **Error Handling**: Built-in n8n retry mechanisms

## Setup Instructions 🔧

### Prerequisites
- n8n instance (self-hosted or n8n.cloud)
- API keys for:
  - OpenRouter (for language model access)
  - Tavily (for search capabilities)
  - Gmail OAuth2 (for email delivery)
  - Discord Bot (for webhook access)

### Configuration Steps
1. Import the JSON workflow into your n8n instance
2. Configure credentials for:
   - OpenRouter API
   - Tavily API
   - Gmail OAuth2
   - Discord Bot API
3. Update the email recipient in the "Send a message" node
4. Verify RSS URLs are current (though they include chatgpt.com tracking parameters)
5. Activate the workflow

### Environment Variables
The workflow relies on n8n's credential system rather than direct environment variables. Set up these credential types:
- `openRouterApi`
- `tavilyApi`
- `gmailOAuth2`
- `discordBotApi`

## Customization 🎛️

### Adjusting Schedule
Modify the "Daily Schedule" node to change execution time or frequency.

### Adding/Removing Sources
1. Add additional "RSS Feed Read" nodes
2. Connect them to the "Combine All Articles" node
3. Update the merge node to include new inputs

### Changing AI Behavior
Edit the prompt in the "Categorize & Summarize" node to:
- Adjust story selection criteria
- Modify output formats
- Change prioritization weights
- Add/ignore specific topics

### Output Channels
- Replace Gmail with other email services (SendGrid, SMTP, etc.)
- Replace Discord with Slack, Teams, or other messaging platforms
- Add additional distribution methods (SMS, push notifications, etc.)

## Technologies Used 💻

- **Workflow Automation**: n8n
- **AI/LLM**: OpenRouter/Groq via LangChain integration
- **Search**: Tavily API
- **Communication**: Gmail API, Discord Webhook
- **Data Processing**: JavaScript (n8n Code node), JSON
- **RSS Parsing**: Built-in n8n RSS node

## Future Enhancements 🚀

- Add more diverse tech news sources (Ars Technica, Wired, etc.)
- Implement sentiment analysis for market-moving news
- Add language translation for international audiences
- Create weekly summary digests
- Enable user customization via web interface
- Add analytics dashboard for open/click rates
- Implement deduplication across days
- Add image extraction for richer Discord posts

## Sample Output 📄

### Email Format
```html
<h1>📰 TECH NEWS DIGEST</h1>
<h2> 1. [Article Title]</h2>
Summary:
• Point 1
• Point 2
• Point 3
• Point 4
• Point 5
Link:
[Original Article URL]
----------------------------------------------------------------------
<h2>2. [Article Title]</h2>
Summary:
• Point 1
• Point 2
• Point 3
• Point 4
• Point 5
Link:
[Original Article URL]
```

### Discord Format
```markdown
# **📰 Tech News Digest**

## **1. [Article Title]**

**Summary:**
• Point 1
• Point 2
• Point 3
• Point 4
• Point 5

**Link:**
[Original Article URL]

## **2. [Article Title]**

**Summary:**
• Point 1
• Point 2
• Point 3
• Point 4
• Point 5

**Link:**
[Original Article URL]
```

## Contributing 🤝

Feel free to fork this workflow and adapt it to your specific needs. Submit pull requests for:
- New source integrations
- Improved AI prompts
- Additional distribution channels
- Bug fixes and optimizations

## License

This workflow is provided as-is for educational and personal use. Customize and deploy according to your instance's terms of service.

--- 

Just add few emojis in it nothing else
<img width="1433" height="545" alt="image" src="https://github.com/user-attachments/assets/9ed39cd9-af8e-4f40-8ba1-2024cf6043d9" />

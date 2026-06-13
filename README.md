# Autonomous Tech News Research and Distribution Agent
<img width="1433" height="545" alt="Screenshot 2026-06-12 223459" src="https://github.com/user-attachments/assets/2c817c4d-944a-413e-bea5-d12f8a1e931f" />

## 📰 Overview
This n8n workflow automates the process of researching, curating, and distributing daily technology news digests. The agent runs on a schedule, fetches articles from multiple tech news sources, uses AI to analyze and select the most relevant stories, and delivers formatted reports via email and Discord.

## 🔧 How It Works
1. **Scheduler** (`Daily Schedule`): Triggers the workflow daily at 8:00 AM.
2. **News Sources** (RSS Feed Readers):
   - Hacker News: `https://news.ycombinator.com/rss?utm_source=chatgpt.com`
   - TechCrunch: `https://techcrunch.com/feed/?utm_source=chatgpt.com`
   - The Verge: `https://www.theverge.com/rss/index.xml`
3. **Article Processing Pipeline**:
   - **Combine All Articles**: Merges feeds from all three sources.
   - **Code in JavaScript**: Formats the first 15 articles into a standardized text format (Title and Link).
   - **Categorize & Summarize**: AI agent that:
     - Analyzes all articles using language models (OpenRouter as primary, Groq as backup).
     - Uses Tavily search for additional context when needed.
     - Filters for genuine technology news (ignoring blogs, opinions, tutorials, etc.).
     - Prioritizes AI news, major announcements, product launches, cybersecurity, funding, acquisitions, and open-source releases.
     - Selects 2 most important unique stories.
     - Generates two reports:
       - **Email Report**: HTML-formatted with detailed summaries (5 bullet points each).
       - **Discord Report**: Markdown-formatted under 1500 characters.
4. **Distribution Channels**:
   - **Email**: Sends formatted HTML report via Gmail.
   - **Discord**: Posts to configured channel via webhook.

## 🛡️ Security Note
- **No API keys or secrets are exposed** in this workflow JSON.
- The workflow uses n8n's credential system: only credential IDs and names are referenced (e.g., `"openRouterApi": { "id": "...", "name": "OpenRouter account" }`).
- Actual API keys are stored securely in your n8n instance's credential manager and are never included in workflow exports.

## 📥 Setup Instructions
1. **Import the workflow**:
   - Save the provided `Autonomous Tech News Research and Distribution Agent main.json` file.
   - In your n8n instance, go to **Workflows → Import** and select the JSON file.
2. **Configure credentials** (create these in n8n under **Credentials**):
   - **OpenRouter API** (name: `OpenRouter account`)
   - **Tavily API** (name: `Tavily account`)
   - **Gmail OAuth2** (name: `Gmail account`)
   - **Discord Bot API** (name: `Discord Bot account 2`)
     *(Note: The credential names must match exactly as referenced in the workflow.)*
3. **Update email recipient**:
   - Open the "Send a message" (Gmail) node.
   - In the "Send To" field, replace `YOUR_EMAIL@gmail.com` with your actual email address.
4. **Activate the workflow**:
   - Toggle the workflow to **Active** in the top-right corner.
   - It will now run daily at 8:00 AM.

## 📄 Sample Output
### Email Format (HTML)
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

### Discord Format (Markdown)
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

## 📁 Files in This Repository
- [`Autonomous Tech News Research and Distribution Agent main.json`](./Autonomous%20Tech%20News%20Research%20and%20Distribution%20Agent%20main.json) - The n8n workflow (with personal data hidden for safety).

## 🚀 Customization
- **Adjusting Schedule**: Modify the "Daily Schedule" node to change execution time or frequency.
- **Adding/Removing Sources**: Add additional "RSS Feed Read" nodes and connect them to the "Combine All Articles" node.
- **Changing AI Behavior**: Edit the prompt in the "Categorize & Summarize" node to adjust story selection criteria, output formats, or prioritization weights.
- **Output Channels**: Replace Gmail with other email services (SendGrid, SMTP, etc.) or Discord with Slack, Teams, or other messaging platforms.

## 💡 Technologies Used
- **Workflow Automation**: n8n
- **AI/LLM**: OpenRouter (primary) / Groq (alternative) via LangChain integration
- **Search**: Tavily API
- **Communication**: Gmail API, Discord Webhook
- **Data Processing**: JavaScript (n8n Code node), JSON
- **RSS Parsing**: Built-in n8n RSS node

## 🙋‍♂️ Contributing
Feel free to fork this workflow and adapt it to your specific needs. Submit pull requests for:
- New source integrations
- Improved AI prompts
- Additional distribution channels
- Bug fixes and optimizations

## 📜 License
This workflow is provided as-is for educational and personal use. Customize and deploy according to your instance's terms of service.

--- 

*Note: Replace `YOUR_EMAIL@gmail.com` in the Gmail node with your actual email before activating the workflow.*
</file>
</file>

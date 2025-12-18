# 🕵️ ArXiv Agent v1.0 - Your Intelligent Research Assistant

<div align="center">

![Version](https://img.shields.io/badge/version-1.0-blue.svg)
![Python](https://img.shields.io/badge/python-3.8+-green.svg)
![License](https://img.shields.io/badge/license-MIT-orange.svg)

**🤖 An AI-powered ArXiv paper crawler that automatically finds, analyzes, and emails you the latest research papers tailored to your interests.**

[Features](#-features) • [Quick Start](#-quick-start) • [Configuration](#-configuration) • [Examples](#-examples) • [Contributing](#-contributing)

</div>

---

## ✨ Features

### 🎯 **Personalized Paper Discovery**
- **Smart Search Expansion**: Automatically generates 3 additional search queries based on your research profile
- **Mixed Search**: Combines manual queries with AI-derived recommendations
- **Intelligent Deduplication**: Merges results intelligently, prioritizing manual searches

### 🧠 **AI-Powered Analysis**
- **Contextual Relevance Scoring**: LLM analyzes papers against your publication history
- **Bilingual Support**: Automatic Chinese/English translation of titles and abstracts
- **TL;DR Summaries**: One-sentence summaries for quick scanning
- **Topic Extraction**: Automatically categorizes papers by research area

### 🔍 **Deep Source Inspection**
- **Venue Detection**: Automatically detects conference/journal templates from LaTeX source code
- **GitHub Link Mining**: Finds hidden code repositories in paper sources
- **Source Tagging**: Distinguishes between abstract-found and source-mined links

### 📊 **Visual Analytics**
- **Global Trend Charts**: Visualizes paper distribution across research areas
- **Category Mapping**: Maps technical categories to readable names
- **Smart Briefing**: AI-generated summaries of today's research landscape

### 📧 **Beautiful Email Reports**
- **Rich HTML Formatting**: Professional, readable email templates
- **Source Badges**: Clear indicators for manual vs AI-recommended papers
- **Venue Badges**: Color-coded conference/journal identifiers
- **GitHub Integration**: Direct links to code repositories with star counts

---

## 🚀 Quick Start

### 1. Clone the Repository

```bash
git clone https://github.com/yourusername/arxiv-agent.git
cd arxiv-agent
```

### 2. Install Dependencies

```bash
pip install -r requirements.txt
```

### 3. Configure Environment

Copy the example environment file and fill in your details:

```bash
cp .env.example .env
nano .env  # or use your favorite editor
```

**Required Configuration:**
- `OPENAI_API_KEY`: Your OpenAI API key (or forwarded key)
- `SMTP_SERVER`, `SMTP_PORT`, `SENDER_EMAIL`, `SENDER_PASSWORD`: Email settings
- `ARXIV_QUERY`: Your search keywords
- `RECIPIENT_EMAIL`: Where to send reports

### 4. (Optional) Set Up User Profile

Create a personalized research profile:

```bash
cp user_profile.json.example user_profile.json
nano user_profile.json
```

Add your research interests and publications to enable:
- **AI-generated search expansion**
- **Contextual relevance analysis**
- **Personalized paper recommendations**

### 5. Run the Agent

```bash
python code/main.py
```

That's it! 🎉 The agent will:
1. Load your profile and generate search queries
2. Crawl ArXiv for relevant papers
3. Analyze papers with AI
4. Inspect LaTeX sources for venues and GitHub links
5. Generate visual trend charts
6. Send you a beautiful email report

---

## ⚙️ Configuration

### Environment Variables

| Variable | Description | Example |
|----------|-------------|---------|
| `OPENAI_API_KEY` | Your OpenAI API key | `sk-...` |
| `OPENAI_BASE_URL` | API base URL (for forwarded keys) | `https://api.example.com/v1` |
| `OPENAI_MODEL` | Model to use | `gpt-3.5-turbo` |
| `SMTP_SERVER` | SMTP server address | `smtp.gmail.com` |
| `SMTP_PORT` | SMTP port | `587` or `465` |
| `SENDER_EMAIL` | Your email address | `your@email.com` |
| `SENDER_PASSWORD` | Email password/app password | `your_password` |
| `ARXIV_QUERY` | Search keywords (comma-separated) | `machine learning, deep learning` |
| `RECIPIENT_EMAIL` | Report recipient | `recipient@example.com` |
| `USER_INTEREST` | Your research interests | `AI for Science, ML` |
| `BROAD_CATEGORY` | Broad category for trends | `cs`, `q-bio`, `stat` |
| `MAX_RESULTS` | Max papers per query | `10` |
| `ARXIV_DAYS` | Days to look back | `3` |

### User Profile Format

```json
{
    "name": "Your Name",
    "research_interests": [
        "Machine Learning",
        "Deep Learning"
    ],
    "publications": [
        {
            "title": "Your Paper Title",
            "abstract": "Your abstract here..."
        }
    ],
    "preferred_venues": [
        "ICLR",
        "NeurIPS",
        "ICML"
    ]
}
```

---

## 📖 Examples

### Basic Usage

Search for papers on a specific topic:

```bash
# Set in .env
ARXIV_QUERY=transformer architecture, attention mechanism
```

### Advanced: Personalized Search

With a user profile, the agent will:
- Generate related queries like `"transformer AND protein"` or `"attention mechanism AND vision"`
- Compare new papers against your publications
- Score papers based on relevance to your research

### Email Report Preview

The email includes:
- 📊 **Global Trend Chart**: Visual distribution of today's papers
- 🎯 **Source Tags**: Manual vs AI-recommended papers
- 🏛️ **Venue Badges**: Detected conference/journal templates
- 📦 **GitHub Links**: Code repositories with star counts
- 💡 **TL;DR**: One-sentence summaries
- 🤖 **AI Reasoning**: Why each paper is relevant

---

## 🏗️ Architecture

```
ArXiv Agent v1.0
├── UserProfileManager      # Loads and manages user research profile
├── ArXivPaperFetcher       # Crawls ArXiv with mixed search
├── PaperProcessor          # AI-powered analysis with contextual matching
├── SourceInspector         # Deep LaTeX source inspection
├── Visualizer             # Trend chart generation
└── EmailSender            # Beautiful HTML email reports
```

### Key Workflows

1. **Profile Loading** → Generates derived search queries
2. **Mixed Search** → Combines manual + AI queries, deduplicates
3. **Parallel Processing** → LLM analysis + source inspection
4. **Contextual Matching** → Compares papers against user publications
5. **Report Generation** → Charts + briefing + formatted email

---

## 🔧 Advanced Features

### Source Inspection

The agent downloads LaTeX source code and:
- Detects conference templates (CVPR, NeurIPS, ICLR, etc.)
- Mines GitHub links from source files
- Handles both tar.gz archives and plain text files

### Concurrency Control

- Uses `asyncio.Semaphore` to limit concurrent downloads (max 3)
- Retry mechanism (2 attempts) for failed downloads
- Extended timeout (60s) for large source files

### Email Providers

Tested with:
- ✅ Gmail (App Password required)
- ✅ QQ Mail
- ✅ 163 Mail
- ✅ CAS Email (中科院邮箱)

---

## 📝 Example Output

```
--- ArXiv Agent v1.0 Started (Personalized Profile Edition) ---
[*] ✅ 成功加载用户画像
[*] 🧠 [画像] 正在根据您的发表记录联想搜索词...
    -> 🧠 AI联想词: ['transformer AND protein', 'multimodal learning', 'MLLM applications']
[*] 🔍 [Manual] 搜索: machine learning ...
[*] 🔍 [AI Derived] 搜索: transformer AND protein ...
[*] 📈 [宏观] 正在扫描全站 cs 领域论文...
[*] 成功获取 15 篇论文（手动: 8, AI推荐: 7），准备进行AI分析...
[*] 开始分析 15 篇论文...
    🕵️ [Deep Scan] 正在请求: 2512.14693 (排队中...)
    ✅ [Venue] 通过文件名检测到模板: NeurIPS (文件: nips_style.sty)
    ✅ [GitHub] 在源码中发现: https://github.com/...
[*] 正在连接SMTP服务器...
[*] 邮件已发送至
--- Mission Complete ---
```

---

## 🤝 Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

### Areas for Contribution

- 🐛 Bug fixes
- ✨ New features
- 📚 Documentation improvements
- 🎨 UI/UX enhancements
- 🌍 Internationalization

---

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

⚖️ License & Acknowledgements
This project is open-sourced under the MIT License.

⚠️ Usage Note regarding ArXiv API
This tool allows you to interact with the ArXiv API and download papers. Please use this tool responsibly and ethically:

Respect Rate Limits: The code includes built-in concurrency limits (Semaphore) to be polite to ArXiv's servers. Do not modify these to perform aggressive scraping, or your IP may be banned by ArXiv.

ArXiv Terms of Use: Users must adhere to ArXiv's Terms of Use.

Data Licensing: The metadata retrieved is typically CC0. However, the PDFs and Source files downloaded are subject to the individual licenses selected by the authors (e.g., CC-BY, arXiv perpetual non-exclusive license). This tool does not grant you copyright over the downloaded content.

Disclaimer: This tool is for personal research and educational purposes. The author is not responsible for any misuse or IP bans resulting from the use of this software.

---

## 🙏 Acknowledgments

- Built with [OpenAI API](https://openai.com/api/)
- Uses [arxiv.py](https://github.com/lukasschwab/arxiv.py) for ArXiv access
- Inspired by the need for smarter research paper discovery

---

## ⭐ Star History

If you find this project useful, please consider giving it a star! ⭐

---

<div align="center">

**Made with ❤️ for researchers who want to stay ahead of the curve**

[Report Bug](https://github.com/yourusername/arxiv-agent/issues) • [Request Feature](https://github.com/yourusername/arxiv-agent/issues) • [Documentation](https://github.com/yourusername/arxiv-agent/wiki)

</div>


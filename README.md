<div align="center">
  <img src="https://drive.google.com/file/d/1w0Cx86oT_mABTB_BCb7K_Dem2XCsHYRn/view?usp=drive_link" alt="Email Analyzer Logo" width="120"/>
  <h1>📧 Email Analyzer</h1>
  <p><strong>AI-Powered Email Triaging & Security Analysis</strong></p>

  <!-- Badges -->
  <p>
    <img src="https://img.shields.io/badge/Java-17-ED8B00?style=for-the-badge&logo=java&logoColor=white" alt="Java 17"/>
    <img src="https://img.shields.io/badge/Spring_Boot-3.3-6DB33F?style=for-the-badge&logo=springboot&logoColor=white" alt="Spring Boot 3.3"/>
    <img src="https://img.shields.io/badge/Ollama-Local-8A2BE2?style=for-the-badge&logo=ollama&logoColor=white" alt="Ollama"/>
    <img src="https://img.shields.io/badge/Chrome_Extension-MV3-4285F4?style=for-the-badge&logo=googlechrome&logoColor=white" alt="Chrome Extension MV3"/>
    <img src="https://img.shields.io/badge/license-MIT-green?style=for-the-badge" alt="License MIT"/>
  </p>

  <p>
    <img src="https://img.shields.io/badge/status-working-success?style=flat-square"/>
    <img src="https://img.shields.io/badge/PRs-welcome-brightgreen?style=flat-square"/>
  </p>
</div>

---

## ✨ Features

| Feature | Description |
|---------|-------------|
| 🏷️ **Smart Categorization** | Auto-classifies emails into Spam, Finance, Educational, Work, or Personal |
| ⚡ **Priority Detection** | Identifies urgency — Low, Medium, or High based on deadlines & action items |
| 🔒 **Security Scanning** | Detects phishing, malware links, fake login pages, and suspicious senders |
| 📝 **Concise Summaries** | Generates 2-sentence summaries so you never read the full email again |
| ✅ **Action Items** | Extracts concrete tasks you need to perform |
| 🚀 **100% Local & Free** | Runs on your machine with Ollama — no API keys, no monthly bills, no data leaving your PC |
| 🔌 **One-Click Extension** | Works seamlessly with Gmail and Outlook via a Chrome extension |

---

## 🏗️ System Architecture

```
┌─────────────────────────────────────────────────────────┐
│                    🖥️ YOUR BROWSER                      │
│  ┌──────────────────────────────────────────────────┐   │
│  │              Chrome Extension                     │   │
│  │  ┌──────────┐  ┌──────────┐  ┌────────────────┐  │   │
│  │  │ popup.js │  │popup.html│  │  content.js    │  │   │
│  │  │ (UI +    │◄─┤ (UI      │  │ (DOM Reader)   │  │   │
│  │  │  API call)│  │  Render) │  │                │  │   │
│  │  └────┬─────┘  └──────────┘  └───────┬────────┘  │   │
│  │       │                              │            │   │
│  │       │     Reads Gmail/Outlook DOM  │            │   │
│  │       └──────────────────────────────┘            │   │
│  └───────────────────┬───────────────────────────────┘   │
└──────────────────────┼───────────────────────────────────┘
                       │ HTTP POST /api/analyze
                       ▼
┌──────────────────────────────────────────────────────────┐
│                   ☕ JAVA BACKEND                        │
│                                                          │
│  ┌──────────────┐   ┌──────────────────┐                │
│  │  Controller   │──►│  Service Layer   │                │
│  │  /api/analyze │   │  (OllamaService) │                │
│  │  /api/health  │◄──│                  │                │
│  └──────────────┘   └────────┬─────────┘                │
│                              │                           │
│                     Cleans & sanitizes                   │
│                     email text, strips                   │
│                     images/HTML                         │
│                              │                           │
│                              ▼                           │
│  ┌──────────────────────────────────────────────────┐   │
│  │         POST /api/chat (Ollama API)              │   │
│  └──────────────────────┬───────────────────────────┘   │
└─────────────────────────┼───────────────────────────────┘
                          │
                          ▼
┌──────────────────────────────────────────────────────────┐
│                    🦙 OLLAMA (LOCAL)                     │
│                                                          │
│  ┌──────────────────────────────────────────────────┐   │
│  │  llama3.2:3b — Pure text model                   │   │
│  │  • Runs entirely on your machine                  │   │
│  │  • No internet required after download           │   │
│  │  • Your emails never leave your PC               │   │
│  └──────────────────────────────────────────────────┘   │
└──────────────────────────────────────────────────────────┘
```

---

## 🛠️ Tech Stack

| Component | Technology |
|-----------|-----------|
| **Backend** | Java 17, Spring Boot 3.3, Maven |
| **AI Model** | Ollama + Llama 3.2 (3B) — 100% local |
| **Extension** | Manifest V3, Vanilla JavaScript, HTML/CSS |
| **API Communication** | REST (JSON) over HTTP |
| **Build Tool** | Apache Maven 3.9+ |

---

## 📂 Project Structure

```
email-analyzer/
├── backend/                          # Java Spring Boot API
│   ├── pom.xml                       # Maven dependencies
│   └── src/main/java/com/emailtriager/
│       ├── EmailTriagerApplication.java   # Entry point
│       ├── config/
│       │   └── CorsConfig.java           # CORS for extension
│       ├── controller/
│       │   └── EmailController.java       # REST endpoints
│       ├── dto/
│       │   ├── EmailRequest.java          # Request body
│       │   └── EmailResponse.java         # Response body
│       └── service/
│           └── OllamaEmailAnalysisService.java  # AI logic
│
├── extension/                        # Chrome Extension
│   ├── manifest.json                 # Extension config (MV3)
│   ├── content.js                    # Reads email DOM
│   ├── popup.html                    # Extension UI
│   ├── popup.js                      # UI logic & API calls
│   ├── icon16.png                    # Extension icons
│   ├── icon48.png
│   └── icon128.png
│
└── README.md                         # You are here
```

---

## ⚙️ Installation

### Prerequisites

- ☕ **Java 17+** — [Download](https://adoptium.net/)
- 🐘 **Apache Maven 3.9+** — [Download](https://maven.apache.org/download.cgi)
- 🦙 **Ollama** — [Download](https://ollama.com)
- 🌐 **Chrome Browser**

### Step 1: Set Up Ollama

```bash
# Install Ollama (download from ollama.com)
# Then pull the model:
ollama pull llama3.2:3b

# Verify it's running:
ollama list
```

> ⚠️ Make sure Ollama stays running in your system tray/background.

### Step 2: Start the Backend

```bash
cd backend
mvn spring-boot:run
```

The server starts on **http://localhost:8000**

### Step 3: Load the Extension

1. Open Chrome → `chrome://extensions`
2. Toggle **Developer mode** (top right)
3. Click **Load unpacked**
4. Select the `extension/` folder

---

## 🚀 Usage

### Quick Test

```bash
curl http://localhost:8000/api/health
# → should return 200 OK

curl -X POST http://localhost:8000/api/analyze \
  -H "Content-Type: application/json" \
  -d '{
    "subject": "Urgent: Invoice Overdue",
    "sender": "billing@company.com",
    "body": "Your invoice of $499 is overdue. Pay immediately to avoid service disruption. Click here: http://bit.ly/pay-now"
  }'
```

### Using the Extension

| Step | Action |
|------|--------|
| 1 | Open **Gmail** or **Outlook** in Chrome |
| 2 | Click on any email to read it |
| 3 | Click the 📧 **Email Analyzer** extension icon |
| 4 | The popup auto-analyzes and shows results instantly |

### Understanding Results

```
┌─────────────────────────────────┐
│  📧 Email Analyzer              │
│                                 │
│  Category    [ Work ✔️ ]        │
│  Priority    [ High 🔴 ]        │
│  Security    [ Safe 🟢 ]        │
│                                 │
│  Summary: Invoice overdue from  │
│  billing@company.com. Payment   │
│  required to avoid disruption.  │
│                                 │
│  Action Items:                  │
│  → Pay invoice #INV-4421        │
│  → Contact support if paid      │
└─────────────────────────────────┘
```

### API Endpoints

| Method | Endpoint | Description |
|--------|----------|-------------|
| `GET` | `/api/health` | Health check |
| `POST` | `/api/analyze` | Analyze an email |

**Request body:**
```json
{
  "subject": "string",
  "sender": "string",
  "body": "string (required)"
}
```

**Response:**
```json
{
  "category": "Work",
  "priority": "High",
  "summary": "2-sentence summary of the email.",
  "actionItems": ["Task 1", "Task 2"],
  "securityRisk": "Safe",
  "securityDetails": ""
}
```

---

## 🧪 Sample Outputs

### 📨 Finance Email
```json
{
  "category": "Finance",
  "priority": "High",
  "summary": "Bank statement for June 2026 shows a total balance of $12,450. Unusual login from new device detected.",
  "actionItems": ["Review recent transactions", "Verify login activity"],
  "securityRisk": "Suspicious",
  "securityDetails": "Login from unrecognized device in another city"
}
```

### 🎣 Phishing Email
```json
{
  "category": "Spam",
  "priority": "High",
  "summary": "Fake PayPal security alert requesting account verification via external link.",
  "actionItems": ["Do not click any links", "Report as phishing"],
  "securityRisk": "Dangerous",
  "securityDetails": "Spoofed sender address, fake login page link detected"
}
```

---

## 🔧 Troubleshooting

| Problem | Solution |
|---------|----------|
| ❌ "Backend not reachable" | Start the backend: `mvn spring-boot:run` |
| ❌ "No email found" | Click on an email in your inbox first |
| ❌ Extension not responding | Reload the Gmail tab (F5) |
| ❌ Ollama not responding | Check Ollama is running in system tray |
| ❌ "Model not found" | Run `ollama pull llama3.2:3b` |

---

## 📈 Roadmap

- [x] Smart email categorization
- [x] Priority detection
- [x] Security/phishing analysis
- [x] Chrome extension (Gmail & Outlook)
- [ ] Outlook desktop support
- [ ] Multi-language email support
- [ ] Batch email analysis
- [ ] Email analytics dashboard

---

## 🤝 Contributing

Contributions are welcome! Open an issue or submit a PR.

1. Fork the project
2. Create your feature branch (`git checkout -b feature/amazing`)
3. Commit changes (`git commit -m 'Add feature'`)
4. Push (`git push origin feature/amazing`)
5. Open a Pull Request

---

## 📄 License

This project is licensed under the **MIT License**.

---

<div align="center">
  <p>Made with ❤️ using Java, Spring Boot & Ollama</p>
  <p>
    <img src="https://drive.google.com/file/d/1w0Cx86oT_mABTB_BCb7K_Dem2XCsHYRn/view?usp=drive_link" alt="Logo" width="48"/>
  </p>
</div>

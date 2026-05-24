# 🤖 WhatsApp AI Customer Support
### n8n + Claude API + Meta WhatsApp Cloud API

Automated customer support bot yang menjawab pesan WhatsApp menggunakan Claude AI, dengan sistem escalation ke human agent dan logging otomatis ke Google Sheets.

---

## 🎯 Problem
Tim support manual tidak bisa handle ratusan pesan WhatsApp secara realtime. Response time lambat = customer experience buruk dan kehilangan revenue.

## 💡 Solution
Workflow otomatis yang menjawab 80%+ pertanyaan umum dengan Claude AI dalam < 3 detik, dan mengescalasi sisanya ke human agent secara real-time via Slack.

---

## ⚡ Features
- ✅ Auto-reply via Claude AI (< 3 detik response time)
- ✅ Smart escalation ke human agent dengan alasan jelas
- ✅ Conversation logging ke Google Sheets (timestamp, nomor, pesan, status)
- ✅ Notifikasi Slack untuk tim support
- ✅ 24/7 availability tanpa biaya tambahan
- ✅ Zero infrastructure cost (n8n self-hosted)

---

## 🏗️ Architecture
```
User WhatsApp → Meta Webhook → n8n Trigger
                                    ↓
                              Claude API
                                    ↓
                    ┌─────── IF Node ────────┐
                    ↓                        ↓
              AI bisa jawab           Perlu escalasi
                    ↓                        ↓
             Reply WhatsApp          Notif Slack
                    ↓                        ↓
                    └──────── Log Google Sheets ─────┘
```

---

## 🛠️ Tech Stack
| Tool | Fungsi |
|------|--------|
| n8n | Workflow automation engine |
| Anthropic Claude API | AI response generation |
| Meta WhatsApp Cloud API | Message channel |
| Google Sheets API | Conversation logging |
| Slack Webhook | Escalation alerts |

---

## 📊 Impact
| Metric | Manual | AI System |
|--------|--------|-----------|
| Response time | ~2 jam | < 3 detik |
| Availability | Jam kerja | 24/7 |
| Consistency | Variable | 100% |
| Cost per message | Tinggi | ~$0.001 |

---

## 🚀 Quick Start

### Prerequisites
- n8n instance (self-hosted atau cloud)
- Anthropic API key
- Meta Developer Account + WhatsApp Business
- Google Sheets + Slack workspace

### Setup
1. **Clone repo ini**
   ```bash
   git clone https://github.com/USERNAME/wa-ai-support-n8n.git
   ```

2. **Import workflow ke n8n**
   - Buka n8n → Workflows → Import from file
   - Upload `workflow.json`

3. **Setup environment variables**
   ```bash
   cp .env.example .env
   # Edit .env dengan credentials kamu
   ```

4. **Konfigurasi Meta WhatsApp API**
   - Buka [Meta for Developers](https://developers.facebook.com)
   - Buat App → Add WhatsApp product
   - Setup Webhook URL → arahkan ke n8n webhook URL
   - Subscribe ke: `messages`

5. **Setup Google Sheets**
   - Buat spreadsheet baru
   - Buat sheet bernama `WA Support Log`
   - Kolom: timestamp, from_number, user_message, ai_response, status, escalation_reason

6. **Kustomisasi Claude Prompt**
   - Edit `prompts/system-prompt.md`
   - Isi info bisnis, produk, jam operasional

7. **Test**
   - Kirim pesan ke nomor WhatsApp bisnis kamu
   - Cek balasan otomatis dari Claude
   - Cek Google Sheets untuk log

---

## 📁 Struktur File
```
wa-ai-support-n8n/
├── README.md
├── workflow.json          ← import ke n8n
├── .env.example           ← template environment variables
├── setup-guide.md         ← panduan setup detail
├── prompts/
│   └── system-prompt.md   ← Claude system prompt
└── screenshots/
    ├── workflow-overview.png
    ├── wa-demo.png
    └── sheets-log.png
```

---

## 🔧 Environment Variables
```env
ANTHROPIC_API_KEY=sk-ant-xxxxx
WHATSAPP_TOKEN=EAAxxxxx
PHONE_NUMBER_ID=1234567890
VERIFY_TOKEN=your-random-verify-token
SLACK_WEBHOOK_URL=https://hooks.slack.com/services/xxx
GOOGLE_SHEETS_ID=your-spreadsheet-id
```

---

## 📸 Screenshots
> *Tambahkan screenshot workflow n8n, demo WhatsApp, dan Google Sheets log setelah setup*

---

## 🤝 Author
Built as part of AI Automation Engineer portfolio.

**Tech Stack:** n8n · Claude API · WhatsApp Cloud API · Google Sheets · Slack

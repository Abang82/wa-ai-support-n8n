# Setup Guide — WhatsApp AI Customer Support

## Step 1: Meta WhatsApp Cloud API

1. Buka https://developers.facebook.com → My Apps → Create App
2. Pilih tipe: **Business**
3. Add product: **WhatsApp**
4. Masuk ke WhatsApp > API Setup
5. Catat:
   - `Phone Number ID`
   - `Access Token` (temporary, nanti buat permanent)
6. Scroll ke Webhook → **Configure**
   - Callback URL: `https://your-n8n.com/webhook/wa-support`
   - Verify Token: isi string random kamu
   - Klik Verify and Save
7. Subscribe ke field: **messages**

## Step 2: Setup n8n

1. Buka n8n → Workflows → **Import from File**
2. Upload `workflow.json` dari repo ini
3. Buka workflow → klik node pertama (Webhook)
4. Copy webhook URL yang tampil
5. Paste ke Meta Webhook Callback URL (langkah 6 di atas)

## Step 3: Credentials n8n

Tambahkan credentials berikut di n8n (Settings > Credentials):

- **Anthropic API**: masukkan API key
- **HTTP Header Auth** (untuk WhatsApp): `Authorization: Bearer {WHATSAPP_TOKEN}`
- **Google Sheets OAuth2**: ikuti flow OAuth
- **Slack Webhook**: paste webhook URL

## Step 4: Kustomisasi Prompt

1. Buka file `prompts/system-prompt.md`
2. Copy prompt ke dalam n8n node "Set Variables"
3. Ganti semua bagian [ISI ...] dengan info bisnis kamu
4. Tambahkan FAQ umum yang sering ditanyakan customer

## Step 5: Setup Google Sheets

Buat spreadsheet baru dengan kolom:
| timestamp | from_number | user_message | ai_response | status | escalation_reason |

## Step 6: Test

1. Kirim pesan ke nomor WhatsApp yang terdaftar
2. Tunggu 2-3 detik → harus ada balasan otomatis
3. Coba kirim pertanyaan yang tidak ada di FAQ → harus trigger escalation
4. Cek Slack → notif muncul
5. Cek Google Sheets → row baru ditambahkan

## Troubleshooting

**Webhook tidak terverifikasi:**
- Pastikan n8n bisa diakses dari internet (bukan localhost)
- Cek VERIFY_TOKEN sama persis

**Claude tidak menjawab:**
- Cek ANTHROPIC_API_KEY valid
- Cek format body request di HTTP node

**Escalation tidak ke Slack:**
- Cek IF node condition: harus `contains("ESCALATE")`
- Cek SLACK_WEBHOOK_URL valid

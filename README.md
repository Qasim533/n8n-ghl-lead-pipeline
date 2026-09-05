# 🤖 GHL Lead Pipeline — AI Scoring + Google Sheets (n8n)

Jab bhi koi lead GHL funnel form submit kare, yeh workflow automatically lead score karta hai, Hot ya Cold route karta hai, AI se personalized message generate karta hai, aur Google Sheets mein save karta hai.

## Flow

```
GHL Webhook → Lead Scoring → Hot or Cold?
  → Hot: AI Message Hot Lead → Extract AI Message
  → Cold: AI Message Cold Lead → Extract AI Message
→ Save to Google Sheets → Respond to GHL
```

## Lead Scoring Logic

| Budget | Points |
|---|---|
| $5k+ | +40 |
| $2k–$5k | +30 |
| $500–$2k | +20 |
| Under $500 | +5 |

| Business Size | Points |
|---|---|
| Enterprise | +40 |
| Medium | +30 |
| Small | +20 |
| Solo | +10 |

| Tier | Score |
|---|---|
| 🔥 Hot | 60+ pts |
| 🟡 Warm | 30–59 pts |
| 🧊 Cold | 0–29 pts |

## Setup

1. Replace `YOUR_OPENROUTER_API_KEY_HERE` in both AI nodes
2. Replace `YOUR_GOOGLE_SHEET_ID_HERE` in Google Sheets node
3. Create a `Leads` tab in your Google Sheet with these columns:
   `first_name | last_name | email | phone | business_type | business_size | budget | current_tools | main_problem | lead_score | lead_type | ai_message | timestamp`
4. Set up Google Sheets OAuth2 credential in n8n
5. Copy webhook URL from `GHL Webhook` node
6. In GHL: Automations → Webhook → paste URL
7. Activate workflow

## GHL Payload Expected

```json
{
  "first_name": "John",
  "last_name": "Doe",
  "email": "john@example.com",
  "phone": "+1234567890",
  "budget": "$5k+",
  "business_size": "Medium",
  "business_type": "E-commerce",
  "current_tools": "Zapier, HubSpot",
  "main_problem": "Lead follow-up too slow"
}
```

## Built With

- [n8n](https://n8n.io)
- [GoHighLevel](https://gohighlevel.com)
- [OpenRouter](https://openrouter.ai) + Llama 3.1 8B
- [Google Sheets](https://sheets.google.com)

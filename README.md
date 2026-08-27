# shopify-ai-abandoned-cart-agent
Automated event-driven n8n workflow powered by Groq AI and Shopify/WhatsApp APIs to recover abandoned checkouts with personalized dynamic discount codes.

# 🛒 Shopify AI Abandoned Cart Recovery Agent

An enterprise-grade, event-driven AI automation workflow built with **n8n**, **Groq Chat Models (Llama-3)**, and **Shopify / WhatsApp Business APIs**. This system dynamically captures abandoned checkout events, verifies customer contact details, waits for purchase completion, generates personalized dynamic discount codes via Shopify Admin API, and dispatches context-aware WhatsApp engagement messages in real time.

---

## 🎯 Key Capabilities

- **Real-Time Webhook Catching:** Triggers instantly upon Shopify checkout creation (`checkout/created`).
- **Smart Delay & Payment Verification:** Implements a 15-minute wait buffer to check order payment status before initiating recovery.
- **Dynamic Offer Generation:** Communicates directly with Shopify Admin REST API to create unique 10% discount codes dynamically per user.
- **Groq AI Copy Generation:** Leverages Llama-3 via Groq to draft human-like, non-spammy personalized recovery copy.
- **Multi-Channel Delivery:** Dispatches messages through WhatsApp Cloud API (Graph API) and tags order status for analytics.

---

## 📐 Workflow Architecture
![System Architecture](./Shopify%20AI%20Abandoned%20Cart%20Arbitrage%20Agent.jpg)

[Shopify Webhook: Checkout Created]
│
▼
[Extract Checkout Data]
│
[Has Contact Info?] ── (False) ──► [Stop - No Contact Info]
│ (True)
▼
[Wait 15 Minutes]
│
[Check If Already Paid]
│
[Already Paid?] ────── (True) ──► [Stop - Already Paid]
│ (False)
▼
[Create Dynamic Shopify Price Rule (10% Off)]
│
[Generate Unique Discount Code]
│
[Groq AI - Personalize Recovery Message]
│
[Prepare & Send WhatsApp Message]
│
[Tag Order: AI_Contacted] ──► [Success Log]

---

## 🛠️ Tech Stack & Integrations

- **Orchestration:** n8n Workflow Automation
- **AI / LLM:** Groq API (Llama-3 Models)
- **E-Commerce Platform:** Shopify Admin API (Webhooks, Price Rules, Discounts)
- **Messaging Service:** Meta WhatsApp Business Cloud API
- **Language:** JavaScript / JSON (n8n Node expressions)

---

## 🚀 How to Import & Run

1. Clone this repository or download the `Shopify_AI_Abandoned_Cart_Agent.json` workflow file.
2. Open your n8n instance dashboard.
3. Click **Workflows** ➔ **Import from File** and select the `.json` file.
4. Configure your environment credentials in n8n:
   - **Shopify Access Token** (Admin API)
   - **Groq API Key**
   - **WhatsApp Cloud API Token & Phone ID**
5. Activate the workflow trigger URL and hook it to your Shopify Webhooks configuration.

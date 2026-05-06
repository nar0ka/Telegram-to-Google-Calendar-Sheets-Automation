# Instructions: Telegram to Google Calendar & Sheets Automation

Welcome! This guide will help you set up and launch your Telegram-to-Google-Workspace automation using n8n. 

---

### ⚙️ Prerequisites

Before you begin, make sure you have:
1. **n8n** (either a self-hosted instance or n8n Cloud account).
2. **A Google Account** (with access to Google Sheets and Google Calendar).
3. **A Telegram Account**.

---

### 🚀 Step-by-Step Setup

#### Step 1: Create Your Telegram Bot
1. Open Telegram and search for the official **[@BotFather](https://t.me/BotFather)**.
2. Send the command `/newbot` and follow the instructions to name your bot.
3. Copy the **HTTP API Token** provided by BotFather (you will need it for the n8n node).

#### Step 2: Prepare Your Google Sheets Document
1. Create a new Google Sheet.
2. In the first row, create the following headers:
   * **Column A:** `Date`
   * **Column B:** `Chat ID`
   * **Column C:** `Message`
3. Copy the spreadsheet ID from your browser’s URL bar (the long string of letters and numbers between `/d/` and `/edit`).

#### Step 3: Import the Workflow
1. Open your n8n instance and create a new workflow.
2. Build the workflow using the 4 nodes or import the provided `workflow.json` file.

#### Step 4: Configure Nodes in n8n

* **Telegram Trigger Node:**
  * Click to add credentials and paste the Telegram Bot token you copied in Step 1.
  * Set **Updates** to `message`.

* **Google Calendar Node:**
  * Connect your Google account.
  * Set Calendar ID to `primary`.
  * Set the action to create an event and map the input data.

* **Google Sheets Node:**
  * Connect your Google account.
  * Paste your Document ID from Step 2.
  * Map the columns as follows:
    * Column 1 (Date): `{{ new Date().toLocaleString() }}`
    * Column 2 (Chat ID): `{{ $json.message.chat.id }}`
    * Column 3 (Message): `{{ $json.message.text }}`

* **Telegram Bot Node:**
  * Select the same Telegram credentials.
  * Set the **Chat ID** to `{{ $json.message.chat.id }}`.
  * Define the success message in the text field (e.g., `✅ Event added to Calendar & logged!`).

---

### 🏁 Finalizing

1. Click the **Activate** button (Publish) to turn the workflow live.
2. Open your Telegram bot and send a message or note to test the integration!

---

### 🔗 Links & Contacts
* **GitHub**: [github.com/nar0ka](https://github.com/nar0ka)
* **Gumroad Store**: [naroka.gumroad.com](https://naroka.gumroad.com)

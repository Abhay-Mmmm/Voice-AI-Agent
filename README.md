# AI-Agent


## Overview

**AI-Agent** is a modular AI-powered automation suite built with n8n, designed to handle calendar scheduling, email management, research, and conversational tasks. Each agent is specialized for a domain and can be orchestrated together for advanced workflows.

> **Note:** This project has not been deployed.

---

## Agents

### 1. Calendar Agent
**Purpose:** Expert scheduling and event creation for Google Calendar (abhaykrishna280@gmail.com), with strict timezone and validation rules.

- **Timezone:** Always Asia/Kolkata (UTC+05:30)
- **Default date:** Today or tomorrow (never random)
- **Default duration:** 1 hour
- **Time parsing:** Handles natural language ("10", "10 AM", "tomorrow 3pm", etc.)
- **Validation:** Ensures valid, non-overlapping events
- **Title/Description:** Auto-generates if missing
- **Attendees:** Adds if mentioned
- **Output:** Always returns a single JSON payload for event creation
- **Tools:**
	- Get current date/time
	- Create event (with/without attendees)
	- Fetch events

**Example:**
> "Meet Jack at 10 AM" → schedules for today/tomorrow at 10:00 AM IST

---

### 2. Email Agent
**Purpose:** Ensures all emails sent by "Abhay Krishna" from my email, end with the exact sign-off:

		Best regards,
		Abhay Krishna

- **Sender:** Always me.
- **Sign-off:** Enforced, never paraphrased or duplicated
- **Formatting:** Preserves quoted text, signatures, and uses HTML for Gmail
- **Tools:**
	- Fetch messages
	- Send email (with subject/body prediction)
- **Flow:**
	1. Fetch draft/message
	2. Confirm author
	3. Append sign-off if missing
	4. Send email

---

### 3. JerryBot
**Purpose:** Telegram chatbot that routes user queries to the correct agent (Calendar, Email, Research, or Contact DB).

- **Platform:** Telegram
- **Capabilities:**
	- Understands user intent
	- Uses Contact DB (Google Sheets) for contact details
	- Delegates to Email Agent, Calendar Agent, or Research Agent as needed
- **Memory:** Maintains session context per user

---

### 4. Research Agent
**Purpose:** Answers user questions using Wikipedia, Hacker News, and Serp API.

- **Flow:**
	1. Search Wikipedia
	2. If not found, search Hacker News
	3. If still not found, use Serp API
- **Tools:** Wikipedia, Hacker News, Serp API

---

## How It Works

1. **User interacts** (via Telegram, web, or other interface)
2. **JerryBot** receives the message and determines intent
3. **Delegation:**
	 - Calendar queries → Calendar Agent
	 - Email tasks → Email Agent
	 - Research questions → Research Agent
	 - Contact lookups → Contact DB
4. **Agents** process the request and return results

---

## Requirements

- n8n (self-hosted or cloud)
- Google Calendar, Gmail, Google Sheets, Telegram, and API credentials for integrations

---

## Credits

Created by Abhay Krishna with ❤️

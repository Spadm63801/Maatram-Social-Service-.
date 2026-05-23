# 🌟 MAATRAM v2.0 – Social Impact & Emergency Help Platform

> **மாற்றம்** (Maatram) = "Change" in Tamil

---

## 🚀 Quick Start

```bash
# 1. Install
npm install

# 2. Configure environment
cp .env.example .env.local
# Fill in your keys (see below)

# 3. Run everything
npm run dev:all
# Frontend → http://localhost:3000
# Backend  → http://localhost:5000
# WebSocket→ ws://localhost:5000/ws/location
```

---

## 🔑 Environment Variables

| Variable | Required | Description |
|---|---|---|
| `TWILIO_ACCOUNT_SID` | For real SMS | From https://twilio.com (free trial) |
| `TWILIO_AUTH_TOKEN` | For real SMS | Twilio auth token |
| `TWILIO_PHONE_NUMBER` | For real SMS | Your Twilio number e.g. `+1XXXXXXXXXX` |
| `TWILIO_WHATSAPP_NUMBER` | For WhatsApp | `whatsapp:+14155238886` (sandbox) |
| `ENABLE_WHATSAPP` | Optional | `true` to enable WhatsApp via Twilio |
| `FAST2SMS_API_KEY` | Alt to Twilio | India-only SMS, cheaper. https://fast2sms.com |
| `USE_FAST2SMS` | Optional | `true` to use Fast2SMS instead of Twilio |
| `JWT_SECRET` | Yes | Any random secret string |
| `PORT` | No | Default 5000 |

> **Dev Mode:** When no SMS provider is configured, OTPs print in your terminal and appear on screen.

---

## 📱 Features

### 🔐 OTP Authentication (Real SMS)
- **Twilio** or **Fast2SMS** (India) for real SMS delivery
- 6-digit OTP with auto-advance input boxes
- 10-minute expiry, 5 attempts max, 60-second resend cooldown
- Dev mode: OTP shown on screen + printed in server console

### 🆘 SOS Emergency
- 5-second countdown before trigger (prevents accidents)
- Real GPS location captured at trigger time
- **SMS sent** to all guardians via Twilio/Fast2SMS
- **WhatsApp message sent** with live tracking link
- Per-guardian WhatsApp re-send buttons in UI
- Resolve with "I'm Safe" button

### 👥 Guardian Management
- Add up to 5 trusted guardians
- Guardian gets **real verification OTP via SMS**
- WhatsApp quick-open button per guardian
- Primary guardian badge
- Remove anytime

### 📍 Live Location Sharing
- Real GPS via Browser Geolocation API
- **WebSocket (ws://)** for real-time push updates to viewers
- HTTP polling fallback every 15 seconds
- SMS + **WhatsApp message** with tracking link sent to contacts
- Per-contact WhatsApp re-send buttons
- OpenStreetMap embedded iframe (free, no API key)
- Google Maps direct link for opening in maps app
- Shareable link works in any browser — no app needed
- Auto-updates every 30 seconds while active
- Choose duration: 30 min / 1 hr / 2 hr / 8 hr

### 🗺️ Live Map Tracker (`/track/live/:sessionId`)
- Public page — guardians can open without logging in
- OpenStreetMap embedded (dark-tinted)
- WebSocket live connection indicator
- Coordinate display with accuracy
- Google Maps + OpenStreetMap deep links
- Session expiry info
- Responsive, mobile-first

### 🪪 KYC Verification (4-step)
1. **Personal Info** — name, DOB, gender, address (with validation)
2. **Document Upload** — Aadhaar / PAN / Voter ID / Passport / DL
   - Document number format validation
   - Front + back image upload with drag-and-drop
   - Image compression before upload
3. **Selfie Capture** — live camera with face oval guide, or upload
4. **Review & Submit** — summary, face match score, consent

- Auto-approval in dev (8 seconds after submit)
- KYC status badge on Profile page
- Yellow dot on BottomNav when KYC pending
- Re-apply flow for rejected KYC

### 💝 Donations
- 6 seeded campaigns with real images
- Category filters + search
- Quick-select amounts + custom amount
- Anonymous donation toggle
- Transaction ID on success

### 🐷 Child Savings
- Goals: Education / Marriage / Startup / Travel / Home
- Monthly savings calculator
- Milestones at 25%, 50%, 75%, 100%
- Contribution history with notes

---

## 🏗️ Architecture

```
maatram/
├── src/
│   ├── pages/
│   │   ├── LoginPage.tsx     # OTP auth (real SMS)
│   │   ├── HomePage.tsx      # Dashboard
│   │   ├── SafetyPage.tsx    # SOS + Guardians + Location + WhatsApp
│   │   ├── DonatePage.tsx    # Campaigns
│   │   ├── SavingsPage.tsx   # Child savings
│   │   ├── KYCPage.tsx       # 4-step KYC
│   │   ├── ProfilePage.tsx   # Profile + KYC status
│   │   └── TrackPage.tsx     # Public live map tracker
│   ├── components/
│   │   ├── BottomNav.tsx     # With SOS + KYC badges
│   │   └── ui/               # Button, Card, Input, Modal, etc.
│   ├── hooks/
│   │   ├── useGeolocation.ts # GPS hook
│   │   └── useLocationSocket.ts # WebSocket live location
│   ├── context/
│   │   └── AppContext.tsx    # Global state + toast
│   ├── server/
│   │   └── index.ts          # Express + WebSocket server
│   └── utils/
│       └── api.ts            # All API calls
```

---

## 💬 WhatsApp Setup

### Option A: Twilio WhatsApp Sandbox (Free testing)
1. Go to https://console.twilio.com/us1/develop/sms/try-it-out/whatsapp-learn
2. Join sandbox: WhatsApp `+1 415 523 8886`, send `join <your-code>`
3. Set `TWILIO_WHATSAPP_NUMBER=whatsapp:+14155238886`
4. Set `ENABLE_WHATSAPP=true`

### Option B: No config (web links)
When WhatsApp API isn't configured, the app generates `wa.me/` links that open WhatsApp directly on click — still works perfectly.

---

## 📱 SMS Setup

### Twilio (International, recommended)
```
TWILIO_ACCOUNT_SID=ACxxxxxxxxxx
TWILIO_AUTH_TOKEN=xxxxxxxxxx
TWILIO_PHONE_NUMBER=+1XXXXXXXXXX
```

### Fast2SMS (India-only, cheaper: ₹100 = ~1000 SMS)
```
FAST2SMS_API_KEY=your_key_here
USE_FAST2SMS=true
```
Get key: https://fast2sms.com

---

*மாற்றம் தேவை. மாற்றம் நாமே.* — "Change is needed. We are the change."

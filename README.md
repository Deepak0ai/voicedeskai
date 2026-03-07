# VoiceDesk AI 🎙️

A **voice-powered support ticket system**. A voice AI agent collects customer issues and automatically creates support tickets displayed on a real-time dashboard.

---

## 📁 Folder Structure

```
voicedesk-ai/
├── backend/
│   ├── server.js               # Express server entry point
│   ├── routes/
│   │   ├── tickets.js          # POST /webhook, GET /tickets, PATCH /tickets/:id
│   │   └── analytics.js        # GET /analytics
│   └── data/
│       └── tickets.json        # Persistent ticket storage (JSON file)
│
├── frontend/
│   ├── app/
│   │   ├── page.tsx            # Redirects to /voice
│   │   ├── layout.tsx          # Root layout
│   │   ├── globals.css
│   │   ├── voice/page.tsx      # Voice Assistant UI
│   │   ├── dashboard/page.tsx  # Main dashboard (auto-refreshes every 5s)
│   │   ├── tickets/page.tsx    # Ticket management with filters
│   │   ├── analytics/page.tsx  # Charts (Recharts)
│   │   └── settings/page.tsx   # Settings (saved to localStorage)
│   ├── components/
│   │   ├── Navbar.tsx
│   │   ├── StatsCards.tsx
│   │   ├── TicketTable.tsx     # Table + View modal + Resolve button
│   │   ├── VoiceAssistant.tsx  # Mic UI + Bolna integration
│   │   └── AnalyticsChart.tsx  # Recharts bar/pie/line charts
│   └── lib/
│       ├── api.ts              # Fetch helper with base URL
│       └── types.ts            # Shared TypeScript types
│
├── package.json                # Root convenience scripts
└── README.md
```

---

## 🚀 Quick Start (Local Development)

### 1. Clone & install

```bash
git clone https://github.com/YOUR_USERNAME/voicedesk-ai.git
cd voicedesk-ai

# Install backend
cd backend && npm install

# Install frontend
cd ../frontend && npm install
```

### 2. Start the backend

```bash
cd backend
npm run dev
# Runs on http://localhost:5000
```

### 3. Start the frontend

```bash
cd frontend
# Copy env file
cp .env.local.example .env.local

npm run dev
# Runs on http://localhost:3000
```

### 4. Open the app

- **Voice Assistant**: http://localhost:3000/voice
- **Dashboard**:       http://localhost:3000/dashboard
- **Tickets**:         http://localhost:3000/tickets
- **Analytics**:       http://localhost:3000/analytics
- **Settings**:        http://localhost:3000/settings

---

## 🔌 API Endpoints

| Method | Endpoint        | Description                         |
|--------|-----------------|-------------------------------------|
| GET    | /tickets        | Get all tickets                     |
| POST   | /webhook        | Create ticket (from voice agent)    |
| POST   | /create-ticket  | Alias for /webhook                  |
| PATCH  | /tickets/:id    | Update ticket status                |
| DELETE | /tickets/:id    | Delete a ticket                     |
| GET    | /analytics      | Get analytics summary               |
| GET    | /health         | Health check                        |

### Webhook Payload Example

```json
{
  "name": "Rahul Sharma",
  "issue": "Payment failed but money was deducted",
  "priority": "high",
  "category": "billing"
}
```

---

## 🎙️ Bolna Voice Agent Integration

1. Create an account at [bolna.dev](https://bolna.dev)
2. Create a new agent configured to collect: `name`, `issue`, `priority`, `category`
3. Set the agent's webhook URL to your backend: `https://your-backend.onrender.com/webhook`
4. Copy the agent URL and set it in `frontend/.env.local`:

```env
NEXT_PUBLIC_BOLNA_URL=https://app.bolna.dev/agent/YOUR_AGENT_ID
```

When `NEXT_PUBLIC_BOLNA_URL` is set, the mic button opens the real Bolna agent in a new tab. Without it, the app uses demo simulation mode.

---

## ☁️ Deployment

### Backend → Render

1. Push code to GitHub
2. Go to [render.com](https://render.com) → New Web Service
3. Connect your GitHub repo
4. Settings:
   - **Root Directory**: `backend`
   - **Build Command**: `npm install`
   - **Start Command**: `node server.js`
   - **Environment**: Node
5. Deploy → copy your Render URL (e.g. `https://voicedesk-backend.onrender.com`)

### Frontend → Vercel

1. Go to [vercel.com](https://vercel.com) → New Project
2. Import your GitHub repo
3. Settings:
   - **Root Directory**: `frontend`
   - **Framework**: Next.js
4. Add environment variable:
   - `NEXT_PUBLIC_API_URL` = `https://your-backend.onrender.com`
5. Deploy

---

## 📤 GitHub Setup

```bash
cd voicedesk-ai
git init
git add .
git commit -m "Initial commit: VoiceDesk AI full-stack app"
git branch -M main
git remote add origin https://github.com/YOUR_USERNAME/voicedesk-ai.git
git push -u origin main
```

---

## ✅ Feature Checklist

- [x] Voice assistant with mic animation and state machine
- [x] Bolna agent integration (real) + demo simulation mode
- [x] POST /webhook creates tickets from voice agent
- [x] Dashboard auto-refreshes every 5 seconds
- [x] Stats cards: Total / High Priority / Created Today
- [x] Ticket table with View modal and Mark Resolved button
- [x] Tickets page with search + priority/status filters
- [x] Analytics: bar chart, donut chart, line chart (Recharts)
- [x] Settings saved to localStorage with toast confirmation
- [x] Notification toggles (all functional)
- [x] All buttons verified and working
- [x] TypeScript throughout
- [x] Tailwind CSS styling
- [x] Ready for Vercel + Render deployment

# AgroAdvisor AI (AgriSense)
## AI-Powered Agriculture Crop Advisory Assistant

AgroAdvisor AI is an enterprise-grade, full-stack, precision agronomy decision-support platform designed to assist smallholder, commercial, and progressive farmers. By combining **Google Gemini 2.5 Multi-Modal AI** (via the official `@google/genai` SDK), real-time meteorological feeds, and regional mandi commodity rates, AgroAdvisor AI delivers hyper-localized, actionable field advisories.

---

## 🌟 Implemented Features

1. **Farmer Authentication & Holding Profile**:
   - Secure identity management via Supabase Authentication (Email/Password & persistent sessions).
   - Multi-parameter agricultural profile (district, state, farm acreage, soil type, irrigation setup, organic farming method).
2. **AI-Based Crop Suitability Recommendation**:
   - Evaluates soil chemistry (NPK, pH, Organic Carbon), climate, water budget, and season (Kharif, Rabi, Zaid).
   - Generates ranked crop recommendations with duration, water demand, sowing guidelines, precautions, and risks.
3. **Multimodal Visual Disease Detection**:
   - Device camera capture or file dropzone (JPEG, PNG, WebP up to 10 MB).
   - Analyzes foliar necrosis, blights, and pustules using Gemini 2.5 Flash Vision.
   - Outputs disease taxonomy, confidence score, severity badge, and dual-track intervention (organic/biological vs certified chemical).
4. **Smart Fertilizer Prescription**:
   - Balances synthetic split application schedules (Urea, DAP, MOP, SSP) with organic amendments (FYM, Vermicompost, Neem cake, Biofertilizers like Rhizobium and PSB).
   - Soil pH conditioning (lime for acidic soils, gypsum for alkaline/saline soils).
5. **Crop-Stage Dynamic Irrigation Advisory**:
   - Phenology-based water management accounting for crop coefficient ($K_c$) stages, soil drainage (black clay vs sandy loam), and recent rainfall.
6. **Meteorological Intelligence**:
   - Live weather station integration via Open-Meteo API.
   - 5-day precipitation forecasts and farming operational alerts (wind drift spray warnings, thermal stress).
7. **Wholesale Mandi Market Prices**:
   - Live and historical agricultural commodity arrival rates (min, max, modal prices in ₹/Quintal) from wholesale APMC mandis.
8. **Interactive AI Agricultural Chatbot**:
   - Real-time conversation assistant aware of the farmer's holding profile and location.
   - Multilingual support for English, Hindi, Kannada, and Punjabi.
9. **Crop Calendar & Farming Milestones**:
   - Crop-specific 7-stage cultivation milestones with completion checkmarks and custom task additions.
10. **Advisory History & Field Archives**:
    - Complete audit trail of all previous crop recommendations, disease scans, and fertilizer prescriptions.
11. **Notifications & Weather Warnings**:
    - In-app alert center for agricultural advisories and meteorological hazards.
12. **Farmer-Centric Responsive UI**:
    - Accessible, mobile-first design with high-contrast palette (Forest Green `#166534`, Agriculture Green `#22C55E`, Earth Brown `#8B5E3C`).

---

## 🛠️ Technology Stack

| Layer | Technologies |
|---|---|
| **Frontend** | React 18, Vite, TypeScript, Tailwind CSS, React Router v6, TanStack Query v5, Lucide React icons, Recharts |
| **Backend** | Node.js (v20+ LTS), Express.js, TypeScript, Zod, Multer, Helmet, CORS, Express-Rate-Limit |
| **Artificial Intelligence** | Official `@google/genai` SDK (`gemini-2.5-flash`), Multimodal Vision, Structured JSON outputs |
| **Database & Auth** | Supabase PostgreSQL 15+, Row Level Security (RLS), Supabase Storage, SQL triggers & indexes |
| **External Integrations** | Open-Meteo High-Resolution Meteorological API, AGMARKNET / Indian APMC Market Data Adapter |

---

## 📁 Repository Structure

```text
Antigravityproject/
├── client/                     # React 18 + Vite Frontend
│   ├── public/
│   ├── src/
│   │   ├── components/         # Common, layout, disease components
│   │   ├── context/            # Supabase AuthContext & profile state
│   │   ├── pages/              # 16 complete application pages
│   │   ├── services/           # Backend API communication client
│   │   ├── types/              # Full TypeScript interfaces
│   │   ├── App.tsx             # Route definitions & protected guards
│   │   └── main.tsx            # React DOM mounting
│   ├── index.html
│   ├── tailwind.config.js
│   ├── vite.config.ts
│   └── package.json
│
├── server/                     # Node.js + Express + TypeScript Backend
│   ├── src/
│   │   ├── config/             # Zod environment validation & Supabase admin
│   │   ├── controllers/        # REST controllers (Crop, Disease, Weather, Chat...)
│   │   ├── middleware/         # Auth, Multer, Rate Limiting, Error handling
│   │   ├── routes/             # API route registration under /api
│   │   ├── services/           # Gemini AI, Crop, Disease, Weather, Market services
│   │   ├── validators/         # Strict Zod schemas for all requests & AI outputs
│   │   ├── app.ts              # Express application configuration
│   │   └── server.ts           # Server bootstrap and graceful shutdown
│   ├── .env.example
│   ├── tsconfig.json
│   └── package.json
│
├── shared/                     # Shared Zod schemas & TypeScript types
│   ├── src/schemas/agronomy.ts
│   └── package.json
│
├── supabase/                   # Production PostgreSQL Migrations
│   ├── migrations/
│   │   └── 001_initial_schema.sql # 10 tables, RLS policies, triggers, indexes
│   └── seed.sql                # Baseline mandi market records
│
├── tests/                      # Automated Test Suite
│   └── unit/validation.test.mjs # Zod schema validation tests
│
├── package.json                # Monorepo workspace configuration
└── README.md
```

---

## 🚀 Getting Started

### Prerequisites
- **Node.js** v20.x or higher
- **npm** v10.x or higher
- (Optional) **Supabase Account** & **Google AI Studio API Key**

### 1. Clone & Install Dependencies

From the project root:
```bash
# Install root, server, and client dependencies
npm.cmd install
```

### 2. Environment Configuration

#### Server (`server/.env`):
```env
PORT=5000
NODE_ENV=development
FRONTEND_URL=http://localhost:5173

# Google Gemini API Key (Obtain from Google AI Studio: https://aistudio.google.com/)
GEMINI_API_KEY=your-gemini-api-key
GEMINI_MODEL=gemini-2.5-flash

# Supabase Credentials (Obtain from your Supabase Project Settings > API)
SUPABASE_URL=https://your-project.supabase.co
SUPABASE_ANON_KEY=your-supabase-anon-key
SUPABASE_SERVICE_ROLE_KEY=your-supabase-service-role-key

# Weather & Market
WEATHER_API_BASE_URL=https://api.open-meteo.com/v1
WEATHER_API_KEY=
MARKET_API_BASE_URL=https://api.data.gov.in/resource
MARKET_API_KEY=
```

> **Note on Local Development**: If you do not yet have Supabase or Gemini keys configured, the application automatically engages its **Agronomic Rule Engine & Local Dev Mode**, allowing full navigation, UI testing, and demo advisories without crashing.

#### Client (`client/.env`):
```env
VITE_API_BASE_URL=/api
VITE_SUPABASE_URL=https://your-project.supabase.co
VITE_SUPABASE_ANON_KEY=your-supabase-anon-key
```

### 3. Database Migration (Supabase)
In your Supabase SQL Editor, execute the contents of:
- `supabase/migrations/001_initial_schema.sql` (Creates all tables, triggers, indexes, and RLS policies)
- `supabase/seed.sql` (Inserts baseline commodity rates)

### 4. Running the Application

Open two terminal windows:

**Terminal 1 (Backend Server):**
```bash
cd server
npm.cmd run dev
```
*Server starts at `http://localhost:5000`*

**Terminal 2 (Frontend Client):**
```bash
cd client
npm.cmd run dev
```
*Frontend opens at `http://localhost:5173`*

---

## 🧪 Testing

Run the automated validation and unit test suite:
```bash
node --test tests/unit/validation.test.mjs
```

---

## 🚢 Production Deployment

### Frontend (Vercel / Netlify):
1. Build client: `npm.cmd --prefix client run build`
2. Set build directory to `client/dist`.
3. Set environment variable `VITE_API_BASE_URL` to your production backend URL (e.g. `https://api.agrisense.com/api`).
4. Set `VITE_SUPABASE_URL` and `VITE_SUPABASE_ANON_KEY`.

### Backend (Render / Railway):
1. Root directory: `server`.
2. Build command: `npm.cmd install && npm.cmd run build`.
3. Start command: `node dist/server.js`.
4. Supply `GEMINI_API_KEY`, `SUPABASE_URL`, `SUPABASE_SERVICE_ROLE_KEY`, and `FRONTEND_URL`.

---

## 📜 Compliance & Safety Disclosures
- **Not a Confirmed Laboratory Diagnosis**: All AI foliar disease analyses are preliminary visual assessments. Physical leaf samples should be tested at an accredited Krishi Vigyan Kendra (KVK) or extension office before applying restricted chemical compounds.
- **Safety Waiting Periods (PHI)**: Recommended chemical pesticides display mandatory Pre-Harvest Intervals (PHI) in days and required Personal Protective Equipment (PPE) to protect farmer safety and consumer health.

#   A n t i g r a v i t y _ p r o j e c t  
 #   A n t i g r a v i t y _ p r o j e c t  
 #   A n t i g r a v i t y _ p r o j e c t  
 #   A n t i g r a v i t y p r o j e c t  
 
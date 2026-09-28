# TeenSpend — Smart Expense Tracker for Teenagers

> *"Simple enough for a teenager. Powerful enough to build real money habits."*

[![Full-Stack MVC](https://img.shields.io/badge/Architecture-MVC%20Express-6366f1.svg)](#)
[![Database](https://img.shields.io/badge/Database-Supabase%20PostgreSQL-3ecf8e.svg)](#)
[![Frontend](https://img.shields.io/badge/Frontend-React%20%2B%20Vite-61dafb.svg)](#)
[![Security](https://img.shields.io/badge/Security-JWT%20%2B%20Bcrypt%2012%20Rounds-ef4444.svg)](#)
[![Tests](https://img.shields.io/badge/Tests-18%2F18%20Passing-10b981.svg)](#)

TeenSpend is a full-stack, secure, modern financial tracker designed specifically for teenagers and youth. It empowers young earners and students to log pocket money, track daily food, travel, and gaming expenses, visualize cash flow with interactive Recharts, set monthly category caps, and receive intelligent, actionable spending recommendations without feeling judged.

---

## 🌟 Key Features

- **Multi-Source Inflow Tracking**: Log monthly pocket money from parents, math tutoring gigs, festive gifts, and cash earnings.
- **Micro-Budgeting & Category Guardrails**: Set category targets (e.g. Food: ₹2,500, Entertainment: ₹1,200) with visual progress bars and overspend alerts when passing 85% and 100%.
- **Need vs. Want Tagging**: Categorize purchases into Essential Needs vs. Discretionary Wants with automatic percentage ratios.
- **Smart Spending Suggestion Engine**: Analyzes spending velocity, high category concentrations (>30% of income), month-over-month changes, and savings consistency to provide teen-friendly, non-judgmental next actions.
- **Wishlist & Savings Goals**: Plan for noise-cancelling headphones, college books, or concert tickets with progress milestones and direct deposit tracking.
- **Graphical Analytics (Recharts)**:
  1. 6-Month Income vs. Expense Area Chart
  2. Multi-Month Expense Trend Line Chart
  3. Ranked Category Spend Horizontal Bar Chart
  4. Category Distribution Donut Chart
  5. Budget vs. Actual Comparison Bar Chart
  6. Weekly Spending Pace Chart
  7. Essential vs. Discretionary Wants Donut
- **Youth Fintech Aesthetics**: Glassmorphism, smooth gradients, light/dark mode with local storage persistence, responsive mobile drawer navigation, and accessible forms.
- **Enterprise-Grade Security**:
  - Bcrypt password hashing (12 salt rounds, never plaintext, never exposed).
  - JWT stateless session authentication.
  - Strict User Data Isolation (`WHERE user_id = authenticatedUserId`) — User A can never view, update, or delete User B's financial data.
  - Helmet security headers, CORS protection, express-rate-limit protection.

---

## 🏗️ Architecture & Technology Stack

### Backend
- **Runtime**: Node.js v20+ / v24+
- **Framework**: Express.js
- **Design Pattern**: Model-View-Controller (MVC)
  - `controllers/`: HTTP request handling and response delegation
  - `models/`: Database query abstraction with Supabase PostgreSQL
  - `services/`: Business logic (Analytics engine, Budget calculations, Smart Spending rules)
  - `middleware/`: JWT verification, centralized error handling, Joi validation runner, rate limiting
  - `validators/`: Authoritative Joi schemas for requests and queries
- **Database**: Supabase PostgreSQL (Foreign keys, constraints, and Row Level Security)
- **Security**: `bcryptjs`, `jsonwebtoken`, `helmet`, `cors`, `express-rate-limit`, `cookie-parser`

### Frontend
- **Framework**: React.js 18 + Vite 6
- **Routing**: React Router DOM v6
- **Charts**: Recharts
- **Icons**: Lucide React
- **HTTP Client**: Axios with automatic JWT interceptors and 401 handling
- **Styling**: Modern Vanilla CSS Design System with CSS variables and light/dark theme toggle

---

## 📁 Project Structure

```text
c:\Users\sb580\OneDrive\Desktop\Hackathon\
├── backend/
│   ├── src/
│   │   ├── config/
│   │   │   ├── environment.js          # Environment variable parser
│   │   │   └── supabase.js             # Supabase client & in-memory test runner
│   │   ├── controllers/
│   │   │   ├── analyticsController.js  # Dashboard analytics endpoint
│   │   │   ├── authController.js       # Register, login, profile, password
│   │   │   ├── budgetController.js     # Budget management
│   │   │   ├── categoryController.js   # Global default & custom tags
│   │   │   ├── expenseController.js    # Expense CRUD & filtering
│   │   │   ├── incomeController.js     # Income CRUD
│   │   │   ├── savingsGoalController.js# Savings goals CRUD & deposits
│   │   │   ├── suggestionController.js # Smart spending suggestions
│   │   │   └── userController.js       # User profile details
│   │   ├── middleware/
│   │   │   ├── authMiddleware.js       # JWT extraction & user scoping
│   │   │   ├── errorMiddleware.js      # Centralized error handler
│   │   │   ├── rateLimitMiddleware.js  # API and Auth rate limiters
│   │   │   └── validationMiddleware.js # Joi schema runner
│   │   ├── models/
│   │   │   ├── budgetModel.js
│   │   │   ├── categoryModel.js
│   │   │   ├── expenseModel.js
│   │   │   ├── incomeModel.js
│   │   │   ├── savingsGoalModel.js
│   │   │   └── userModel.js
│   │   ├── routes/
│   │   │   ├── analyticsRoutes.js
│   │   │   ├── authRoutes.js
│   │   │   ├── budgetRoutes.js
│   │   │   ├── categoryRoutes.js
│   │   │   ├── expenseRoutes.js
│   │   │   ├── incomeRoutes.js
│   │   │   ├── savingsGoalRoutes.js
│   │   │   ├── suggestionRoutes.js
│   │   │   └── userRoutes.js
│   │   ├── services/
│   │   │   ├── analyticsService.js     # Multi-month aggregations & KPI metrics
│   │   │   ├── budgetService.js        # Spending progress calculations
│   │   │   └── spendingSuggestionService.js # Youth financial rules engine
│   │   ├── utils/
│   │   │   ├── jwt.js                  # Token generation & verification
│   │   │   ├── password.js             # Bcrypt hashing & compare
│   │   │   └── response.js             # Uniform JSON response formats
│   │   ├── validators/
│   │   │   ├── authValidator.js
│   │   │   ├── budgetValidator.js
│   │   │   ├── expenseValidator.js
│   │   │   └── incomeValidator.js
│   │   └── app.js                      # Express configuration & security
│   ├── tests/
│   │   ├── auth.test.js                # Auth & duplicate rejection tests
│   │   ├── budgets.test.js             # Progress calculations tests
│   │   ├── expenses.test.js            # Isolation & CRUD tests
│   │   └── suggestions.test.js         # Recommendation engine tests
│   ├── server.js                       # Server startup script
│   ├── package.json
│   ├── .env.example
│   └── .env
│
├── frontend/
│   ├── public/
│   │   └── favicon.svg
│   ├── src/
│   │   ├── api/                        # Typed Axios service modules
│   │   ├── components/                 # Modals, Tables, Cards, Navigation
│   │   ├── context/                    # AuthContext, ThemeContext, ToastContext
│   │   ├── hooks/                      # useAuth, useExpenses, useAnalytics
│   │   ├── pages/                      # Dashboard, Expenses, Budgets, Analytics, etc.
│   │   ├── utils/                      # Currency formatting & date helpers
│   │   ├── App.jsx                     # Route definitions & protected layouts
│   │   ├── index.css                   # Global theme design system
│   │   └── main.jsx
│   ├── index.html
│   ├── vite.config.js
│   └── package.json
│
├── database/
│   ├── schema.sql                      # Complete Supabase DDL + Indexes + RLS
│   └── seed.sql                        # Sample development data
├── README.md
├── .gitignore
└── package.json                        # Root conductor scripts
```

---

## ⚡ Quick Start

### 1. Prerequisites
- [Node.js](https://nodejs.org/) v18+ (tested on Node v24)
- npm or yarn

### 2. Install All Dependencies
From the root workspace directory, run:
```bash
npm run install:all
```
*(Or install individually inside `/backend` and `/frontend` using `npm install`)*

---

## 🗄️ Database Setup (Supabase)

1. Create a free project at [supabase.com](https://supabase.com).
2. Open your Supabase SQL Editor.
3. Paste and run the contents of [`database/schema.sql`](file:///c:/Users/sb580/OneDrive/Desktop/Hackathon/database/schema.sql). This will:
   - Create tables: `users`, `categories`, `expenses`, `income`, `budgets`, `savings_goals`.
   - Setup Row Level Security (RLS) policies.
   - Setup high-performance foreign key indexes.
   - Insert 11 standard default teen categories (Food, Transport, Education, Gaming, Entertainment, Subscriptions, etc.).
4. *(Optional)* Run [`database/seed.sql`](file:///c:/Users/sb580/OneDrive/Desktop/Hackathon/database/seed.sql) to populate demo teenager data.
5. In your Supabase Dashboard, navigate to **Project Settings -> API** and copy:
   - `Project URL`
   - `anon / public key` or `service_role key`

---

## ⚙️ Environment Variables

Create `backend/.env` (a template is provided in `backend/.env.example`):
```ini
PORT=5000
NODE_ENV=development
CLIENT_URL=http://localhost:5173

# JWT Configuration
JWT_SECRET=your_super_secret_jwt_key_teenspend_2026_xyz
JWT_EXPIRES_IN=7d

# Supabase PostgreSQL Configuration
SUPABASE_URL=https://your-project.supabase.co
SUPABASE_ANON_KEY=your-supabase-anon-key
SUPABASE_SERVICE_ROLE_KEY=your-supabase-service-role-key
```

*Note: The backend features an intelligent fallback store that allows all automated tests and offline development to run smoothly out of the box even before cloud credentials are plugged in!*

---

## 🚀 Running the Application

### Option A: Run Both Concurrently (Recommended)
From the root directory:
```bash
npm run dev
```

### Option B: Run Individually

**Terminal 1 — Backend API Server:**
```bash
cd backend
npm run dev
# Starts on http://localhost:5000
```

**Terminal 2 — React Frontend:**
```bash
cd frontend
npm run dev
# Opens at http://localhost:5173
```

---

## 🧪 Automated Testing & Security Verification

The backend includes a comprehensive test suite covering authentication, bcrypt password hashing, expense authorization, multi-user isolation, budget calculations, and smart suggestions:

```bash
cd backend
npm test
```

### Results
```text
✔ Authentication & Security Tests (Registration, duplicate check, bcrypt, JWT)
✔ Budgets & Analytics Calculation Tests (Progress, utilization, status)
✔ Expenses CRUD & Multi-User Isolation Tests (User B CANNOT read, edit, or delete User A expenses)
✔ Spending Suggestion Engine Tests (Rules engine & teen-friendly guidance)

ℹ tests 18
ℹ suites 4
ℹ pass 18
ℹ fail 0
```

---

## 📖 REST API Documentation

All protected endpoints require the HTTP header:
`Authorization: Bearer <your_jwt_token>`

### 1. Authentication (`/api/auth`)
| Method | Endpoint | Description | Auth Required |
|---|---|---|---|
| `POST` | `/api/auth/register` | Register new user (name, email, password, age, currency, income) | No |
| `POST` | `/api/auth/login` | Authenticate with email & password, returns JWT session | No |
| `POST` | `/api/auth/logout` | Clear session cookie | No |
| `GET` | `/api/auth/me` | Fetch authenticated user profile | Yes |
| `PUT` | `/api/auth/profile` | Update profile info (name, age, currency, monthly income) | Yes |
| `PUT` | `/api/auth/change-password` | Change password with current password verification | Yes |

### 2. Expenses (`/api/expenses`)
| Method | Endpoint | Description |
|---|---|---|
| `POST` | `/api/expenses` | Record new expense (`amount`, `description`, `categoryId`, `expenseDate`, `paymentMethod`, `isNecessary`) |
| `GET` | `/api/expenses` | List expenses with filters (`?category=&startDate=&endDate=&paymentMethod=&minAmount=&maxAmount=&search=&page=1&limit=20`) |
| `GET` | `/api/expenses/:id` | Get single expense (strictly user scoped) |
| `PUT` | `/api/expenses/:id` | Update expense record |
| `DELETE`| `/api/expenses/:id` | Delete expense record |

### 3. Income (`/api/income`)
| Method | Endpoint | Description |
|---|---|---|
| `POST` | `/api/income` | Log income/pocket money (`amount`, `source`, `incomeDate`, `description`) |
| `GET` | `/api/income` | List user income entries |
| `PUT` | `/api/income/:id` | Update income record |
| `DELETE`| `/api/income/:id` | Delete income record |

### 4. Budgets (`/api/budgets`)
| Method | Endpoint | Description |
|---|---|---|
| `POST` | `/api/budgets` | Set overall monthly budget or category budget |
| `GET` | `/api/budgets?month=9&year=2026` | Get budgets with live calculated spent amount and status |
| `PUT` | `/api/budgets/:id` | Update budget target |
| `DELETE`| `/api/budgets/:id` | Delete budget target |

### 5. Analytics & Dashboard (`/api/analytics`)
| Method | Endpoint | Description |
|---|---|---|
| `GET` | `/api/analytics/dashboard` | Returns totals, savings rate, category breakdown, 6-month trends, daily & weekly pacing |

### 6. Spending Suggestions (`/api/suggestions`)
| Method | Endpoint | Description |
|---|---|---|
| `GET` | `/api/suggestions` | Generates rule-based youth financial tips with educational reasoning and action steps |

### 7. Savings Goals (`/api/savings-goals`)
| Method | Endpoint | Description |
|---|---|---|
| `POST` | `/api/savings-goals` | Create wishlist savings target |
| `GET` | `/api/savings-goals` | List user savings targets with progress |
| `PUT` | `/api/savings-goals/:id` | Update goal or deposit additional funds |
| `DELETE`| `/api/savings-goals/:id` | Delete savings target |

---

## 🔒 Security Best Practices Implemented

1. **No Plaintext Passwords**: Every password is processed with `bcryptjs` using a work factor of 12 rounds before storing in the database.
2. **Never Exposing Hashes**: Password hashes are stripped before returning any user data to the client.
3. **Identity from JWT Only**: User identity is extracted directly from the verified cryptographic JWT signature. Client-supplied `user_id` fields are never trusted.
4. **Multi-User Isolation**: Every database interaction enforces `eq('user_id', req.user.id)`. Requests targeting another user's resource return `404 Not Found` rather than exposing information.
5. **Rate Limiting**: Configured with `express-rate-limit` to prevent brute-force credential stuffing on `/api/auth` and DDoS on `/api`.
6. **Input Validation**: Authoritative Joi schemas validate types, formats, positive amounts, and string lengths before execution reaches controllers.
7. **Clean Error Handling**: Centralized error middleware ensures internal database stack traces or credentials are never leaked in API responses.

---

## 🔮 Future AI-Ready Architecture

The `spendingSuggestionService.js` is structured around a clean abstraction:
```javascript
generateSpendingSuggestions(analyticsData)
```
This enables dropping in an LLM pipeline (e.g. Gemini API, DeepMind LLM) in the future without modifying frontend components or API route contracts!

---

## 📄 License
MIT © TeenSpend Team

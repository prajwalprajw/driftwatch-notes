# Supabase + Backend Notes (DriftWatch Project)
## 🔹 What is Supabase?

Supabase = Backend-as-a-Service (BaaS)
Provides:
- Database (PostgreSQL)
- Authentication (JWT login)
- APIs (auto-generated)
- Row Level Security (RLS)
## 🔹 Why we use Supabase?
To avoid building backend features from scratch
Gives ready-made:
- user login system
- secure database access
- cloud storage
Helps build scalable apps fast
##🔹 What we did in project
## 1. Created Supabase project
Got:
- SUPABASE_URL
- SUPABASE_ANON_KEY
- SUPABASE_SERVICE_KEY
## 2. Created backend connection
- create_client(URL, KEY)
- This does NOT create database or tables
- It only creates a connection object (client)
##🔹 Two Supabase Clients
## 🟢 1. supabase_anon
- Used for user-level operations
- Works with RLS (Row Level Security)
- Each user has different data access via JWT
## 🔴 2. supabase_admin (service key)
- Used for backend/scheduler
- Bypasses RLS
- Full database access
- Used for trusted server operations
##🔹 JWT Authentication Flow
- User logs in via Supabase Auth
- Supabase returns JWT token

## Frontend sends:

- Authorization: Bearer <JWT>
- Backend verifies token using Supabase
- Supabase returns user info (user_id)
##🔹 get_current_user()
- Requires login
- Verifies JWT
- Returns user object
Else returns 401 error
##🔹 get_optional_user()
- Login is optional
- If JWT exists → returns user
- If not → returns None
Used for public features
##🔹 One-time scan vs Monitor system
## 🟢 One-time scan
- No login required
- No Supabase needed (optional)
- Stateless operation
## 🔵 Monitor system
- Requires login
- Stores user data
- Uses Supabase DB + RLS
##🔹 How Supabase differentiates users
- Same anon key for all users
- Each user gets UNIQUE JWT
- JWT contains user_id

RLS uses:

- auth.uid()

to filter data per user

##🔹 Key architecture idea
- Frontend → JWT → Backend → Supabase → Database
- JWT = user identity
- RLS = data security rule
- Client = communication bridge
##🔹 Final Summary
- Supabase = ready backend system
- create_client = connection bridge only
- anon key = user access
- service key = admin access
- JWT = user identity
- RLS = row-level security filter
##⚡ One-line revision

👉 “Supabase provides auth + database; frontend sends JWT; backend verifies user and uses Supabase client to securely access data with RLS.”

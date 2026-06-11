# USER CREATES MONITOR — FULL FLOW
# 🔹 Step 1: Frontend form

User enters:

- name, source_type, source_value, date_column,
- ontext, sensitivity, alert_email, interval_hours

AND also sends:

- JWT token
## 🔹 Step 2: Request goes to backend (FastAPI)
- Frontend → POST /create-monitor → main.py route
- it first comes to your main.py route.

# 🔹 Step 3: Auth check happens (VERY IMPORTANT)

Inside route:

- user = Depends(get_current_user)

- 👉 This calls:

- get_current_user()
- verifies JWT via Supabase
- returns user.id
# 🔹 Step 4: Backend now has user identity

Now you have:

- user_id = "abc123"

- (This is NOT from frontend — it is from Supabase Auth)

# 🔹 Step 5: Backend calls monitor function
- create_monitor(user_id, name, ...)
# 🔹 Step 6: supabase_admin stores data
- supabase_admin.table("monitors").insert(data)

- Data becomes:

- {
-  "user_id": "abc123",
 - "name": "...",
 - "source_type": "...",
 - ...
- }

- 👉 Stored in Supabase database table

## 🔹 Step 7: Supabase saves it permanently

Now row is stored in:

- monitors table (PostgreSQL)
## 🧠 FULL FLOW IN ONE LINE
- Frontend → main.py route → JWT verification → user_id extracted → create_monitor() → supabase_admin → database
## ⚡ SIMPLE VERSION

- 👉 User submits form
- 👉 Request hits FastAPI route
- 👉 JWT is checked → user_id extracted
- 👉 Backend attaches user_id
- 👉 Supabase stores monitor in DB

## 🧠 IMPORTANT INSIGHT

- ❌ User does NOT send user_id
- ✔ Backend adds user_id after authentication

## 🚀 ONE-LINE MEMORY
- Frontend sends data → backend verifies JWT → gets user_id → stores monitor in Supabase

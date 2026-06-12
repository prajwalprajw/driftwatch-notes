# App.js Authentication Notes
## 1. session

- Stores login status.

- session = null   → Not logged in

- session = object → Logged in
# 2. getSession()

When the website opens:

- Check if user already logged in before.

## How it works:

- User logs in today
      ↓
- Supabase saves session in browser storage
      ↓
- User refreshes page / closes browser
      ↓
- getSession() asks Supabase:
- "Do you already have a saved session?"
      ↓
- If yes → return session
- If no  → return null

## Purpose:

- Keeps user logged in after refresh.
## 3. Monitor Button

- When user clicks:

Set Up Monitor

- Check:

session exists?

- YES:

Open Monitor Dashboard

- NO:

Open Login Popup
## 4. One-Time Scan
No login required.

- Because:

Nothing is stored.

- Stateless feature.

## 5. Login Success
- Save session
- Close popup
- Open Monitor page
## 6. Logout
- Remove session
- Return to landing page
- Interview Answer

In App.js, I manage user authentication using Supabase. On startup, I use getSession() to restore any previously saved login session from browser storage. When a user tries to access the Monitor feature, I check whether a valid session exists. If not, a login popup is shown. One-Time Scan remains public because it is stateless and does not store user data. This provides a smooth user experience while keeping monitor features protected.

- The key thing to remember about getSession():

- It does NOT log the user in.

- It only checks whether Supabase already has a saved login session.


# Authentication Security Notes (Supabase)
Why JWT alone can be risky

- If a JWT is stolen:

- Attacker may use it until it expires.
- Common Production Solution
- Access Token  → short expiry
- Refresh Token → get new access token
- Token Rotation → refresh token changes after use

- This makes authentication more secure.

- What I did in DriftWatch
I used Supabase Authentication.

## So I did NOT manually implement:

- Refresh Tokens
- Token Rotation
- Session Renewal

because Supabase handles them automatically.

## How Supabase Auth works
- User Login
     ↓
- Supabase issues:      ---     
   • Access Token (JWT)       -----
   • Refresh Token   --
     ↓
- Browser stores session
     ↓
- Access Token expires
     ↓
- Supabase SDK automatically uses Refresh Token
     ↓
- New Access Token generated

- No custom code required from me.

- Interview Answer

I used Supabase Auth for authentication. The frontend receives a JWT after login and sends it to the backend for protected requests. The backend verifies the token using Supabase and extracts the user ID. Supabase automatically manages session persistence, refresh tokens, and token renewal, so I didn't need to implement token rotation manually.

## One-line Memory Trick
- I built authentication integration,
- Supabase built authentication infrastructure.


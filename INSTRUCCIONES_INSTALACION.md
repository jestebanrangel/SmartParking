# ParkIQ — Complete Installation Guide from Scratch
# Windows 10/11 — No prior knowledge required

---

## BEFORE YOU BEGIN — Install these programs

### 1. Node.js
* **Go to:** [https://nodejs.org](https://nodejs.org)
* Click the green **“LTS”** button to download.
* Install using all default settings (**Next → Next → Install → Finish**).

**Verify:** Open CMD (**Windows+R → type `cmd` → Enter**) and type:
`node --version`
You should see something like: `v20.11.0`

---

### 2. PostgreSQL (Database)
* **Go to:** [https://www.postgresql.org/download/windows/](https://www.postgresql.org/download/windows/)
* Click **“Download the installer”** → download the latest version (x86-64).
* **During installation:**
    * When prompted for a password, enter: **admin1234** (WRITE IT DOWN!).
    * **Port:** Leave it as **5432**.
    * **Everything else:** Next → Next → Install.
* At the end, **UNCHECK “Stack Builder”** and click Finish.

**Verify:** Close and reopen CMD, type:
`psql --version`
You should see: `psql (PostgreSQL) 16.x`

---

## STEP 1 — Place the files on your computer

1. Download the `parking-completo.zip` file.
2. Right-click on it → **“Extract All...”**
3. Extract it to: **C:\**
4. The structure should look like this:
   `C:\parking-completo\`
   `├── backend\`
   `├── frontend\`
   `└── README.md`

---

## STEP 2 — Create the database

1. Open CMD (**Windows+R → cmd → Enter**).
2. Type and press Enter:
   `psql -U postgres`
3. It will ask for a password → type: **admin1234**
   *(Note: You won’t see the characters as you type; this is normal security behavior)*.
4. Type the following and press Enter:
   `CREATE DATABASE parking_db;`
5. You should see: **CREATE DATABASE** (This confirms success).
6. Type: `\q` and press Enter to exit.

---

## STEP 3 — Configure the backend

In the CMD window, type these commands one by one:

1. `cd C:\parking-completo\backend`
2. `copy .env.example .env`
3. `notepad .env`

Notepad will open. Find the **DATABASE_URL** line and ensure it looks exactly like this (it should be correct if you used **admin1234**):

`DATABASE_URL="postgresql://postgres:admin1234@localhost:5432/parking_db"`

*If you set a different password during PostgreSQL installation, update it in this line.*

**Save (Ctrl+S)** and close Notepad.

---

## STEP 4 — Install backend libraries

Continue in the same CMD window (inside `C:\parking-completo\backend`):

1. `npm install`
   *(Wait 1–3 minutes; scrolling text is normal).*
2. `npx prisma db push`
   *(This creates the tables in your database).*
3. `npm run db:seed`

**You should see the following at the end:**
* Users created
* 20 lockers created
* Initial rate created: $20 MXN/hour
* Seed v2 completed!

---

## STEP 5 — Install frontend libraries

Open a **SECOND** CMD window (do not close the first one). Type:

1. `cd C:\parking-completo\frontend`
2. `npm install`
   *(Wait 1–2 minutes).*

---

## STEP 6 — Start the system!

You need **TWO** CMD windows open simultaneously:

**── WINDOW 1 (Backend) ──────────────────────────────**
`cd C:\parking-completo\backend`
`npm run dev`

**Expected Output:**
> 🚗 ParkIQ v2 server at http://localhost:4000
> 📡 Socket.io ready

**── WINDOW 2 (Frontend) ─────────────────────────────**
`cd C:\parking-completo\frontend`
`npm run dev`

**Expected Output:**
> ➜ Local: http://localhost:3000/

---

## STEP 7 — Open the application

1. Open **Chrome** or **Edge**.
2. Go to: [http://localhost:3000](http://localhost:3000)
3. You will see the ParkIQ login screen.

### Test Credentials
| Role | Email | Password |
| :--- | :--- | :--- |
| **ADMIN** | `admin@parking.mx` | `admin123` |
| **DRIVER** | `conductor@parking.mx` | `user123` |

---

## STEP 8 — Set up Stripe (Card Payments)

Stripe processes card payments. Without this setup, the system works normally **EXCEPT** for actual payment processing.

1. Go to: [https://dashboard.stripe.com](https://dashboard.stripe.com)
2. Create a free account.
3. Once logged in, navigate to: **Left Menu → Developers → API keys**.
4. Copy the key labeled **“Secret key”** (it starts with `sk_test_...`).
5. Open the file `C:\parking-completo\backend\.env` using Notepad.
6. Find the line **STRIPE_SECRET_KEY** and paste your key:
   `STRIPE_SECRET_KEY="sk_test_YOUR_KEY_HERE"`
7. **Save (Ctrl+S)**.
8. **Restart the backend:** Go to the backend CMD window, press **Ctrl+C**, then run `npm run dev` again.

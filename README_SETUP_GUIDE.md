# Crawley Accountants Ltd: Complete Setup, AI-Prompt Editing & GoDaddy Hosting Guide

This guide covers everything needed to run, edit using Gemini Pro prompts, manage through the Admin Panel, and host the redesigned **Crawley Accountants Ltd** full-stack website (**React.js + Node.js + MySQL**) on **GoDaddy**.

---

## 1. What Was Changed From Your Old Source Code

1. **Removed Completely:**
   - All Android App, iOS App, CAL App branding, Google Play / App Store buttons, and mobile app screenshots (`Group 1000002915.png`).
   - The `Calculate Tax` page (`/calculatetax`), navbar button, and `CalculateTax.js` file (a 301 SEO redirect from `/calculatetax` to `/services` is included so old links do not break).
   - Hardcoded EmailJS keys, placeholder testimonials (`Onetaxi`, `WopeT`, `Newdir`), fake `Watch` buttons, and old `© 2021 Developed by Flograb` footer text.
2. **Preserved:**
   - Official Crawley Accountants logos (`logo-dark.svg`, `logo-white.svg`, `Logo-HQ.png`) and favicon.
   - Brand colour palette (Navy `#0C1E3C`, Indigo `#292668`, Teal `#1AB7AC`, Gold `#F4B400`) and `Poppins` / `Inter` typography.
   - Official contact details: Landline `01293 978498`, WhatsApp `07877831129`, Email `info@crawleyaccountants.com`, Address `15 York Road, Crawley, RH10 5JT, United Kingdom`, Company No. `07469226`.
   - Real Google client reviews (`Joshua Lewis`, `Muhammad Baig`, `Edna Santos`) and the Self-Employed `£99` first-year pricing note stating Making Tax Digital (MTD) is not applicable in that price.
3. **Added New Full-Stack Features:**
   - **Node.js + Express.js + MySQL** backend (`server/`) with zero paid plugins and zero WordPress.
   - **Dedicated Admin Panel (`/admin`)** to edit homepage text, contact details, confirmed company statistics, services & prices, FAQs, client reviews, blog/insights articles, accreditation logos & PDF certificates (with expiry dates and show/hide toggles), SEO redirects, analytics IDs, and view/export enquiries as CSV.
   - **Floating UK HMRC & Website AI Assistant** (works free out of the box using the built-in UK HMRC + Crawley Accountants knowledge base, with optional `GEMINI_API_KEY` support).
   - **SEO & Tracking:** Dynamic page titles/descriptions, automatic `/sitemap.xml`, `robots.txt`, 301 redirects, and Admin fields for Google Analytics 4 (GA4), Google Search Console, Meta Pixel, and Google Ads.

---

## 2. Default Admin Panel Login Credentials

Once you run the database setup step below, log in at:
- **Local PC URL:** `http://localhost:5173/admin/login` (development) or `http://localhost:5000/admin/login` (production build)
- **Live Website URL:** `https://crawleyaccountants.co.uk/admin/login`

| Field | Default Value |
| :--- | :--- |
| **Admin Email** | `admin@crawleyaccountants.com` |
| **Default Password** | `CrawleyAdmin@2026!` |

**Important:** Change this password immediately after your first login via **Admin Panel > Homepage & Settings > Change Admin Password**.

---

## 3. Software to Install on Your Windows PC (Exact Versions)

Install these three free tools in order on Windows:

1. **Node.js (LTS Version)**
   - **Recommended version:** Node.js **22 LTS** or **24 LTS** (or current **26 LTS**). GoDaddy Node.js Hosting runs Node.js 22 ([GoDaddy Node.js Deployment Guide](https://www.godaddy.com/resources/news/deploy-a-node-js-app-to-godaddy-from-your-terminal-or-let-your-coding-agent-do-it)), and Node.js 26.13.x is the latest Active LTS ([Node.js Downloads](https://nodejs.org/en/download)). Any of 22/24/26 works cleanly with this project.
   - During installation, leave all default checkboxes ticked (including "Add to PATH").
   - Verify in Command Prompt (`cmd`) or PowerShell:
     ```bash
     node -v
     npm -v
     ```

2. **MySQL Community Server 8.4 LTS + MySQL Workbench**
   - Download **MySQL Community Server 8.4 LTS** ([MySQL 8.4 LTS Downloads](https://dev.mysql.com/downloads/mysql/8.4.html)) and **MySQL Workbench** ([MySQL Workbench Download](https://dev.mysql.com/downloads/workbench/)).
   - During setup, choose a root password (for example `RootPass123!`) and write it down. Leave the port at `3306`.

3. **Code Editor (Visual Studio Code)**
   - Install VS Code so you can open the project folder, edit `.env`, and run terminal commands in one window.

---

## 4. Step-by-Step Local Setup on Your Windows PC (Zero Errors)

### Step 1: Extract the Project Folder
Unzip `CrawleyAccountants-Redesigned-FullStack.zip` to a simple folder without spaces, such as:
`C:\Projects\crawley-accountants-web`

### Step 2: Create Your `.env` Configuration File
1. Open `C:\Projects\crawley-accountants-web` in VS Code.
2. Duplicate `.env.example` and rename the copy to `.env`.
3. Update these lines inside `.env`:
   ```env
   PORT=5000
   NODE_ENV=development
   SITE_URL=https://crawleyaccountants.co.uk

   DB_HOST=127.0.0.1
   DB_PORT=3306
   DB_USER=root
   DB_PASSWORD=PUT_YOUR_MYSQL_ROOT_PASSWORD_HERE
   DB_NAME=crawley_accountants

   JWT_SECRET=put_any_long_random_text_here_at_least_32_chars
   ADMIN_EMAIL=admin@crawleyaccountants.com
   ADMIN_PASSWORD=CrawleyAdmin@2026!
   ```
   *(Leave `SMTP_HOST` blank for local testing, or enter your GoDaddy email SMTP details to test enquiry email alerts.)*

### Step 3: Install Dependencies
Open the VS Code Terminal (`Ctrl + ~`) and run:
```bash
npm run install-all
```
This installs both `server/` and `client/` packages in one command.

### Step 4: Create the MySQL Database & Seed Initial Data
Make sure your MySQL service is running on Windows, then run:
```bash
npm run init-db
```
You should see:
- `[initDb] Tables verified/created.`
- `[initDb] Admin user created: admin@crawleyaccountants.com`
- `[initDb] Database initialization complete!`

### Step 5: Run the Website Locally
Open **two** terminals in VS Code:
- **Terminal 1 (Backend API):**
  ```bash
  npm run dev:server
  ```
- **Terminal 2 (React Frontend):**
  ```bash
  npm run dev:client
  ```
Now open your browser:
- **Public Website:** `http://localhost:5173`
- **Admin Panel:** `http://localhost:5173/admin/login`

---

## 5. How to Edit the Website Using Only Admin Panel or Gemini Pro Prompts

### A. Daily Content Changes (No Coding Needed)
Use the **Admin Panel** (`/admin`) directly for:
- Editing hero headline, subtitle, About text, phone, WhatsApp, email, address, and social links.
- Updating confirmed company statistics.
- Adding or editing services, prices, and price notes.
- Uploading accreditation logos (PNG/JPG/SVG/WebP) and PDF certificates, setting expiry dates, and toggling visibility.
- Publishing or editing Blog/Insights articles and featured images.
- Adding or editing FAQs and client reviews.
- Viewing enquiries, changing lead status, and exporting all enquiries to Excel/CSV.
- Adding Google Analytics 4 (`G-...`), Google Search Console verification code, Meta Pixel ID, Google Ads ID, and 301 SEO redirects.

### B. Layout or Feature Changes Using Gemini Pro Prompts
Whenever you want to change layout, colours, or add a new section using **Gemini Pro**, open the exact file in VS Code, paste its contents into Gemini Pro, and use one of these copy-paste prompt templates:

**Prompt Template 1: Edit Visual Design or Section Layout**
> I am editing my React + Vite website for Crawley Accountants Ltd. Below is the complete code for `client/src/pages/Home.jsx` (and `client/src/styles/global.css`).
> Please make ONLY this change: [describe exact change, e.g. change the hero button colour to gold #F4B400 and make the services grid 4 columns on desktop].
> Rules: Do not add any mobile app or tax calculator references. Keep all existing API calls and routes working. Return the complete updated file so I can copy and paste it directly.

**Prompt Template 2: Add a New Feature to Backend + Admin Panel**
> My website uses React 18 (Vite) in `client/`, Node.js + Express in `server/`, and MySQL (`mysql2/promise`).
> I want to add [describe feature].
> Please give me:
> 1. The exact SQL `ALTER TABLE` or `CREATE TABLE` query to run in MySQL Workbench.
> 2. The exact updated code for the relevant file in `server/routes/`.
> 3. The exact updated code for the relevant file in `client/src/admin/`.
> Return complete copy-pasteable files with clear file paths.

**Prompt Template 3: Fix Any Error You See in Terminal**
> I got this exact error when running `npm run build` (or `npm run dev:server`) on Windows with Node.js:
> [paste exact red error text from terminal]
> Tell me which single file caused it and give me the exact fixed code to paste.

---

## 6. Step-by-Step GoDaddy Hosting & Deployment Guide

This project uses a **single-server architecture**: once you build the React frontend (`npm run build`), the Node.js Express server (`server/app.js`) serves **both** the React website and all `/api/*` endpoints from one domain with zero CORS issues.

### Step 1: Build the Production Frontend on Your PC
In VS Code terminal, run:
```bash
npm run build
```
This creates the optimised static files inside `client/dist/`.

### Step 2: Create the MySQL Database in GoDaddy cPanel
Follow GoDaddy's official MySQL setup steps ([GoDaddy cPanel MySQL Guide](https://www.godaddy.com/help/create-a-mysql-database-in-my-web-hosting-cpanel-16016)):
1. Log in to **GoDaddy > My Products > Web Hosting > Manage > cPanel Admin**.
2. Under **Databases**, open **MySQL Database Wizard**.
3. Create a database (e.g. `cpaneluser_crawley`), create a database user with a strong password, and tick **ALL PRIVILEGES**.
4. Open **phpMyAdmin** in cPanel, select your new database, click **Import**, and upload `database/schema.sql`.

### Step 3: Deploy the Node.js App on GoDaddy
GoDaddy supports two Node.js deployment methods depending on your hosting plan:

#### Option A: GoDaddy cPanel ("Setup Node.js App" / Application Manager)
Follow the cPanel Node.js deployment documentation ([cPanel Node.js Guide](https://docs.cpanel.net/knowledge-base/web-services/how-to-install-a-node.js-application/)):
1. Zip your project folder **excluding** `node_modules` (keep `client/dist/`, `server/`, `database/`, and `package.json`).
2. In cPanel **File Manager**, create a folder named `crawley-app` in your home directory, upload the zip, and extract it.
3. Create a `.env` file inside `crawley-app/` using your **GoDaddy MySQL** database name, username, password, `DB_HOST=localhost`, `NODE_ENV=production`, `SITE_URL=https://crawleyaccountants.co.uk`, and your GoDaddy cPanel email SMTP settings (`SMTP_HOST`, `SMTP_USER`, `SMTP_PASS`).
4. Open **Setup Node.js App** (or **Application Manager**) in cPanel:
   - **Node.js Version:** Select `22.x` (or highest available LTS).
   - **Application Mode:** `Production`
   - **Application Root:** `crawley-app`
   - **Application URL:** `crawleyaccountants.co.uk`
   - **Application Startup File:** `server/app.js`
5. Click **Create**, then click **Run NPM Install** (or open cPanel **Terminal**, `cd ~/crawley-app/server && npm install --omit=dev`).
6. In cPanel **Terminal**, run `node ~/crawley-app/server/scripts/initDb.js` once to seed your admin user and initial content.
7. Click **Restart** in Setup Node.js App.

#### Option B: GoDaddy Node.js Hosting (Direct ZIP Upload)
If your plan uses GoDaddy's newer Node.js Hosting ([GoDaddy UK Node.js Hosting](https://www.godaddy.com/en-uk/hosting/nodejs)):
1. Upload the project ZIP directly in the GoDaddy Node.js Hosting dashboard (it runs `npm start` on Node.js 22 automatically).
2. Add all variables from `.env.example` into the dashboard's **Environment Variables** section.
3. Connect your domain `crawleyaccountants.co.uk` and enable HTTPS/SSL.

### Step 4: Enable HTTPS, Domain Redirect & Backups
1. **HTTPS (SSL):** In GoDaddy cPanel, confirm AutoSSL / SSL certificate is active for both `crawleyaccountants.co.uk` and `www.crawleyaccountants.co.uk`.
2. **Redirect Old Domain:** Point `crawleyaccountants.com` to `https://crawleyaccountants.co.uk` using GoDaddy Domain Forwarding (301 Permanent Redirect) so all visitors and Google links land on one canonical domain.
3. **Weekly Backup Plan:**
   - In GoDaddy cPanel, open **Backup Wizard** (or **JetBackup** if included in your plan) to download a weekly MySQL database dump + `server/uploads/` folder (which stores uploaded accreditation logos, PDF certificates, and blog images).
   - From local/SSH terminal, you can also run:
     ```bash
     mysqldump -u YOUR_DB_USER -p YOUR_DB_NAME > backup_$(date +%F).sql
     ```

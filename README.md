# ⚡ SplitFlow

SplitFlow is a premium, neumorphic expense-sharing platform inspired by Splitwise, built as a zero-compile, high-performance Single Page Application (SPA) designed to load instantly and run lag-free.

---

## Features

- **Unique Share ID**: Automatically generated `SF-XXXXXX` on signup (no phone numbers needed).
- **Group Management**: Create groups, join via Group Invite Code, and invite users via Share ID search.
- **Dynamic Splits**: Split equally, by exact dollar amounts, by percentages, or by custom shares.
- **Settlement Engine**: Intelligent client-side greedy pairing engine that minimizes the transactions required to settle the group.
- **Receipt Storage**: PDF, PNG, JPG, and JPEG receipt uploads stored securely in Supabase Storage.
- **Row-Level Security (RLS)**: Fine-grained constraints preventing users from viewing groups, expenses, and receipts they don't belong to.
- **Realtime Sync**: Subscribes to table updates in real-time.
- **SPA Routing**: Fast, smooth, and lightweight page navigation.

---

## Tech Stack

- **Core**: HTML5 + ES6 JavaScript
- **Styling**: Tailwind CSS (loaded via CDN)
- **Database/Auth/Storage/Realtime**: Supabase (JS Client SDK v2 loaded via CDN)

---

## Setup Instructions

### 1. Create a Supabase Project
1. Log in to the [Supabase Dashboard](https://supabase.com/dashboard).
2. Create a new project named **SplitFlow**.

### 2. Database Migration (`schema.sql`)
1. Go to the **SQL Editor** in the Supabase Dashboard.
2. Click **New Query**.
3. Copy the contents of the [schema.sql](file:///c:/Users/prave/.gemini/antigravity-ide/scratch/splitwise/schema.sql) file and paste them into the SQL Editor.
4. Click **Run** to create all tables, indexes, triggers, and Row Level Security (RLS) policies.

### 3. Create Storage Bucket
1. Go to the **Storage** section in the Supabase Dashboard.
2. Click **New Bucket**.
3. Name the bucket exactly `receipts`.
4. Ensure the bucket is set to **Private** (recommended since we have custom RLS policies in `schema.sql` protecting access).
5. The policies in `schema.sql` automatically enable users to view, upload, and delete receipts in the folder corresponding to their group (e.g. `group_id/receipt.jpg`).

### 4. Optional: Disable Email Confirmation (For Fast Testing)
To speed up developer testing:
1. Go to **Authentication** &gt; **Providers** &gt; **Email** in the Supabase Dashboard.
2. Toggle **Confirm Email** to **Off** and click Save.
3. This allows you to log in instantly after signing up without validating dummy email addresses.

---

## Local Development & Environment Config

Since SplitFlow is a static SPA, there are **no heavy compiler configurations, compile times, or dependencies** causing computer lag!

1. Open [index.html](file:///c:/Users/prave/.gemini/antigravity-ide/scratch/splitwise/index.html) directly in any web browser (or run a local lightweight server like VS Code Live Server or Python's `python -m http.server`).
2. You will be greeted by the **Setup Screen**.
3. Paste your **Supabase URL** and **Supabase Anon Key** (found in Project Settings &gt; API in your Supabase Dashboard).
4. Click **Connect Instance** to link your local runtime to your cloud database. Config values are stored safely in your browser's local storage.
5. Create accounts, form groups, and start splitting bills!

---

## Deployment

Since the frontend consists of a single `index.html` file, deployment is trivial and free:

### 1. Vercel
1. Install Vercel CLI: `npm install -g vercel`
2. Run `vercel` in the workspace root.
3. Follow the CLI wizard to deploy instantly.

### 2. Netlify / GitHub Pages
Upload or drag-and-drop `index.html` to deploy.
For invite links (`?join=GROUP_ID`) to function on subpages, ensure your static router routes default requests back to `index.html`.

---

## File Security Policies
- **Database**: Enforced via RLS in `schema.sql` allowing group members to read/write only their own expenses/settlements/member data.
- **Storage**: Enforced using folder names matching `group_id`. A user can only access storage path `group_id/filename.ext` if `group_id` exists in the database and user is registered as a member.

- <img width="545" height="705" alt="image" src="https://github.com/user-attachments/assets/05e2ccfb-3929-40eb-98d6-952529a55daa" />
<img width="558" height="892" alt="image" src="https://github.com/user-attachments/assets/5ac13dd7-3e4c-447a-9d07-e1224a7b4ead" />


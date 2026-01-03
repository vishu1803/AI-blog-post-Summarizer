

# 🧠 AI Blog Post Summarizer

**A Full-Stack Application for Summarizing & Enhancing Blog Articles with AI**

This project fetches articles from a source (BeyondChats), analyzes them, and performs AI-powered summarization and enhancement before displaying them in a user-friendly UI.

---

## 🚀 Project Overview

Modern content applications often need to summarize, improve readability, or reframe existing articles for SEO and user engagement. This platform does exactly that by combining:

* **Original article retrieval**
* **Search for contextual content**
* **Intelligent scraping**
* **AI-powered rewriting**
* **Frontend display with filters and pagination**

The workflow is automated and deployable in production.

---

## 📌 Table of Contents

1. [Architecture](#architecture)
2. [Features](#features)
3. [Technologies Used](#technologies-used)
4. [Installation & Setup](#installation--setup)
5. [Production Deployment](#production-deployment)
6. [Challenges Faced](#challenges-faced)
7. [Project Structure](#project-structure)
8. [API Reference](#api-reference)
9. [License](#license)

---

## 🏗 Architecture

```
                            +----------------------+
                            |   BeyondChats API    |
                            | (WordPress REST API) |
                            +----------+-----------+
                                       |
                                       v
                            +----------------------+
                            |   Laravel Backend    |
                            |   (Render + Supabase)|
                            +----------+-----------+
                                       |
                                       |  Original Articles
                                       v
           +---------------------+   +---- AI Worker ----+
           | React Frontend UI   |   | Node.js + Gemini  |
           | (Display Articles)  |<->| SerpAPI + Scrape  |
           +---------------------+   +-------------------+
```

1. **Original content** is sourced from a WordPress API.
2. **Backend** stores and serves through REST APIs.
3. **Node AI Worker** orchestrates search + scraping + AI generation.
4. **Frontend** displays content with filters and pagination.

---

## ✨ Features

### **Frontend**

✔ View original articles
✔ View AI enhanced articles
✔ Pagination & filters (Original / AI)
✔ Dark mode
✔ Back navigation
✔ Highlights references

---

### **Backend**

✔ REST API for articles
✔ Retrieves, stores, and lists articles
✔ Supports original & generated versions
✔ Linked parent/child article relationships
✔ Deployed with Docker

---

### **AI Worker**

✔ Searches Google using SerpAPI
✔ Scrapes reference sites (Cheerio + Axios)
✔ AI rewriting via Gemini
✔ Safe retry and logging support
✔ Queued execution

---

## 🧰 Technologies Used

### Frontend

* React
* Vite
* Tailwind CSS
* React Router
* React Markdown

### Backend

* Laravel 11
* PHP 8
* Eloquent ORM
* Supabase PostgreSQL
* Docker
* Render Hosting

### AI Worker

* Node.js (20+)
* Express
* Axios
* Cheerio
* SerpAPI
* Gemin AI
* Winston Logging

---

## 🛠 Installation & Setup

### 🟦 Backend — Laravel API

```bash
cd backend-laravel/backend-laravel
composer install
cp .env.example .env
```

Update `.env` with Supabase credentials:

```ini
DB_CONNECTION=pgsql
DB_HOST=your-supabase-host
DB_PORT=5432
DB_DATABASE=postgres
DB_USERNAME=postgres
DB_PASSWORD=your-password
DB_SSLMODE=require
```

Run database migrations:

```bash
php artisan migrate
```

Start local server:

```bash
php artisan serve
```

---

### 🟩 Node AI Worker

```bash
cd node-llm-worker
npm install
```

Create `.env`:

```ini
GEMINI_API_KEY=xxxx
SERPAPI_KEY=xxxx
LARAVEL_BASE_URL=http://127.0.0.1:8000
```

Start development:

```bash
npm run dev
```

---

### 🟦 Frontend

```bash
cd frontend
npm install
```

Create `.env`:

```ini
VITE_API_BASE=http://127.0.0.1:8000
VITE_GENERATOR_API=http://127.0.0.1:5000
```

Run:

```bash
npm run dev
```

---

## 🛡 Production Deployment

| Component   | Deployment          |
| ----------- | ------------------- |
| Laravel API | Render (Docker)     |
| Node Worker | Render (Docker)     |
| Frontend    | Vercel              |
| Database    | Supabase PostgreSQL |

Make sure env variables are configured correctly for production in your platforms.

---

## 🧠 API Reference

### ❗ Fetch All Articles

```
GET /api/articles
```

### ❗ Fetch Single Article

```
GET /api/articles/:id
```

### ❗ Latest Original Article

```
GET /api/articles-latest
```

### ❗ Create Article (Used internally)

```
POST /api/articles
```

---

## 🚧 Challenges Faced

### **1. Source Discovery**

The assignment did not specify where to fetch original articles.
We discovered and used the WordPress API endpoint:

```
https://beyondchats.com/wp-json/wp/v2/posts?per_page=10&orderby=date
```

---

### **2. Web Scraping Challenges**

Cloudflare protections and dynamic rendering made scraping hard.

Handled via:

* Custom user-agent
* Fallback selectors
* Error handling

---

### **3. AI Output Formatting**

Some models produce unstructured text → we enforced structured output via prompt engineering.

---

### **4. Deployment Issues**

* SSL issues with Supabase
* Render Docker configuration
* ENV var consistency
* Port binding issues

Resolved with proper Docker configuration and environment setups.

---

## 📁 Project Structure

```
/
├── backend-laravel/
├── frontend/
├── node-llm-worker/
└── README.md
```

---


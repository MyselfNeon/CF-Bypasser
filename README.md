## ⚡ Neon Bypass API

> **The ultimate, ultra-fast solver for Cloudflare Turnstile and IUAM (Under Attack Mode).**

Built for maximum stealth and speed. No bloated generic browsers—just raw performance optimized for automated scraping and bypassing. 

Developed and maintained by **[MyselfNeon](https://myselfneon.is-a.dev)**.

---

### 🚀 Why Choose Neon Bypass?

Unlike traditional automation frameworks, this solver is engineered specifically to evade modern bot detection while consuming minimal resources.

* **Blazing Fast:** Powered by the **Bun** runtime for incredibly quick execution and startup times.
* **Undetectable:** Utilizes **Rebrowser-Puppeteer** to strip away standard headless bot fingerprints.
* **Human-Like Interaction:** Integrates **Ghost Cursor** for realistic, randomized mouse movements and clicks.
* **Resource Efficient:** Automatically blocks unnecessary media, ads, and fonts to save bandwidth and memory footprint.
* **Headless Optimization:** Runs efficiently on VPS or Docker environments using **Xvfb**.
* **Smart Caching:** Built-in memory TTL caching delivers instant bypass results (~0.04s) for repeated domains.

---

### 🛠️ Quick Start & Deployment

### Method 1: Docker (Recommended)
The cleanest way to run the API without worrying about system-level Chromium or Xvfb dependencies.

```bash
# Build the Docker image
docker build -t neon-bypass .

# Run the container (detached, mapped to port 3000)
docker run -d -p 3000:3000 --name neon-bypass neon-bypass
```

### Method 2: Local Install
If you prefer to run it bare-metal, ensure you have the [Bun runtime](https://bun.sh/) installed on your machine.

```bash
# Install all required dependencies
bun install

# Launch the API server
bun start
```

---

### 📖 API Reference

### **Base Endpoint:** `/cloudflare`
* **Method:** `POST`
* **Headers:** `Content-Type: application/json`

---

### Mode A: Bypassing "Under Attack Mode" (IUAM)
Use this mode to extract the required `cf_clearance` cookie from Cloudflare's "Checking your browser" pages.

**Request Payload:**
```json
{
    "mode": "iuam",
    "domain": "[https://target-website.com](https://target-website.com)",
    "proxy": {
        "username": "user",
        "password": "pass"
    },
    "ttl": 60000 
}
```
*Note: Use the base `domain`, not the full URL path. The `proxy` and `ttl` (cache time in milliseconds) fields are optional.*

**Success Response:**
```json
{
    "code": 200,
    "cf_clearance": "your-clearance-cookie-value...",
    "user_agent": "Mozilla/5.0 ...",
    "cookies": [...], 
    "elapsed": "0.82s",
    "cached": false
}
```

---

### Mode B: Solving Turnstile (CAPTCHA)
Use this mode when you encounter a Cloudflare Turnstile widget and need the validation token to submit a form or request.

**Request Payload:**
```json
{
    "mode": "turnstile",
    "domain": "[https://target-website.com](https://target-website.com)",
    "siteKey": "0x4AAAAAA...",
    "proxy": {
        "username": "user",
        "password": "pass"
    }
}
```

**Success Response:**
```json
{
    "code": 200,
    "token": "0.X_TOKEN_VALUE...",
    "elapsed": "1.45s"
}
```

---

*Need more details or updates? Connect with **[Neon](https://myselfneon.is-a.dev)**.*

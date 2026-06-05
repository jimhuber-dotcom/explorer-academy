# Explorer Academy — Backend API

This is the secure backend server for Katherine's Explorer Academy dashboard.
It keeps your Anthropic API key hidden from the browser.

---

## What's in this repo

| File | What it does |
|------|-------------|
| `server.js` | The actual server — receives chat messages, calls Claude, returns responses |
| `package.json` | Lists the two dependencies (express, cors) |
| `render.yaml` | Tells Render how to deploy automatically |
| `.env.example` | Template showing what environment variable you need |
| `.gitignore` | Makes sure your real .env key is never uploaded |

---

## Step-by-step setup

### 1. Upload these files to GitHub

- Go to your GitHub repo (explorer-academy or whatever you named it)
- Upload all these files: server.js, package.json, render.yaml, .gitignore
- Commit with message: "Add backend server"

### 2. Connect to Render

- Go to render.com → New → Web Service
- Choose "Connect a Git repository"
- Select your GitHub repo
- Render will auto-detect the settings from render.yaml

### 3. Add your API key on Render

- In your Web Service settings, go to "Environment"
- Click "Add Environment Variable"
- Key: ANTHROPIC_API_KEY
- Value: (paste your Anthropic API key from console.anthropic.com)
- Click Save

### 4. Deploy

- Click "Deploy" — takes about 2 minutes
- When it says "Live", copy your URL — looks like:
  https://explorer-academy-api.onrender.com

### 5. Update the dashboard

- Open explorer_academy_dashboard.html
- Find this line (near the bottom in the sendMsg function):
  const resp = await fetch('https://api.anthropic.com/v1/messages', {
- Replace it with:
  const resp = await fetch('https://YOUR-RENDER-URL.onrender.com/chat', {
- Also remove the headers that include x-api-key and anthropic-version
  (the server handles those now)
- Save the file

### 6. Host the dashboard on Netlify

- Go to netlify.com/drop
- Drag your updated HTML file onto the page
- You get a URL like: https://explorer-academy-abc123.netlify.app
- That's Katherine's link — works on any device

---

## Local testing (optional)

```bash
# Install dependencies
npm install

# Create a real .env file
cp .env.example .env
# Edit .env and paste your real API key

# Start the server
npm start

# Server runs at http://localhost:3000
```

---

## Cost

- Render free tier: $0 (server sleeps after 15 min inactivity, wakes in ~30 sec)
- Render paid ($7/mo): Always on, no cold start
- Anthropic API: ~$0.01–0.05 per full conversation session
- Netlify: Free for static hosting

---

## Questions?

The server has one endpoint:
- GET / → health check, returns {"status": "Explorer Academy API is running"}
- POST /chat → sends messages to Claude, returns response

That's it. Simple by design.

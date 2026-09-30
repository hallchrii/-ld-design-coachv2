# Deployment Guide: Instructional Design Coach (v3)

## What's in the folder

| File | What it does |
|---|---|
| `index.html` | The chatbot. Opens in any browser and works offline. |
| `api/assist.js` | The AI connection. Runs on Vercel and keeps your Claude API key hidden. |
| `package.json` | Tells Vercel how to run the AI file. Leave it as is. |
| `CHATBOT-SUMMARY.md` | Project summary and talking points. |
| `DEPLOYMENT-GUIDE.md` | This guide. |

## Two modes

- **✨ AI on:** Claude classifies the need, asks follow-up questions, and tailors goals, roles, objectives, and scenarios.
- **Offline mode:** The tool uses built-in content for 9 program areas plus a custom path. It still catches typos and asks a follow-up question when a need is unclear.

The tool checks for AI when it loads, and the header shows which mode is active. If an AI call fails, the tool switches to offline mode and keeps going.

---

## Part 1: Get a Claude API key (10 minutes)

1. Go to **console.anthropic.com** and sign in.
2. Add a payment method and buy a small amount of credit.
3. Open **API Keys** and create a key. Name it `ld-design-assistant`.
4. Copy the key and store it somewhere safe. You only see it once.
5. **Set a monthly spend limit** in the Console's limits settings. This is your real protection against surprise bills.

**Estimated cost per full session:** about 1 cent on the default model (Claude Haiku 4.5). A session makes three AI calls.

---

## Part 2: Put the files on GitHub (10 minutes)

1. Sign in at **github.com** (a free account works).
2. Click **New repository**. Name it `ld-design-assistant`. Private is fine.
3. On the new repo page, click **uploading an existing file**.
4. Drag in `index.html`, `package.json`, and the whole `api` folder.
5. Click **Commit changes**.

---

## Part 3: Deploy on Vercel (10 minutes)

1. Sign in at **vercel.com** with your GitHub account.
2. Click **Add New → Project** and import `ld-design-assistant`.
3. Leave the Framework Preset as **Other**.
4. Open **Environment Variables** and add:
   - Name: `ANTHROPIC_API_KEY`
   - Value: your key from Part 1
5. Click **Deploy**.
6. Open your live URL. The header should show **✨ AI on**.

**If it shows "Offline mode":**

- Check the variable name for typos.
- Redeploy. Go to **Deployments**, open the ⋯ menu on the latest one, and click **Redeploy**. New variables only apply after a redeploy.
- Check **Logs** for errors like "Anthropic API error 401" (bad key) or "400" (model name problem).

**To update the tool later:** edit or re-upload files in GitHub. Vercel redeploys on its own.

### Optional settings

| Variable | Default | Use it to |
|---|---|---|
| `ANTHROPIC_MODEL` | `claude-haiku-4-5-20251001` | Switch models. `claude-sonnet-5` writes stronger questions and scenarios, runs slower, and costs about 2–3 cents per session. |
| `RATE_LIMIT_PER_10_MIN` | `40` | Cap AI requests per visitor. |
| `ALLOWED_ORIGINS` | none | Let a page on another domain call the API directly. Not needed for the embeds below. |

---

## Part 4: Add it to your portfolio

### Google Sites

1. Open the page in edit mode.
2. Click **Insert → Embed → By URL**.
3. Paste your Vercel URL and click **Insert**.
4. Drag the embed box to about 900px tall.
5. Write the title and description in native text blocks above it.

AI mode works in the embed because the page and the API share your Vercel address.

### Storyline 360

- **With AI:** Insert → Web Object → paste your Vercel URL.
- **Offline:** Put `index.html` alone in a folder. Insert → Web Object → choose that folder.
- Web objects don't report completion to the LMS. Add a Storyline trigger or button if you need tracking.

### LinkedIn and resume

Link straight to the Vercel URL.

---

## Privacy and safety notes

- Your API key lives only in Vercel settings. It never appears in the page.
- In AI mode, what users type goes to Anthropic to generate suggestions. Add a short note on your portfolio page, like: "AI mode sends your answers to Claude. Don't enter confidential details."
- The endpoint limits requests per visitor and rejects calls from unknown websites.
- User input is treated as data. The AI is told never to follow instructions typed into the chat.

---

## Test checklist

- [ ] Header shows **✨ AI on** at your Vercel URL
- [ ] Type a vague need ("People aren't doing it right"). The tool asks a follow-up question.
- [ ] Type a need with a typo ("onbording is slow"). The tool still finds Onboarding.
- [ ] Answer the four root-cause questions. The diagnosis matches your answers.
- [ ] AI follow-up questions refer to your situation.
- [ ] Goals, roles, and scenarios show **✨ Tailored**
- [ ] Click **Open summary (PDF-ready)**, then try both **Download PDF** and **Save as PDF or print**
- [ ] Download the plan and open the .txt file
- [ ] Open `index.html` from your computer. The header shows **Offline mode**, and the full flow still works.
- [ ] Embed works on Google Sites
- [ ] Spend limit is set in the Anthropic Console

# Automated Stock Research Assistant
> Stop reading news manually. Let AI do it for you.

---

## 🧠 The Problem

Every morning I was spending 45 minutes doing the same thing.

Open Google. Search stock news. Click article. Read. Close. Repeat 10 times.

By the time I was done, my brain was already tired and half the articles were just the same news rewritten by different journalists.

I was drowning in noise, not information.

---

## 💡 The Solution

I built an AI agent that does my entire morning research automatically.

Every morning while I sleep, it:
- Searches the web for the latest stock news
- Scrapes full article content from each source
- Uses AI to extract only raw facts, numbers and statements
- Generates a clean PDF report
- Delivers it to my inbox before I wake up

I open one email. Read one report. Make my decisions. Done.

---

## 📊 Impact

| Metric | Before | After |
|--------|--------|-------|
| Daily research time | 45 minutes | 5 minutes |
| Websites visited | 10+ | 0 |
| Manual effort | High | Zero |
| Articles missed | Often | Never |

---

## 🔄 How It Works
```
Schedule Trigger → Serper → Split Out → Remove Duplicates
→ Wait → Jina Reader → Limit → Loop Over Items
→ Wait → Groq AI → Aggregate → Code → PDFShift → Gmail
```

| Step | Tool | What It Does |
|------|------|-------------|
| 1 | Schedule Trigger | Runs automatically every morning at 9am |
| 2 | Serper API | Searches web for latest stock news |
| 3 | Split + Deduplicate | Cleans and organizes article links |
| 4 | Jina Reader | Scrapes full content from each article |
| 5 | Groq AI | Extracts raw facts, numbers and statements |
| 6 | PDFShift | Converts everything into a clean PDF |
| 7 | Gmail | Delivers report to inbox automatically |

---

## ⚡ Key Technical Decisions

**Why Jina Reader over direct scraping?**
Different news websites have different HTML structures. Jina Reader handles all of them reliably and returns clean markdown content.

**Why Groq AI over summarization?**
I don't want summaries. I want raw facts. The AI prompt is specifically designed to extract only what's actually in the article, no opinions, no additions.

**Why a Loop with Wait nodes?**
Groq's free tier has token per minute limits. Processing articles one by one with a delay prevents rate limit errors.

---

## 🚧 Challenges I Faced

| Challenge | How I Solved It |
|-----------|----------------|
| JSON errors from unescaped article content | Used `.replace()` chain to escape special characters |
| Groq model deprecation | Migrated from `llama3-8b-8192` to `llama-3.3-70b-versatile` |
| Rate limit errors on free tier | Added Wait nodes inside the loop + limited to 5 articles |
| PDFShift rejecting content | Wrapped content in proper HTML with DOCTYPE declaration |
| Wait node outside loop | Restructured workflow to place Wait inside Loop Over Items |

---

## ⚙️ Setup Instructions

1. Import `My workflow-2.json` into your n8n instance
2. Add your API keys:
   - [Serper](https://serper.dev) — Web search
   - [Groq](https://console.groq.com) — AI processing
   - [Jina Reader](https://jina.ai) — Article scraping
   - [PDFShift](https://pdfshift.io) — PDF generation
   - Gmail OAuth — Email delivery
3. Change the stock name in the Serper node query
4. Set your email address in the Gmail node
5. Activate the workflow

---

## 🛠️ Tech Stack

`n8n` `Groq AI` `Serper` `Jina Reader` `PDFShift` `Gmail` `JavaScript`

---

## 📸 Demo

**Watch Demo** - https://bit.ly/4tXTCM6 | **View Portfolio** - https://kmukhija.lovable.app

---

## 📈 Future Improvements

- [ ] Support multiple stocks in one report
- [ ] Add sentiment analysis per article
- [ ] WhatsApp delivery option
- [ ] Weekly summary report

---

*Built by [Khilesh Mukhija](https://linkedin.com/in/khilesh-mukhija)*

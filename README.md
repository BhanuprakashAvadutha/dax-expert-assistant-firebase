# DAX Expert Assistant

Claude-powered DAX formula assistant deployed on Firebase Hosting. Paste a Power BI problem in plain English, get a working DAX formula with explanation.

**Live:** [dax-expert-assistant.web.app](https://dax-expert-assistant.web.app)

## What it does

```
User: "Calculate YTD sales that resets every financial year starting April"

Claude: 
  YTD Sales FY = 
  CALCULATE(
      SUM(Sales[Amount]),
      DATESYTD(Calendar[Date], "3-31")  ← Indian FY end
  )
  
  Explanation: DATESYTD with "3-31" sets the year-end to March 31,
  making the calculation reset on April 1 — matching Indian financial year.
```

## Why I built this

Power BI users at financial firms spend hours debugging DAX. Most DAX documentation assumes a Jan–Dec calendar year, which breaks for Indian firms using Apr–Mar financial year. This assistant is pre-prompted with Indian financial market context — FY conventions, NSE/BSE data patterns, SEBI reporting requirements.

## Stack
- **Anthropic Claude API** — claude-sonnet for DAX generation
- **Firebase Hosting** — static deployment, free tier
- **Single HTML file** — no build step, instant deploy

## Deploy your own

```bash
git clone https://github.com/BhanuprakashAvadutha/dax-expert-assistant-firebase.git
cd dax-expert-assistant-firebase

# Add your API key to index.html (line 45)
# ANTHROPIC_API_KEY = 'your-key-here'

firebase deploy
```

## Example prompts
- "Running total that resets monthly"
- "Month-over-month growth % with blank handling"  
- "Top N customers by revenue with others bucket"
- "SEBI quarter dates — Q1 Apr-Jun, Q2 Jul-Sep..."

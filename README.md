# LeadFilter — $50 Intake Purchase Intent Experiment

**Live URL:** https://jarbaspsantosbr.github.io/leadfilter-landing/
**Repo:** https://github.com/jarbaspsantosbr/leadfilter-landing
**Deployed:** 2026-05-29 via GitHub Pages (free)

## What This Is

A minimal landing page to test whether solo consultants would pay $50 for an intake form that filters out unqualified leads. The page describes the benefit, includes a mock $50 CTA button (opens a "coming soon" modal), and captures email sign-ups.

## How It Works

The page has two conversion paths:

1. **$50 Button Click** — clicking "Start qualifying leads — $50" opens a modal saying "We're launching soon" and invites email signup. This is the primary conversion metric: what % of visitors are willing to pay?

2. **Email Signup** — secondary CTA for those not ready to pay. "Not ready to pay? Get on the list."

Both are tracked client-side via localStorage analytics.

## Analytics

The page has a built-in analytics engine (no external dependency). All data is tracked in `localStorage` under key `leadfilter_analytics`.

### Tracked Metrics

| Metric | Description |
|--------|-------------|
| `visitors` | Total page views (including repeats) |
| `uniqueVisitors` | Unique sessions (per browser) |
| `fiftyClicks` | Number of clicks on the $50 CTA button |
| `emailSignups` | Number of email form submissions |
| `ctaClicks` | Other CTA clicks (hero, nav) |
| `events` | Full event log with timestamps |

### Viewing Analytics (Browser Console)

Open the page in any browser, press F12, and run:

```javascript
JSON.stringify(window.getAnalytics(), null, 2)
```

To reset analytics:

```javascript
window.resetAnalytics()
```

### Conversion Rate Formula

```
$50 Interest Rate = fiftyClicks / uniqueVisitors × 100
Email Capture Rate = emailSignups / uniqueVisitors × 100
Total Engagement Rate = (fiftyClicks + emailSignups) / uniqueVisitors × 100
```

## Email Capture Backend

The email form uses Web3Forms (free tier: 250 submissions/month). 

**To activate (30 seconds):**
1. Go to https://web3forms.com/
2. Enter your email, verify it
3. Copy your access key
4. Replace `YOUR_WEB3FORMS_ACCESS_KEY` in `index.html` (line ~600)

Without a key, the form simulates success for demo purposes. Email signups are tracked in analytics regardless.

## Traffic Plan

Goal: 200+ unique visitors to get a statistically meaningful signal.

### Reddit (primary)

Post in subreddits where solo consultants hang out:

| Subreddit | Audience | Post Type |
|-----------|----------|-----------|
| r/consulting | Management/strategy consultants | Value post: "I built a $50 intake form to filter leads — here's what happened" |
| r/freelance | Freelance consultants | Problem post: "Free consultations are killing your close rate" |
| r/smallbusiness | Solo business owners | Tip post: "Why I charge for discovery calls now" |
| r/Entrepreneur | Startup consultants | Story post linking to the experiment |

**Posting guidelines:**
- Don't spam the URL directly — lead with value
- Frame as an experiment, not a sales pitch
- Example: *"I'm testing whether a $50 intake form filters serious leads from tire-kickers. Built a landing page to validate. Would love feedback from other consultants."*
- Include the link naturally in the post body
- Post across 48 hours (not all at once) to avoid spam flags

### LinkedIn

Post from Leo's LinkedIn profile:

- **Post 1 (Day 1):** "I've been thinking about the cost of free consultations. The average solo consultant spends 5-10 hours a week on calls with people who never buy. I built a quick experiment to test whether a paid intake changes the dynamic."
- **Post 2 (Day 3):** Follow-up with early results

### Traffic Tracking

All visitors from these sources will show up in the analytics. To differentiate sources, add UTM parameters to the shared URL:

- Reddit: `https://jarbaspsantosbr.github.io/leadfilter-landing/?utm_source=reddit&utm_medium=social`
- LinkedIn: `https://jarbaspsantosbr.github.io/leadfilter-landing/?utm_source=linkedin&utm_medium=social`

## Success Criteria

The experiment validates purchase intent if:

- **Strong signal:** ≥5% of visitors click the $50 button (≥10 clicks per 200 visitors)
- **Moderate signal:** 2-5% click the $50 button
- **Weak signal:** <2% click — may need to pivot messaging or target audience
- **Email validation:** Email signup rate should be 2-3× higher than $50 click rate (lower friction)

If the experiment shows strong signal, the next step is building the actual product with Stripe integration.

## Cost

**$0.00** — everything uses free tiers:
- GitHub Pages: free static hosting
- Web3Forms: free tier (250 subs/month)
- No ads, no paid tools, no monthly fees

---

## Conversion Report Template

After driving 200+ visitors, fill in:

```
=== LeadFilter Conversion Report ===
Date range: [start] — [end]

TRAFFIC
  Total visitors: ___
  Unique visitors: ___
  Traffic sources: Reddit (__%), LinkedIn (__%), Other (__%)

$50 BUTTON (PRIMARY METRIC)
  Clicks: ___
  Conversion rate: ___% (clicks / unique visitors)
  Signal strength: [strong / moderate / weak]

EMAIL SIGNUPS (SECONDARY)
  Signups: ___
  Conversion rate: ___% (signups / unique visitors)

OVERALL ENGAGEMENT
  Total engagements: ___ ($50 clicks + email signups)
  Engagement rate: ___%

OBSERVATIONS
  - 
  - 

DECISION
  [ ] Strong signal — build the product
  [ ] Moderate signal — iterate messaging, retest
  [ ] Weak signal — pivot or abandon
```

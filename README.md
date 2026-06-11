# AceTV+

The website for AceTV+, a media network for people who love the game and the culture. Sports leads the lineup, with screen (film and culture) and comedy on deck.

Tagline: We're all we got.

## What this is

A single static `index.html` site. No framework, no build step. HTML, CSS, and JavaScript are inline. Open `index.html` in a browser to preview locally, or deploy to Vercel.

## Sections

- Broadcast power-on intro
- Hero (Love the game. Not the noise.)
- Latest From The Sideline (links out to YouTube)
- Mission (Context over noise)
- Join The Deck (community and Ace+ membership waitlist)
- The Breakdown newsletter
- The Network (Sports live, Screen and Laughs on deck)
- Press and partnerships
- Straight Answers (FAQ)

## Deploy

Static site. Framework preset: Other. No build command. Output: repo root.

```bash
vercel deploy --prod
```

## Placeholders to wire up

- Google Tag Manager container ID (`GTM-XXXXXXX`)
- Beehiiv email endpoint (via n8n webhook in the `cap()` function)
- Social links (YouTube, Instagram, TikTok, Discord, X)
- Press and contact inboxes
- Media kit PDF

**[Facebook Comment Scraper](https://apify.com/dz_omar/facebook-comment-scraper?fpr=smcx63)** extracts **comments and threaded replies from any public Facebook content** — **reels, videos, photos, text posts, group posts and page posts**. Provide your URLs and run: no setup, no login and no browser extensions for public content. Cookies are optional, for private groups or login-restricted posts.

Perfect for **social media researchers**, **community managers** and **marketers** who need Facebook comment data without scrolling through thousands of posts.

## What does Facebook Comment Scraper do?

- **Every content type** — reels, videos, photos, albums, page posts (including `pfbid` URLs), group posts, permalinks and share links.
- **Threaded replies** — direct replies and nested sub-replies with full pagination, each linked to its parent.
- **Reactions breakdown** — total plus per-type counts (Like, Love, Haha, Wow, Sad, Angry, Care).
- **Author data** — ID, name, profile URL and picture, plus gender, verification and work info when available.
- **Cost control** — cap top-level comments per URL and replies per comment.
- **Resumable** — progress is saved after every URL.

### Which Facebook URLs are supported?

| Content type | Example URL | Status |
|---|---|---|
| **Reels** | `https://www.facebook.com/reel/123456789` | ✅ Supported |
| **Videos** | `https://www.facebook.com/watch/?v=123456789` | ✅ Supported |
| **Photos** | `https://www.facebook.com/photo?fbid=123456789` | ✅ Supported |
| **Photo albums** | `https://www.facebook.com/photo/?fbid=123&set=a.456` | ✅ Supported |
| **Page posts** | `https://www.facebook.com/page/posts/pfbid0Bb...` | ✅ Supported |
| **Group posts** | `https://www.facebook.com/groups/.../posts/123456789` | ✅ Supported |
| **Permalink posts** | `https://www.facebook.com/permalink.php?story_fbid=123` | ✅ Supported |
| **Share links** | `https://www.facebook.com/share/...` | ✅ Supported |

### What data can you extract from Facebook comments?

| Category | Fields |
|---|---|
| 💬 Comment | `id`, `text`, `created_at`, `created_time_unix`, `url`, `parent_id` (null for top-level), `total_reactions`, `reactions`, `like_count`, `reply_count`, `attachments`, `badges` (e.g. "Top fan") |
| 👤 Author | `id`, `name`, `url`, `profile_picture`, `gender`, `is_verified`, `work_info` |
| 🔗 Source | `source.url`, `source.id`, `source.type` (`reel`, `video`, `photo`, `post`, `unknown`) |
| 🌐 Language & run | `source_language` (e.g. `en_XX`), `translation_type`, `scraped_at` |

### Why scrape Facebook comments?

- **Sentiment analysis** — feed comments into NLP models to measure reactions to a product, campaign or event.
- **Content moderation** — find toxic, spammy or policy-violating comments at scale.
- **Competitive research** — learn audience pain points from comments on competitor posts.
- **Community management** — export every comment from your brand's posts, reels, photos or videos.
- **Academic research** — study public discourse and viral dynamics.
- **Lead generation** — find engaged users in niche communities.

### Why use Facebook Comment Scraper on Apify?

Running it on Apify gives you **API access**, **scheduling**, **monitoring**, **integrations** (Make, Zapier, n8n, webhooks) and **proxy rotation** without managing infrastructure.

## How to scrape Facebook comments

1. Open [Facebook Comment Scraper](https://apify.com/dz_omar/facebook-comment-scraper?fpr=smcx63) in Apify Console.
2. Paste one or more Facebook URLs into **URLs** — mix content types freely.
3. Choose **Sort order**: Most Relevant, Newest or All Comments.
4. Set **Max comments per URL** (start small: `10`), and turn on **Fetch replies** with a **Max replies per comment** cap if you need threads.
5. Click **Start**, then download the results as JSON, CSV or Excel, or fetch them over the API.

## How much does it cost to scrape Facebook comments?

You pay per comment and per reply delivered, plus a start fee:

| Event | FREE | BRONZE | SILVER | GOLD |
|---|---|---|---|---|
| Comment | $0.0015 | $0.00045 | $0.0004 | $0.00035 |
| Reply | $0.0018 | $0.001 | $0.0008 | $0.0006 |
| Actor start (per GB of memory) | $0.02 | $0.005 | $0.005 | $0.005 |

- **1,000 comments** cost about **$1.50** on the FREE plan price and **$0.35** on GOLD (+ the start fee).
- Replies are uneven — most comments have none while one popular comment can carry 80+ — so set `maxRepliesPerComment` to keep costs predictable.

## Input and output examples

### Input

```json
{
    "urls": [
        { "url": "https://www.facebook.com/photo?fbid=1450353236655661" },
        { "url": "https://www.facebook.com/humansofnewyork/posts/pfbid0BbKbkisExKGSKuhee9a7i86RwRuMKFC8NSkKStB7CsM3uXJuAAfZLrkcJMXxhH4Yl" },
        { "url": "https://www.facebook.com/reel/1312736054237897" },
        { "url": "https://www.facebook.com/watch?v=1673231300789929" }
    ],
    "maxCommentsPerUrl": 100,
    "fetchReplies": true,
    "maxRepliesPerComment": 5
}
```

| Field | Default | What it does |
|---|---|---|
| `urls` | — (required) | Facebook URLs to scrape; mix content types in one run |
| `commentsSortOrder` | `RANKED_FILTERED_INTENT_V1` | ⭐ Most Relevant; `REVERSE_CHRONOLOGICAL_UNFILTERED_INTENT_V1` 🕒 Newest; `RANKED_UNFILTERED_CHRONOLOGICAL_REPLIES_INTENT_V1` 💬 All Comments. The old name `commentsIntentToken` is still accepted |
| `maxCommentsPerUrl` | `10` | Top-level comments per URL; `0` or empty = unlimited. Does not count replies |
| `fetchReplies` | `false` | Fetch direct replies and nested sub-replies with full pagination |
| `maxRepliesPerComment` | `0` (unlimited) | Cap on the **whole thread** under each comment; only with `fetchReplies: true`. A maximum, not a target |
| `customCookies` | — | Optional, only for private groups or login-restricted content |

### Output

Each dataset item is one comment or reply; replies have a non-null `parent_id`.

```json
{
    "source": {
        "id": "4364570517119853",
        "url": "https://www.facebook.com/reel/4364570517119853",
        "type": "reel"
    },
    "comment": {
        "id": "892296663703975",
        "parent_id": null,
        "author": {
            "id": "100004647828036",
            "name": "Sadeer Ayad",
            "profile_picture": "https://scontent.ftlm1-1.fna.fbcdn.net/v/...",
            "url": "https://www.facebook.com/sadeer.ayad.553481",
            "gender": "FEMALE",
            "is_verified": null,
            "work_info": null
        },
        "text": "Don't you dare to move when you hear the music 😂",
        "created_at": "2026-03-11T00:57:18.000Z",
        "created_time_unix": 1773190638,
        "url": "https://www.facebook.com/reel/4364570517119853/?comment_id=892296663703975",
        "total_reactions": 1600,
        "reactions": {
            "Like": 1105,
            "Haha": 553,
            "Love": 4,
            "Sad": 1
        },
        "like_count": 1600,
        "reply_count": 4,
        "attachments": [],
        "badges": [],
        "source_language": "en_XX",
        "translation_type": "ORIGINAL"
    },
    "scraped_at": "2026-03-14T10:42:52.848Z"
}
```

### Reply record

```json
{
    "source": {
        "id": "4364570517119853",
        "url": "https://www.facebook.com/reel/4364570517119853",
        "type": "reel"
    },
    "comment": {
        "id": "942208778497508",
        "parent_id": "892296663703975",
        "author": {
            "id": "61580896441183",
            "name": "James W. Mohan",
            "profile_picture": "https://scontent.ftlm1-1.fna.fbcdn.net/v/...",
            "url": "https://www.facebook.com/profile.php?id=61580896441183",
            "gender": "MALE",
            "is_verified": null,
            "work_info": null
        },
        "text": "Sadeer Ayad or breathe",
        "created_at": "2026-03-11T01:11:04.000Z",
        "created_time_unix": 1773191464,
        "url": "https://www.facebook.com/reel/4364570517119853/?comment_id=892296663703975&reply_comment_id=942208778497508",
        "total_reactions": 51,
        "reactions": {
            "Haha": 41,
            "Like": 10
        },
        "like_count": 51,
        "reply_count": 3,
        "source_language": "en_XX",
        "translation_type": "ORIGINAL"
    },
    "scraped_at": "2026-03-14T10:42:57.056Z"
}
```

## Other Actors you might need

<!-- RECOMMENDED:START (generated by apify-actor-forge/tools/recommend.py; edits inside are overwritten) -->

| Actor | What it adds |
|---|---|
| **[Facebook Ads Scraper Pro](https://apify.com/dz_omar/facebook-ads-scraper-pro?fpr=smcx63)** | Extract Facebook Ad Library data: creatives, targeting & metrics. |
| **[Facebook Posts Scraper](https://apify.com/dz_omar/facebook-posts-scraper?fpr=smcx63)** | Groups & Profiles & NO COOKIES |
| **[Facebook Reviews Scraper](https://apify.com/dz_omar/facebook-reviews-scraper?fpr=smcx63)** | Recommendations & Owner Replies |
| **[Instagram Comment Scraper](https://apify.com/dz_omar/instagram-comment-scraper?fpr=smcx63)** | Comments from public Instagram Reels: usernames, text, likes & timestamps, no login |
| **[Facebook Marketplace Scraper](https://apify.com/dz_omar/facebook-marketplace-scraper?fpr=smcx63)** | Sellers, Vehicles & Rentals |

<!-- RECOMMENDED:END -->

## Frequently asked questions

### Do I need a Facebook account?

No — not for public content. Only private group posts or login-restricted content need browser cookies from a logged-in session.

### Can I scrape private groups?

Yes, with cookies from an account that is a member of the group, passed in `customCookies`:

```json
{
    "customCookies": [
        { "name": "c_user", "value": "<your c_user value>" },
        { "name": "xs",     "value": "<your xs value>" },
        { "name": "datr",   "value": "<your datr value>" }
    ]
}
```

Export them with the [Copy Cookies](https://chromewebstore.google.com/detail/copy-cookies/jcbpglbplpblnagieiknmmkiamekcdg) Chrome extension (log in to facebook.com → **Copy as JSON**) or [Cookie-Editor](https://cookie-editor.com/) (**Export → Export as JSON**). Treat these values like a password and never share them; use a dedicated account if you are concerned about account security.

### How are my cookies protected?

They are **encrypted at rest** (AES-256-GCM with a 2048-bit RSA key unique to your user and this Actor), **decrypted only inside the Actor**, **never logged** or shown in the Console, and isolated per user and Actor.

### How does `maxCommentsPerUrl` interact with replies?

It limits **top-level comments only**. With `fetchReplies: true` and no reply cap, every reply of the collected comments is fetched — `maxCommentsPerUrl: 10` gives 10 top-level comments plus all their replies. Use `maxRepliesPerComment` to cap threads; a low value also makes runs on large threads noticeably faster.

### What is the difference between the sort modes?

**Most Relevant** mirrors Facebook's default — friends' and highly-reacted comments first (good for engagement analysis). **Newest** returns all comments newest first (real-time monitoring). **All Comments** includes lower-engagement comments Facebook normally filters out (the most complete dataset).

### What happens if a run is interrupted?

| Trigger | What gets saved |
|---|---|
| After each URL completes | Processed IDs and current position |
| Platform migration | Full state snapshot |
| End of run | State cleared |

The next run resumes from the next unprocessed URL — no duplicates, no lost progress.

### Why am I getting empty results?

| Situation | What you see in logs | What to do |
|---|---|---|
| No session established | `No valid session` | Run again; if it persists, provide cookies |
| Facebook returns an empty response | `Could not parse comments from root query response` | Check the post is public; try again in a few minutes |
| Post has 0 comments | `Total comments reported by Facebook: 0` | Expected — no data to collect |
| Private content without cookies | `Could not extract feedbackId` | Provide cookies from an account that can access it |

If a URL format isn't working, [open an issue on the Actor page](https://console.apify.com/actors/K5EXlxalV2BCYfgKM/issues).

### Is it legal to scrape Facebook comments?

The Actor processes publicly available data (and, with your own cookies, content your account can see). Comply with Facebook's terms and data-protection laws (GDPR, CCPA) when storing or using personal data. This is not legal advice.

### Can I use Facebook Comment Scraper in Make, Zapier, n8n or my own code?

Yes — through Apify's integrations, or with the Apify API and client libraries.

## Support

- 🌐 **Website:** [flowextractapi.com](https://flowextractapi.com)
- 📧 **Email:** [support@flowextractapi.com](mailto:support@flowextractapi.com)
- 💬 **GitHub:** [FlowExtractAPI](https://github.com/FlowExtractAPI)
- 💼 **LinkedIn:** [flowextract-api](https://www.linkedin.com/in/flowextract-api/)
- 🐦 **X (Twitter):** [@FlowExtractAPI](https://x.com/FlowExtractAPI)
- 📱 **Facebook:** [flowextractapi](https://www.facebook.com/flowextractapi)
- 🎵 **TikTok:** [@flowextractapi](https://www.tiktok.com/@flowextractapi)

## Legal & compliance

- **Public data only** — public Facebook content by default; cookies are optional and only for content your own account can access.
- **Rate limiting** — modest request rates with back-off.
- **Data protection** — no storage of personal information or unauthorized data collection.
- **Commercial use** — suitable for business intelligence and research.
- No affiliation with or endorsement by Facebook or Meta is implied.

---

*Facebook Comment Scraper — by FlowExtract API. Turn any website into structured data.*

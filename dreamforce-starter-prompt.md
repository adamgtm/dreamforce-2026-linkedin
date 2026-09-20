# 2,856 Dreamforce LinkedIn posts

*Cleaned up, summarized, and ready to hand to an agent.*

Hi, I'm Adam. I didn't attend Dreamforce this year, but I still wanted to know about the big themes, the moments, and what matters for my business. So I collected the posts. I'm analyzing them and will share my takeaways in [my newsletter](https://adamgtm.com), but figured others would want the raw data too.

Here it is. Give `dreamforce-2026-posts.csv` to Claude, ChatGPT, Codex or anything else that reads a CSV, and start asking.

On GitHub, `preview-top-50.csv` opens as a table if you want to see the shape of it before downloading 3.5 MB. `dreamforce-2026-posts.csv` is the whole thing.

## How I built this

I collected the posts with [Apify](https://apify.com/?fpr=adamgtm), then used Codex and Claude to throw out everything that wasn't actually about the event, dedupe what was left, and write the one-sentence summary on every row. I ran a lot of query variants to reach as much of the conversation as I could, but LinkedIn only gives you so much, so treat this as a solid sample and not every post ever written about Dreamforce. If you want to do the same thing for your own event, [sign up for Apify free](https://apify.com/?fpr=adamgtm) and point it at your audience.

## What's in the file

2,856 rows, one per post, published between 2026-09-08 and 2026-09-18. 13 columns:

| Column | What it is |
|---|---|
| `posted_date` | UTC date the post went up. |
| `author_name` | The person or company page that wrote it. 2,110 of them. |
| `author_headline` | Their LinkedIn headline as captured. Raw, blank on 156 rows. This is your handle for segmenting the file. |
| `author_type` | `person` or `company`. 747 rows are company pages. |
| `is_repost` | `yes` on 226 rows. It's a reshare, so `post_text` is the resharer's own commentary and not the post they shared. |
| `has_media` | `yes` on 2,160 rows: the post carried an image or video. Those rows have a median 29 engagements against 9 for the rest. |
| `likes` `comments` `reposts` | Counts as measured once, on 2026-09-19. |
| `total_engagement` | The three added. Range 0 to 5,583, and 194,408 across the file. |
| `summary` | One sentence per post, written by Claude, naming what the post says. |
| `post_text` | The full post, verbatim. I normalized the line separators and left everything else, hashtags and links included. |
| `post_url` | The public LinkedIn permalink, exactly as captured. Unique, one row per post. |

I left out author profile URLs.

## Before you segment by employer

There's no employer column, on purpose. The obvious cut is Salesforce people against everyone else, and it's harder than it looks. A column that got it wrong would be worse than no column.

Use `author_headline` and write the test yourself. Two things to know first. A headline carrying the word Salesforce usually belongs to the ecosystem and not the payroll: of the 826 rows a word-match calls staff, 532 name a different employer in the same headline, "Co-Founder and Salesforce Practice Head @ Girikon Inc." among them. And the host's own pages post under product names like Sales Cloud, Tableau, MuleSoft, Trailhead, with no Salesforce in the author field at all. Make your agent say which test it used and how many rows it couldn't place.

## The shape of it

- Salesforce posted 73 times, more than anyone else. The median author posted once.
- Engagement is concentrated. The top 1% of posts hold 30% of it, the top 10% hold 62%. The median post has 22 engagements, and 196 have none. Any average you compute will be the wrong number to quote.
- 43% of the posts landed on 2026-09-18 alone.

## Three things to tell your agent

1. Engagement is attention, not proof. A well-liked post about a product doesn't mean the product sold. "The most-engaged posts said X" is fair. "X worked" is not.
2. The counts are one snapshot, read on 2026-09-19, and they've moved since. Posts published late in the week had less time to collect anything, so part of any day-over-day decline is just when I took the numbers.
3. The `summary` column is a model's reading of the post, not a source. Cluster on it, then check `post_text` before you quote.

## Openings

Paste one of these along with the CSV.

> Read `dreamforce-2026-posts.csv`. Don't summarize it. Tell me the five distinct things this crowd was arguing about, each with its post count, its share of total engagement, and three `post_url`s I can open. Rank by engagement share, not post count.

> From `dreamforce-2026-posts.csv`, pull every product or feature name that appears in `post_text`. Count unique posts per name, not mentions. Show me the top 25 with an example URL each. Then tell me which names sit mostly with people who work at the host and which ones outsiders picked up. The gap is the interesting part.

> Segment `dreamforce-2026-posts.csv` by what `author_headline` says the author does. Give me median engagement per group, the three top posts in each, and the vocabulary each group uses that the others don't. I want to know whether they were all at the same conference. Say which rows you couldn't place.

> Find the criticism in `dreamforce-2026-posts.csv`, the posts that push back, express doubt, or name something that didn't work. They'll be a small minority. Quote them, give me URLs, and tell me whether they earned more or less engagement than the enthusiasm did.

> Take the 50 highest-engagement posts in `dreamforce-2026-posts.csv` and read them as writing, not data. What do they share in openings, length, formatting, whether they name people? Give me the pattern, then the ones that did well without it.

> Using `posted_date`, show me what the conversation was about each day. I want to see what arrived on keynote day and what only turned up in the recaps.

## Then push on it

The summaries make the file quick to skim, which isn't the same as knowing what's in it. When a finding matters, make the agent quote `post_text` and hand you the `post_url`, and go open it. Then ask what it left out.

---

*Built by Adam Schoenfeld. More at [adamgtm.com](https://adamgtm.com). Source snapshot `8ce9402636dd400d`, packed 20 September 2026. Use it and quote it, a link back is appreciated.*

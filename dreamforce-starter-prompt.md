# Dreamforce 2026 on LinkedIn

`dreamforce-2026-posts.csv` is next to this file: 2,856 LinkedIn posts about Dreamforce 2026, published between 2026-09-08 and 2026-09-18. A model read every one to confirm it is about the event and not just using the word.

Give both files to Claude, ChatGPT, Codex or any agent that reads a CSV, and start asking.

Looking at this on GitHub: `preview-top-50.csv` opens as a table in the browser if you want to see the shape of it first. `dreamforce-2026-posts.csv` is the whole file, behind the download button.

---

## What is in the file

2,856 rows, one per post, 12 columns.

| Column | What it is |
|---|---|
| `posted_date` | UTC date the post was published. |
| `author_name` | The person or company page that wrote it. 2,110 distinct authors. |
| `author_headline` | Their LinkedIn headline as captured. Raw, unedited, blank on 156 rows. Your handle for segmenting the file. |
| `author_type` | `person` or `company`. 747 rows are company pages. |
| `is_repost` | `yes` on 226 rows. The post is a reshare, so `post_text` is the resharer's own commentary, not the post they shared. |
| `likes` `comments` `reposts` | Counts as measured once, on 2026-09-19. |
| `total_engagement` | The three added. Range 0 to 5,583, and 194,408 across the file. |
| `summary` | One sentence per post, written by Claude, naming what the post says. |
| `post_text` | The full post, verbatim. Line separators normalised, nothing removed, hashtags and links intact. |
| `post_url` | The public LinkedIn permalink, exactly as captured. Unique: one row per post. |

Author profile URLs are not included.

## Before you segment by employer

There is no employer column, on purpose. The obvious cut, Salesforce people against everyone else, is harder than it looks, and a column that got it wrong would be worse than no column.

Use `author_headline` and write the test yourself, knowing two things. A headline carrying the word Salesforce usually belongs to the ecosystem, not the payroll: of the 826 rows a word-match calls staff, 532 name a different employer in the same headline, "Co-Founder and Salesforce Practice Head @ Girikon Inc." among them. And the host's own pages post under product names like Sales Cloud, Tableau, MuleSoft, Trailhead, with no Salesforce in the author field at all. Make your agent say which test it used and how many rows it could not place.

## The shape of it

- Salesforce posted 73 times, more than anyone else. The median author posted once.
- Engagement is concentrated. The top 1% of posts hold 30% of it, the top 10% hold 62%. The median post has 22 engagements, and 196 posts have none. Any average you compute will be the wrong number to quote.
- 43% of the posts landed on 2026-09-18 alone.

## What it answers, and what it does not

It answers what the conversation was about. Which products, sessions and people got named, how often, and by whom. How the talk moved across the days. What people complained about. Which posts earned engagement and how they were written. Which vendors other than the host surfaced, and in whose words.

It cannot tell you how big Dreamforce was on LinkedIn. This is a measured sample of a conference, not a census. LinkedIn search returns about 250 posts per query per sort, so depth comes from running many query variants, and some of the conversation was never reachable. Do not compare this row count against another event's.

Three things to tell your agent:

1. Engagement is attention, not proof. A well-liked post about a product does not mean the product sold. "The most-engaged posts said X" is fair. "X worked" is not.
2. The counts are one snapshot, read on 2026-09-19, and they have moved since. Posts published late in the week had less time to collect anything, so part of any day-over-day decline is just when the numbers were taken.
3. The `summary` column is a model's reading of the post, not a source. Cluster on it, then verify against `post_text` before quoting.

## Openings

Paste one of these along with the CSV.

> Read `dreamforce-2026-posts.csv`. Do not summarise it. Tell me the five distinct things this crowd was arguing about, each with its post count, its share of total engagement, and three `post_url`s I can open. Rank by engagement share, not post count.

> From `dreamforce-2026-posts.csv`, pull every product or feature name that appears in `post_text`. Count unique posts per name, not mentions. Show me the top 25 with an example URL each. Then tell me which names sit mostly with people who work at the host and which ones outsiders picked up. The gap is the interesting part.

> Segment `dreamforce-2026-posts.csv` by what `author_headline` says the author does. Give me median engagement per group, the three top posts in each, and the vocabulary each group uses that the others do not. I want to know whether they were all at the same conference. Say which rows you could not place.

> Find the criticism in `dreamforce-2026-posts.csv`, the posts that push back, express doubt, or name something that did not work. They will be a small minority. Quote them, give me URLs, and tell me whether they earned more or less engagement than the enthusiasm did.

> Take the 50 highest-engagement posts in `dreamforce-2026-posts.csv` and read them as writing, not data. What do they share in openings, length, formatting, whether they name people? Give me the pattern, then the ones that did well without it.

> Using `posted_date`, show me what the conversation was about each day. I want to see what arrived on keynote day and what only turned up in the recaps.

## Then interrogate it

The summaries make the file skimmable, which is not the same as knowing what is in it. When a finding matters, make the agent quote `post_text` and hand you the `post_url`, and go open it. Ask what would have to be true for the answer to be wrong. Ask what it left out.

---

*Collected and published by Adam Schoenfeld at [adamgtm.com](https://adamgtm.com), The GTM Report. Source snapshot `8ce9402636dd400d`, packed 20 September 2026. Use it and quote it. A link back is appreciated.*

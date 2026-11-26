---
name: website-review
description: Review a website by using it in a browser, beyond Fulldev Scan's automatic checks, how it looks, how easy it is to use and what happens when you try it, with screenshots and screen recordings as proof, and put the result in a shared scan report. Use when the person asks for a deeper review, analysis or audit of a website, or for a shared scan report with their own findings.
license: MIT
compatibility: Needs the Fulldev CLI (the fulldev skill), a browser you can drive, such as Playwright, and ffmpeg for recordings.
---

# Website review

Fulldev Scan checks a website by itself. A review adds what only someone using the site sees, and the shared report shows it on top, with the scan under it: the sharer's note, a summary of the scan in three points and the review's findings with their screenshots and recordings. It is done on request, never on a schedule.

## Before you start

- Find the website in Scan with `scan_list_sites` and its latest scan with `scan_get_result`. Keep the id of its latest completed or partial scan: `lastScan.id` unless that scan failed, else the newest such scan from `fulldev api services query scan runs --site-id <siteId>`. The report shares that scan. Read its own findings with the CLI, `fulldev api services query scan report --id <runId>`, following `findings.nextCursor` with `--after`; `scan_get_findings` lists the site's open findings across scans, so it can hold one the shared scan lacks. Without a finished scan, ask the person whether to run one with `scan_run`.
- You need a browser you can drive. Without one, say so and stop: a review holds only what you saw yourself.

## Review

Use the live site at a phone width (390 px) and a desktop width (1440 px), as a first-time visitor:

1. **First view:** what the site sells or does, for whom, and its main action, without scrolling.
2. **Finding things:** the menu on a phone, search with a common and a misspelled term, filters and sorting.
3. **The main path:** in a shop a product from a category into the cart and through checkout up to payment; elsewhere a contact, quote or booking form up to sending. Never pay, order, send a form, create an account or sign up, unless the person asks.
4. **Forms:** labels, error messages, the keyboard a phone offers.
5. **Look:** layouts that break, text cut off or overlapping, low contrast, blurry or stretched images, banners and pop-ups that cover the page.
6. **Speed as felt:** how long until a page can be used on a phone.
7. **Trust:** contact details, delivery and returns, reviews, prices with VAT.
8. **The scan's findings:** check its critical findings and its main warnings on the live site. Keep what holds, and say it where a visitor sees something else than the scan suggests. A review finding that shows one of the scan's findings takes its severity and, when that is a point of the summary, says which.

## Proof

- See each problem twice, and note the page, the device and the day; say the day in what you saw. Note a page by its public address, never one of a session, such as a cart, checkout or account address.
- Take a screenshot of each problem: the screen where it shows, as WebP, with chat bubbles and pop-ups closed where they cover it.
- Record a sequence, such as a tap that ends on an error, as an MP4 of at most 20 seconds without sound, under 4 MB, that starts once the page shows: `ffmpeg -ss <start> -t 20 -i in.webm -c:v libx264 -crf 26 -pix_fmt yuv420p -movflags +faststart -an out.mp4`, and check its size.
- Keep personal data out of every file: no account pages, email addresses or other people's names.

## Write

Write in the reader's language and in the sharer's voice, first person.

- **Review findings,** most important first: a title that says what is wrong in plain words; severity (`critical` stops a visitor, `warning` costs visitors, sales or trust, `hint` is polish); what you did and saw, so the reader can repeat it; why it matters; how to fix it; the page and the device; and its screenshots and recordings, each with a caption that says what it shows.
- **Summary:** the scan's three points with the most effect, the most important first, each a title and one sentence with a concrete example from the site. A figure the scan also gives is the scan's, or says what it counts. The report adds how many of the scan's findings it shows.
- **Note:** two short paragraphs: who the sharer is, why they looked, and what was done. Say "I checked" only for what the sharer checked themselves.
- Only what you checked: no guessed causes, figures, quotes or promises.

A note and summary in Dutch read like this:

```json
{
  "note": "Ik ben Sanne van Studio Noord. We bouwen en verbeteren webshops. Je vroeg me om naar je webshop te kijken.\n\nWe hebben 1.240 pagina's gescand en een aantal punten nagelopen op de live website.",
  "highlights": [
    {
      "title": "Links naar 12 pagina's lopen dood",
      "text": "Drie producten uit de nieuwsbrief van oktober openen een foutpagina."
    }
  ]
}
```

## Share

An uploaded file is public to anyone with its address, also after the report's link is turned off, so nothing goes up before the person agrees.

1. Show the person the whole draft: the note, the summary, every review finding with its files, the scan's date and the level. `partial`, the copy for a first talk, shows the scan's findings with why they matter, without their pages or fixes, and the review without its fixes, as a first round in a short time; `full`, the technical copy, shows everything.
2. On their go-ahead, upload each file with `scan_prepare_upload` (its `contentType` and `size`), POST its bytes to `uploadUrl` and keep its `fileId`.
3. Call `scan_share_report` with `siteId`, the approved scan's id as `runId` (a newer scan only after they approve the draft updated to it), `level`, `note`, `highlights` and `review`, each file as its `fileId` and caption (`alt`). The link is public at once: open it yourself, check that every screenshot shows and every recording plays, then give the person its `url`, and never send it to anyone yourself.
4. A shared report never changes, except that a hint hidden in Scan leaves it. For a correction, share again and turn off the old link with `scan_unshare_report`.

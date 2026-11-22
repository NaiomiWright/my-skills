---
name: campaign-kit
description: Turn a short brief for any product into a full campaign kit - the Excel plan, the external pack, the internal pack, a landing page with tracked links, and a results dashboard once there is a results file. Built from the Brackenfold Settle week in this folder, including what went wrong and how it was fixed. Use when the user says "campaign kit", "run the kit", "make the plan and packs for a new product", or gives a short product brief and wants the week's work repeated.
argument-hint: "<short brief, or which parts to make>"
---

# Campaign kit

Portfolio project by Naiomi Wright. Brackenfold Settle is a made-up product.

This skill repeats one real week of work: the Brackenfold Settle campaign "A calmer Christmas", built from 16 to 22 November 2026. Every step below is what we actually did. The "Lessons" section is what went wrong and how we fixed it. Read it before you start.

## What it makes

| Part | Files | When |
|---|---|---|
| 1. Brief and plan | `plan/brief.md`, `plan/campaign-plan.xlsx` | Always first |
| 2. External pack | `external/*.md` (one file per email or post), `external/external-pack.docx`, `external/brand-review.md` | After the plan |
| 3. Internal pack | `internal/launch-email.md`, `internal/sales-briefing.docx`, `internal/customer-care-faq.docx`, `internal/launch-deck.pptx` | After the plan |
| 4. Landing page | `site/index.html`, tracked links on the Calendar tab | After the external pack |
| 5. Results | `data/<name>-results.csv`, `data/results.xlsx`, `site/dashboard/index.html`, `data/readout.md` | Only when the user gives a results file |

The user can ask for only some parts, or only some pieces of a part (for example "the plan and the three owner emails"). Make only what they ask for, and skip the rest of that part, including its review file, Word pack and Calendar updates.

If they ask for a test run, write everything into the folder they name (for example `test-run/`). Every path in this skill (`plan/`, `external/`, `internal/`, `site/`, `data/`) then means that folder instead. Never write into the main folders during a test.

Write down the start time before you begin, so you can say how long it took.

## Step 0: before anything

1. Read the user's global `CLAUDE.md`, then this project's `CLAUDE.md`. Follow both.
2. If the folder is public, every file gets the public line, word for word, and every number is labelled as made up. The line for this project is:
   "Portfolio project by Naiomi Wright. Brackenfold Settle is a made-up product."
   For a new made-up product in this folder, keep that line word for word and add a second line under it, for example: "Ravenmoor Fireside is also a made-up product." In a new project folder, use that project's own line.
3. Never invent a product detail, a claim or a number the brief does not give. If the brief is short, ask, or mark it "to confirm".
4. Check the tools on this computer once, before building anything:
   - Office files are built with **Microsoft Office itself**, driven from Windows PowerShell 5.1 (`New-Object -ComObject Excel.Application`, `Word.Application`, `PowerPoint.Application`). Test this by running it, not by looking for files.
   - Python and Node are **not** installed here. Do not plan around `openpyxl` or `python-docx`. If you need one, ask first.
   - Git and the GitHub CLI (`gh`) are installed. If a new shell cannot find them, reload the path (see Lessons).
   - Write each build as a `.ps1` script saved as UTF-8 with BOM, run it, then read the file back to check it.
5. Close the file in Excel, Word or PowerPoint before you rebuild it. An open file is locked and the save fails.

## Step 1: the brief

Get these from the user's short brief. Ask one short question at a time for anything missing.

- Company and product (made up, if the folder is public). Do a quick web search to check the name is not a real pet brand, and write the date of the check at the bottom of the brief.
- Campaign name and dates.
- Market.
- Budget (one number).
- Goal (one number, for example sign-ups for a free sample).
- What the brand wants to be known for.
- Each audience: what they care about, and one message for each. Outside the company and inside it.
- Channels. List them and say "We use these channels and no others."
- Rules for all copy. Always include: no medical claims (nothing treats, cures, prevents or calms), and no naming other products. Add any safety wording that needs checking.
- **Messages you wrote are not approved.** If the brief gives no message for an audience and nobody can answer, draft one, mark it "to confirm", and say so at the end. Never use a draft message "word for word" as if it were approved.
- **Offer terms are details too.** "UK homes only" or "while samples last" must come from the brief or be marked "to confirm".
- **Name check against the rules.** Check the product's own description too: "joint supplement" or "calming chew" can suggest a benefit on its own. Read the product name and the campaign name next to the copy rules. If either one makes a claim by itself (like "Settle" or "A calmer Christmas" did), say so in one line and offer 2 or 3 neutral names.

Write `plan/brief.md` with these sections, in this order: The campaign on one page (a table), What we want to be known for, Who we talk to, Channels, Budget summary, Sign-up targets, Rules for all copy, Name check.

## Step 2: the Excel plan

Build `plan/campaign-plan.xlsx` with Excel through PowerShell. Five tabs, in this order:

| Tab | What goes on it |
|---|---|
| Brief | The one-page table: company, product, campaign, dates, market, budget, goal, planned cost per sign-up, people reached, calendar items, audiences, channels. The last four pull from the other tabs. |
| Audiences | One row per audience: audience, internal or external, what they care about most, the one message. A copy rule under the table. |
| Calendar | Date, channel or audience, item, owner, status, tracked link. Internal rows are marked "Internal (not a campaign channel)". Briefings for the teams are dated before the first external item. Weekly updates and the wrap-up come during and after the campaign. |
| Budget | Cost line, channel, quantity, unit cost, total, notes. Shared lines (samples, postage, design, literature) are split equally across the channels. A total, the budget agreed, and a check row: "Check: total equals budget". |
| Targets | One row per channel, as a funnel: people reached, open rate (emails only), opens, click rate, clicks, sign-up rate (of clicks), sign-ups, channel cost, share of shared costs, total cost, cost per sign-up. Check rows: sign-ups equal the goal, total cost equals the budget. |

Rules for the workbook:

- Blue numbers are inputs the user can change. Black cells are formulas. Green cells pull from another tab. Write that "How to use" line at the top of the Budget and Targets tabs.
- Every total and rate is a formula, never a typed number. Check after saving: for example `Budget!E15` is `=SUM(E6:E14)` and equals the budget, and the Targets total equals the goal.
- Put the budget and the goal on the Brief tab as blue inputs. Budget and Targets pull them from there.
- Work the targets backwards from the goal, so the check rows come out true. Do not type a total to make them match.
- Wrap sign-ups in `ROUND(...,0)`. Rates like 0.8% can give 159.99999, and an "equals" check then shows FALSE.
- Social channels have no open rate. Work their clicks as people reached × click rate, and say so on the tab.
- Money cells use the £ format. Dates use the UK format (day month year).
- Freeze the header row on every tab. Bold headers. Widen columns so nothing is cut off.
- Put the public line on the Brief tab, and "All numbers are made up" under it.
- After saving, open the file again from disk and read back the totals. Say the cell and its value in the receipt.

## Step 3: the external pack

1. Write one markdown file per email or post, in `external/`. Name them by channel and order: `email-1-launch.md`, `email-2-reminder.md`, `email-3-last-chance.md`, `email-vets.md`, `facebook-1-launch.md` and so on.
2. Each email file has: send date, audience, image, subject line, preview text, then the email. Each post file has: post date, channel, image, the post, and the hashtags.
3. Use the approved message for each audience **word for word**.
4. Every promotional email needs: a sign-up link, a terms link, a privacy link and an unsubscribe link. Until the real links exist, write them as `TRACKED-LINK-TO-ADD`, `TERMS-LINK-TO-ADD`, `PRIVACY-LINK-TO-ADD` and `UNSUBSCRIBE-LINK-TO-ADD`, and add a "Before sending" note.
5. Images: the user makes them in another tool (this week, ChatGPT) and drops them in `assets/images/`. Keep the full-size PNG. Make a web copy as JPG (hero 1600 wide, social 1080 square, email banner 1200 wide). Write alt text for each in `assets/images/descriptions.md`.
6. Run the `brand-review` skill on every piece. Save it as `external/brand-review.md`. Fix every "must change" item in **every** file that has the same problem before the pack is built, and commit the fixes the same day.
7. Build `external/external-pack.docx` with Word: a cover page, then one section per item with its image, so the head of marketing can sign it off in one file.
8. Add each external item to the Calendar tab.

## Step 4: the internal pack

Read `plan/brief.md` for the inside audiences first.

| File | Rule |
|---|---|
| `internal/launch-email.md` | Written as the user, using the `my-launch-email` skill. That skill reads the user's voice file. Never copy the voice file into this folder. Ask "Does this sound like you?" |
| `internal/sales-briefing.docx` | **One page.** Check Word says "Page 1 of 1". |
| `internal/customer-care-faq.docx` | Ten questions. Dates, stock levels and the sample process. Any health question is answered "please speak to your vet". |
| `internal/launch-deck.pptx` | Five slides for the Monday team meeting: The goal, Who we are talking to, The calendar, What I need from each team, How we will measure it. |

Add each internal item to the Calendar, dated before the first external item.

## Step 5: the landing page and tracked links

1. Build `site/index.html` as one file: top bar, hero image, the owner message as the main heading, three reasons, a sample form, and the public line in the footer.
2. Take the colours from the hero image. Put them in CSS variables at the top.
3. The form is a demo. It sends nothing and saves nothing. Say so on the page, next to the form and on the thank-you message.
4. Copy the web hero image into `site/` (for example `site/hero-web.jpg`), because only `site/` is published.
5. Add a `site/.nojekyll` file.
6. Build a tracked link for every external row on the Calendar with the `tracked-link` skill:
   `<page address>?utm_source=<channel>&utm_medium=<type>&utm_campaign=<campaign>`
   Count the rows and the links. They must match, with 0 missing.
7. Publish with GitHub Pages. The live site comes from the `gh-pages` branch, which is a copy of the `site/` folder:
   - Commit on `main` first.
   - Then run `git subtree push --prefix site origin gh-pages`.
   - Check the live address loads (HTTP 200) before you say it is live.
   - Ask the user before every push.

## Step 6: results (only with a results file)

1. Save the results file as `data/<name>-results.csv`. Columns this week were: date, week, channel, audience, item, reached, opens, clicks, page_visits, sign_ups, spend_gbp. The CSV gets no public line, so it stays a clean data file. Say that in `data/README.md` instead.
2. Build `data/results.xlsx` with Excel: tabs Raw data, Summary (by channel and by week) and vs Targets. Every number on Summary and vs Targets is a formula pointing at Raw data.
3. Build `site/dashboard/index.html` in the same colours as the landing page: headline tiles, best and worst item, a filter by audience, click rate by channel, cost per sign-up by channel, sign-ups week by week, and an "About these numbers" box. Draw the charts as plain SVG in the page, so it needs nothing from outside. Add `noindex`.
4. Write `data/readout.md`: three questions (What worked? What did not work? Where would you move the money?). Ask the user each one and write her exact words. Then write your answer, then "Do we agree?".
5. Check every number in the user's answer against the data before you agree with it.

## Lessons: what went wrong and how we fixed it

These are real problems from the Brackenfold week, in the order they happened. Each one has the fix that worked.

### Tools and set-up

| What went wrong | What fixed it |
|---|---|
| Three sessions lost their first step trying `python` and `openpyxl`. Python here is only the Microsoft Store stub ("Python was not found..."). | Check tools in Step 0. Build Office files with Excel, Word and PowerPoint through PowerShell. |
| One session looked for Office `.exe` files, found none, decided Office was missing, and hand-wrote the Office XML instead. | Do not look for files. Test it: `New-Object -ComObject Excel.Application`. If that works, Office is there. Use hand-written XML only if it truly fails. |
| Git and `gh` were not installed on day one. | `winget install --id Git.Git` and `winget install --id GitHub.cli`. Then reload the path in each new shell: `$env:Path = [Environment]::GetEnvironmentVariable('Path','Machine') + ';' + [Environment]::GetEnvironmentVariable('Path','User')`. |
| GitHub sign-in looked like it failed ("emails domain could not be verified"). It had worked in the user's own browser. | Ask the user what their browser shows before trying again. |
| A real email address could end up in public commits. | Set the commit email to the GitHub "noreply" address before the first commit. |

### Excel

| What went wrong | What fixed it |
|---|---|
| "Unable to cast object of type 'System.Int32' to type 'System.String'" when setting a cell's `.Value2`. It came back on two different days. | Write numbers and formulas through `.Formula`, or cast the value first. |
| Writing a whole table at once (`Range.Value2 = $array`) failed with a cast error. | Write cell by cell. It is slower but it works. |
| A cell showed `#SPILL!` because a formula was overwritten as a range (`=B12:B21`). | After every build, read back each key formula, not only its value. |
| "The process cannot access the file... being used by another process". | Ask the user to close Excel before you rebuild, check or commit. |
| A Calendar update left 8 rows blank and put the wrong text in another row. It was found only at receipt time, after it had been pushed. | Never look rows up by position in a list. After any Calendar change, read back every row and check none are blank. |
| The user thought she had "messed up" the budget. Her change had not been saved. | Open the file from disk and show her the saved values before changing anything. |

### PowerShell traps

| What went wrong | What fixed it |
|---|---|
| Helper functions called `rd`, `SP` and `R` ran the built-in commands with the same short names instead. | Give every helper a full Verb-Noun name, like `Set-CellText`. |
| `"$r: "` is a parse error. | Write `"${r}: "`. |
| The £ sign came out wrong. | Save PowerShell scripts as UTF-8 with BOM. |
| A search of the whole user folder for the images timed out after 180 seconds. | Look in Downloads first. |

### Words and claims

| What went wrong | What fixed it |
|---|---|
| The launch email opened with a busy, noisy house, then offered a product called "Settle". Each line was fine. Together they implied it calms dogs, which the brief ruled out. UK advertising rules judge the overall impression. | Run the `brand-review` skill on every piece, not only the first. Read pieces as a whole, not word by word. Then search for claim words: a base list (anxi, stress, calm, soothe, relax, ease, pain, stiff, cure, treat, prevent) plus every banned word in this brief's own copy rules. Watch for false matches: "ease" in "please", "play" in "display", "move" in "remove". If a word like "calm" is one of the brand's values, check each match by hand. |
| The same busy-house idea was still in the vet email, a LinkedIn post and a Calendar post title after the fix. | When a review finds a problem, search every file for the same idea and fix them all. |
| The product name "Settle" and campaign name "A calmer Christmas" kept pulling the copy towards a claim. We left the campaign name off the landing page to stay safe. | Check the product and campaign names against the copy rules in Step 1, before anything is written. Suggest a neutral name if one makes a claim on its own. |
| The user asked to change "festive" to "Christmas" on the live page, then asked to change it back. | Before you change approved wording, say in one line if it will stop matching the brief and the other pieces. Undo with `git revert`, never by hand. |
| One image showed ribbon round the dog's paws (a swallowing risk) and one dog looked sad. A fix prompt was written, but the image was never remade. | Check every image for animal welfare and mood before it goes into any pack. Remake it before use. |
| The brand-review fixes were never committed. | Commit fixes the same day, with the review. |

### Checks and receipts

| What went wrong | What fixed it |
|---|---|
| The one-page sales briefing could not be proven one page, because the file had never been opened in Word. | Build Word files with Word, so it counts the pages. Or ask the user to open it and read the page count. |
| A PDF preview failed: "pdftoppm is not installed". | Check Word files through Word itself: count pages, pictures and headings. |
| The dashboard footer used other wording, not the exact public line. | Search every public file for the exact line before any push. |

### Publishing

| What went wrong | What fixed it |
|---|---|
| Two different ways were used to update the live site. The second one (a temporary `git worktree`) could not be deleted afterwards: "Permission denied". This folder is in OneDrive. | Always use `git subtree push --prefix site origin gh-pages`. Do not use `git worktree` inside OneDrive. |
| Asking GitHub to switch Pages on gave "409 already enabled". | Pushing the `gh-pages` branch switches it on. Check with `gh api repos/<owner>/<repo>/pages --jq .status` until it says "built", then check the address gives HTTP 200. It takes 10 to 25 seconds. |

### Results and readout

| What went wrong | What fixed it |
|---|---|
| The user called LinkedIn "free" because the results showed £0 spend. The plan gave it £450. | Compare spend with the plan for every channel. Flag any £0 or any big gap before anyone draws a conclusion. |
| Her week 3 figures were the four-week totals. Her Instagram "click rate" was its sign-up rate. | Keep her words exactly, then check each number against the data and say plainly which ones differ. |
| A results week with no email was the weakest week. | Point out gaps in the plan, not only in the numbers. |
| The first try on the last day hit the usage limit. | Do the biggest build early in a session. |

### How the user likes to work

- Every run starts by showing the computer name and the folder.
- One short question at a time. She often answers by voice. If a question box is skipped, ask again in the chat.
- Give 2 or 3 options when there is a choice.
- Push only when she says so. Leave files you did not change alone.
- Receipts are strict. A check is YES only with proof.
- If anything fails twice, stop and write `blockers.md` in plain words.

## Finish every run with

- A list of every file made, with its size.
- The checks you ran, and what they showed (cells and values, page counts, slide counts, link counts, HTTP status).
- Anything not done, in plain words.
- How long it took, from start to finish.

# Prototype Revision

## Priority improvements

All three peer reviewers ran the central task, and two found the same trust problem: after editing a value, the fit rating stayed the same, and the copied row combined the new value with the old rating. I confirmed it: changing "23,400 meters" to "120,000 meters" still showed **Match**, and Copy produced `120,000 meters … Match`. A researcher could paste that row into their account list and pursue the wrong account. The first two priorities fix that failure; the third makes the flow easier to use.

1. **The fit rating recalculates from what is on screen.** The rating is computed from the current field values every time the user edits, confirms, or rejects a fact, and a note appears when the rating changes ("Rating changed from Match after your changes"). The value, the rating, and the copied row can no longer disagree.
2. **Review before copy (risk safeguard).** Each fact has **Confirm** and **Reject** buttons and a status tag (From source, Edited by you, Added by you, Confirmed, Rejected). Copy stays locked until every fact with a value is confirmed or rejected. Editing a confirmed fact sends it back for review. An edited fact shows a flag that it no longer matches its source sentence, and the copied row records the review date and how many values the reviewer changed.
3. **A clearer, more readable flow.** A "New here?" line tells first-time users where to start, a progress counter shows how many facts are reviewed, and the fields are now multi-line, so long values such as trigger events are no longer cut off. I also added a fourth prepared sample, a co-op job posting, to test a document type that does not use the word "cooperative."

I also fixed access: all three reviewers got "Page not found" from the private Replit link. The Replit is now published, and GitHub Pages serves a backup copy.

## Response to peer feedback

Three classmates reviewed the First Working Slice.

| Feedback or observed issue | Decision | What changed, or why it was deferred |
| --- | --- | --- |
| The Replit link returned "Page not found" and asked for an invite (all three reviewers). Two ran `index.html` from GitHub instead; one could not test the app at all. | Acted on | Published the Replit app with a public link and added a GitHub Pages backup link. Both are at the top of the README. |
| After editing the meter count (to 5,000 in one review, 120,000 in another), the rating stayed **Match** and the copied row read "120,000 meters … Match" (two reviewers). | Acted on | The rating now recalculates on every edit and shows when it changed. Both reviewers' inputs now rate **No match** (test R, below). |
| Flag any field whose edited value no longer matches its source sentence (one reviewer). | Acted on | An edited fact is tagged "Edited by you," with a warning under its source sentence, and it must be re-confirmed before Copy unlocks. |
| Showing the exact source sentence for every fact makes verification fast (all three, as a strength). | Kept | The source sentence remains the center of the review step, and the new Confirm/Reject buttons sit directly beneath it. |
| Expand beyond the three prepared sample documents to real utility documents (one reviewer). | Adapted | I added a fourth prepared sample of a different document type (a job posting). I deferred connecting a live model to the final project: it needs an API key, cost controls, and its own testing, and this milestone's evidence pointed to fixing trust in the review step first. |

## Evaluation

Tested November 18, 2026, in Chromium at desktop width and at 390 px phone width, with no page errors. All extraction results are **prepared by hand (Wizard-of-Oz)**, so these tests check whether the flow, rating, and safeguards work and whether the example outputs are understandable. **They do not measure how accurate a real AI model would be.**

| Case | Input or action | Expected result / success criterion | Actual result | Pass, partial, or fail | Implication or next step |
| --- | --- | --- | --- | --- | --- |
| Typical 1 | Sample: co-op annual report → Analyze → confirm all five facts → Copy | Five facts, each with its source sentence; rated **Match**; Copy locked until all five are reviewed, then copies one complete row | All five facts with quotes; **Match** with rule shown; counter went 0 → 5 of 5; Copy unlocked and copied the row with "Reviewed 2026-11-18" | Pass | The core flow works end to end. Reviewing five facts adds about five clicks, which still fits the "minutes, not an hour" goal. |
| Typical 2 | Sample: co-op job posting (an "electric membership corporation," 41,000 meters, owns SCADA) → Analyze → confirm all → Copy | Recognized as a co-op even though the text never says "cooperative"; rated **Match**; all five facts filled with quotes | Type shown as "Electric distribution cooperative (electric membership corporation)"; **Match**; five facts with quotes; row copied | Pass | Shows why the task needs AI rather than keywords, but this result was prepared by hand. A live model must be tested on real job postings. |
| Challenge | Sample: member newsletter ("roughly 18,000 members," no operations detail) | Members not treated as meters; missing facts shown as "Not found," not invented; rating explains what is missing | Size shown as "About 18,000 members (meter count not stated)"; three facts "Not found"; **Not enough information**, naming meter count and SCADA; only 2 facts to review | Pass | The honest "not enough information" result is useful: it tells the researcher which facts to look up next. |
| Invalid or empty | (a) Analyze with an empty box. (b) Paste an unrelated sentence about a soccer game. | (a) Clear error, no results. (b) No invented facts; user is told why the profile is blank; nothing can be copied while the profile is empty | (a) "Paste some text about a utility first…" error; no results shown. (b) Note that only the four samples have prepared results; blank profile rated **Not enough information**; Copy locked with "Add at least one value to copy a profile." | Pass | No dead ends. Non-sample text still gets no AI help, which is the main remaining limitation. |
| Risk | Annual report sample: confirm all five facts, then change meters to "120,000 meters" and try to copy | Rating changes to **No match**; edited fact flagged; Copy locks again until the edit is re-confirmed; copied row shows the new rating and records the edit | Rating changed to **No match** with "Rating changed from Match after your changes"; size tagged "Edited by you" with the mismatch warning; counter dropped to 4 of 5 and Copy locked; after re-confirming, the row read "120,000 meters … No match … 1 value(s) edited by reviewer" | Pass | The value, rating, and copied row now agree. One reviewer's 5,000-meter edit also now rates **No match**. Rejecting the SCADA fact correctly drops the rating to **Partial**. |

### Before and after: the same edit

Input: the co-op annual report sample, with "23,400 meters" changed to "120,000 meters."

| | Before (First Working Slice) | After (this revision) |
| --- | --- | --- |
| Rating | Stayed **Match** | Changes to **No match**, with the rule "120,000 meters is outside the 10,000 to 80,000 target range" and a note that the rating changed |
| Edited field | No sign that it differed from the source sentence still showing 23,400 | Tagged "Edited by you," with a warning that it no longer matches the source |
| Copy | Copied "120,000 meters … Match" immediately | Locked until the edit is re-confirmed; then copies "120,000 meters … No match … 1 value(s) edited by reviewer" |
| Screenshot | [before-edit-120000-meters.png](screenshots/before-edit-120000-meters.png) | [after-edit-120000-meters.png](screenshots/after-edit-120000-meters.png) |

The revision fixed the problem the reviewers reported: a copied profile can no longer pair a value with a rating that contradicts it.

### What the evidence tells me

The central flow now works from paste to a reviewed, copied row, and the rating and copied row stay consistent with whatever the user edits, which was the main trust problem reviewers found. The tests support the claim that **reviewing** a sourced draft is fast and that the safeguards behave correctly. They do **not** support the claim that AI can produce these drafts accurately, because every extraction was written by hand for four fictional documents; any real utility document still gets a blank profile. The fit rules are also simple: they read numbers from free text, so an edit like "about twenty thousand meters" would not be recognized as a meter count. Untested so far: whether researchers actually read the source sentence before clicking Confirm, and how a real model performs on messy public documents. Next I would connect a language model, run it on 5 to 10 real public co-op documents, and count how often the quote check has to remove a fact.

## Risk response: over-reliance on AI output

**Who is affected and what could go wrong:** the researcher, and the sales team that uses the account list. If the tool's output flows straight into a spreadsheet unchecked, a wrong fact or a stale rating can send the team after an account that does not fit, or cause them to drop one that does. With a live model this risk grows, because models can state wrong numbers confidently. This connects to the course theme of **over-reliance on AI**: the design should make checking the AI's work the natural path, not an optional extra.

**What I changed:** the user must confirm or reject every fact, with its source sentence directly above the buttons, before Copy unlocks. Edits that depart from the source are flagged and must be re-confirmed, the rating always reflects the values on screen, and the copied row records that it was reviewed and how many values were changed. This is working code, not a simulated safeguard; only the extraction itself is simulated.

**What risk remains:** a hurried user can click Confirm five times without reading, so the lock forces a decision but not careful reading. The quote check also cannot be fully tested yet: the prepared results always quote real sentences, so the check has never had to catch an invented quote from a real model. The risk test shows the lock and rating work; it does not show that users verify carefully.

## Remaining limitations

Ranked by effect on the central task:

1. **AI is simulated for four prepared documents only.** Other text gets a blank profile to fill in by hand, so the core time savings cannot be tested on real utilities yet.
2. **Prepared results are best-case output.** They show none of the errors a real model makes, such as wrong numbers or invented quotes, so the quote check is untested against real failures.
3. **Confirm can be rubber-stamped.** The review lock forces a decision on every fact but cannot ensure the user read the source.
4. **Members and meters share one field, and the rules read numbers from free text.** Unusual wording in an edit may not be parsed as a meter count.
5. **Nothing is saved.** Profiles disappear on refresh (by design for this slice).

## Next priorities

1. **Connect a live language model** and test it on 5 to 10 real public co-op documents, comparing its output to hand-checked answers and counting how often the quote check removes a fact.
2. **Split members and meters into separate fields**, so the size rule never treats a member count as a meter count.
3. **Test the review step with one or two researchers** to see whether they read the source sentences before confirming, and adjust the design if they do not.

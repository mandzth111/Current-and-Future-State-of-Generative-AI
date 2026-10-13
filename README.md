# Utility Account Qualifier

A web tool that turns public text about one electric utility into a draft account profile, where every fact links back to the sentence it came from, so a market-entry researcher can qualify an account in minutes instead of an hour.

## What the first working slice does

1. The user loads one of three sample documents (or pastes their own text) and clicks **Analyze**.
2. The app shows five fields: utility type, members or meters served, SCADA/OT ownership signals, named operations or IT leaders, and recent trigger events. Each field shows its source sentence, or "Not found."
3. The app rates fit against the target customer profile (Match, Partial, No match, or Not enough information) and shows the rule behind the rating.
4. The user edits or clears any field and clicks **Copy profile** to copy one tab-separated row for an account spreadsheet.

## How to open the prototype

- **Live prototype:** https://replit.com/@aschell3/Utility-Account-Qualifier-1
- **Or run it yourself:** open `index.html` in any browser. It is a single file with no dependencies, server, or API key.

## AI status: Wizard-of-Oz prototype

The product's AI behavior is **simulated**. No AI model or API is connected.

| Part | Status |
| --- | --- |
| Extracting the five fields with source quotes (the future AI task) | **Simulated, prepared by hand.** For each of the three sample documents, I wrote the result the future AI model should return and stored it in `index.html` (`PREPARED`). The app recognizes the sample and displays the result after a brief "Analyzing" pause. |
| Text that is not one of the samples | **Completed manually.** The app explains that it has no pre-filled results and shows a blank profile that the user fills in by hand. |
| Quote check: each field's quote must appear word for word in the pasted text | **Working** code. If a sample is edited so a quote no longer matches, that field is removed and flagged. |
| Fit rating against the target profile | **Working** code. This is deliberately rules-based, not AI. |
| Editing fields and copying the profile | **Working.** |

**What the future AI system is intended to do:** a language model will read unstructured public text (annual reports, board summaries, job postings) and extract the five fields, each with a supporting quote. AI suits this because utilities describe the same facts in many different ways that fixed keyword rules miss. The model will be told to report only what the text states, never to infer security weaknesses, and to keep members and meters separate. Its output stays an unverified draft the user reviews.

The three sample documents describe **fictional** utilities. No API keys, passwords, or private data are in this repository.

## Test results

Tested on October 13, 2026, in a browser at desktop and phone width.

| Test | Input or action | What happened | Result |
| --- | --- | --- | --- |
| Typical case | Co-op annual report sample (23,400 meters, own SCADA, two named leaders, board-approved cybersecurity assessment) | All five fields filled, each with its source sentence; both leaders shown with both quotes. Rated **Match** with the rule shown. Copy profile; put the reviewed row on the clipboard. | Pass |
| Challenge case | Member newsletter sample: an "Energy Co-op" with "roughly 18,000 members," no operations detail | Type shown as "likely electric," size as "about 18,000 members (meter count not stated)." SCADA, leaders, and triggers showed "Not found," with nothing invented. Rated **Not enough information**, naming meter count and SCADA as missing. | Pass |
| Invalid or empty case | Clicked Analyze with an empty box; then pasted an unrelated sentence about a soccer game | Empty: error message, no results, samples offered. Unrelated text: a note that only the samples have prepared results, a blank profile I could fill in and copy, rated **Not enough information**. No dead end. | Pass |

I also edited the sample report's meter count from 23,400 to 31,000 and re-ran it. The quote check removed the size field, flagged it, and the rating dropped to Partial.

## Known limitations

1. **The AI is simulated for three prepared documents only.** Any other text gets a blank profile to fill in by hand, so the core time savings cannot be tested on real utilities yet. Next, connect a language model using the API key stored in Replit Secrets and compare its output to these prepared results.
2. **The prepared results are best-case output.** I wrote them carefully, so they show none of the errors a real model makes, such as wrong numbers or invented quotes. Next: test the real model on the challenge cases and check how often the quote check has to remove a field.
3. **Single-line fields cut off long values, and nothing is saved.** Long trigger descriptions are hard to read and edit, and profiles disappear on refresh (by design for this slice). Next: use multi-line fields and add a session list of reviewed profiles.

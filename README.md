# Utility Account Qualifier

A web tool that turns public text about one electric utility into a draft account profile, where every fact links back to the sentence it came from, so a market-entry researcher can qualify an account in minutes instead of an hour.

**Intended user:** a market-entry researcher at a cybersecurity company qualifying small electric cooperatives in Indiana and Ohio as potential customers. Today, building one account row by hand from annual reports and news pages takes 30 to 60 minutes.

## Open the prototype

- **Live prototype (Replit):** [ADD PUBLISHED REPLIT LINK]
- **Backup link (GitHub Pages):** https://mandzth111.github.io/Current-and-Future-State-of-Generative-AI/
- **Or run it yourself:** download `index.html` and open it in any browser. It is a single file with no server, sign-in, or API key.

No sign-in is needed. Start by clicking **Sample: co-op annual report**, then **Analyze**.

## What the prototype does

1. The user loads one of four sample documents (or pastes their own text) and clicks **Analyze**.
2. The app shows five facts: utility type, members or meters served, SCADA/OT ownership signals, named operations or IT leaders, and recent trigger events. Each fact shows its source sentence, or "Not found."
3. The app rates fit against the target customer profile (Match, Partial, No match, or Not enough information) and shows the rule behind the rating. **The rating updates as the user edits.**
4. The user **confirms, edits, or rejects** each fact. Edited facts are flagged when they no longer match their source sentence.
5. **Copy profile** unlocks once every fact is reviewed. It copies one tab-separated row (five facts, fit rating, review note) for an account spreadsheet.

## AI status: Wizard-of-Oz prototype

The product's AI behavior is **simulated**. No AI model or API is connected.

| Part | Status |
| --- | --- |
| Extracting the five facts with source quotes (the future AI task) | **Simulated, prepared by hand.** For each of the four sample documents, I wrote the result the future AI model should return and stored it in `index.html` (`PREPARED`). The app recognizes the sample and shows the result after a brief "Analyzing" pause. |
| Text that is not one of the samples | **Completed manually.** The app says it has no prepared results and shows a blank profile the user fills in by hand. |
| Quote check: each quote must appear word for word in the pasted text | **Working** code. |
| Fit rating, recalculated from the values on screen | **Working** code. Deliberately rules-based, not AI. |
| Edit flags and the review lock on Copy | **Working** code. |
| Live language model that reads any public document | **Planned** for the final project. |

**What the AI will do:** a language model will read unstructured public text (annual reports, board summaries, job postings) and return the five facts, each with a supporting quote. AI suits this task because utilities describe the same facts in many ways that keyword rules miss; for example, the job-posting sample calls the co-op an "electric membership corporation" and never uses the word "cooperative." The model's output stays a draft that the user reviews before it is used.

## Revision documentation

**[revision.md](revision.md)** contains:

- Priority improvements and what changed
- Response to peer feedback
- Five test cases with success criteria and results
- Before-and-after comparison (screenshots in [`screenshots/`](screenshots/))
- What the evidence tells me
- Risk response
- Remaining limitations and next priorities

## AI-use disclosure

**[ai-use-disclosure.md](ai-use-disclosure.md)**

## Demo Video

**Draft demo (Google Drive):** [ADD GOOGLE DRIVE LINK]

Viewing access has been granted to Emelia Hughes and Samuel Huang.

## Files

- `index.html`: the complete prototype (HTML, CSS, and JavaScript in one file)
- `.replit`: the run configuration for Replit
- `revision.md`: revision documentation
- `ai-use-disclosure.md`: draft AI-use disclosure
- `screenshots/`: before-and-after images for the main revision

All four sample documents describe **fictional** utilities. No API keys, passwords, or private data are in this repository.

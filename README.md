# Take-Home Exercise — Equipment Rental

Thanks for taking the time to do this! You'll work with a **small app that already exists** — much like you would on the job. A few core functions are left unimplemented (they raise `NotImplementedError`) for you to fill in against the business rules described in `app.py`, and there are a couple of existing bugs to track down and fix.

It should take around **3–4 hours**. We don't expect everything to be perfect — we mostly want to see how you read unfamiliar code, reason about a spec, and track down a problem in code that isn't yours.

---

## The app

A simple tool for renting out equipment (cameras, drills, etc.). It has:

- `app.py` — a small Python (Flask) backend with the booking logic and a JSON API
- `index.html` — a one-page frontend (plain JavaScript) for making a booking
- `bookings.json` — where bookings are stored
- `requirements.txt`

## Prerequisites

You'll need **Python 3.10 or newer** installed. Check your version with:

```bash
python3 --version    # macOS / Linux
python --version     # Windows
```

If it prints something lower than 3.10, or the command isn't found, install Python first:

- **macOS** — download the installer from [python.org/downloads](https://www.python.org/downloads/), or if you use Homebrew: `brew install python`.
- **Windows** — download the installer from [python.org/downloads](https://www.python.org/downloads/) and, on the first screen, **tick "Add python.exe to PATH"** before clicking Install. (Alternatively: `winget install Python.Python.3.12`.)

No database or other tools are needed — just Python and a web browser.

---

## Running the app

We recommend using a virtual environment so the dependencies stay isolated.

**On macOS / Linux:**

```bash
# from inside the project folder
python3 -m venv venv          # create a virtual environment
source venv/bin/activate      # activate it (your prompt should now show "(venv)")
pip install -r requirements.txt
python app.py
```

**On Windows (PowerShell):**

```powershell
# from inside the project folder
python -m venv venv           # create a virtual environment
venv\Scripts\Activate.ps1     # activate it (your prompt should now show "(venv)")
pip install -r requirements.txt
python app.py
```

> If PowerShell blocks the activate script with an execution-policy error, run
> `Set-ExecutionPolicy -Scope Process -ExecutionPolicy Bypass` once in that window, then activate again.
> If you use the classic Command Prompt (cmd.exe) instead of PowerShell, activate with `venv\Scripts\activate.bat`.

Then open **http://localhost:5000** in your browser. Have a click around first to get a feel for it. The business rules are described in a comment at the top of `app.py`.

When you're done working, you can leave the virtual environment with `deactivate`.

---

## Your tasks

### 1. Implement booking-conflict detection
`dates_overlap`, `find_conflicting_booking`, and `rental_days` in `app.py` are left unimplemented (they currently `raise NotImplementedError`). Implement them against the business rules described in the comment at the top of `app.py` — including the same-day-turnover exception. *(The seed data in `bookings.json` gives you fixtures to test against — for example, there's a booking for the Canon DSLR Camera from Jan 10–15. Work out for yourself which nearby date ranges should and shouldn't be allowed, and test them.)*

### 2. Implement pricing
`calculate_total` in `app.py` is also unimplemented. Rentals are billed per the business rules at the top of the file — inclusive day counting, plus the long-rental discount. *(Pay close attention to the exact boundary of the discount rule, and test both sides of it.)*

### 3. Add a rule: no booking equipment under maintenance
Equipment can have a status of `maintenance` (the HD Projector is one). Right now it can still be booked and still shows up as available. **Add the rule that maintenance equipment cannot be booked**, and make sure it no longer appears as available. Think about all the places this rule needs to apply.

There's more than one reasonable way to handle this in the UI. Pick one and add a one-sentence justification for your choice to `NOTES.md` (see Task 5).

### 4. The frontend price bug
On the booking page, change the **start** date and the total updates. Change the **end** date and it... doesn't always. Find and fix it so the total stays correct.

Once you've added the 7-day discount from Task 2, double-check this page too: the total shown *before* booking should always match what the customer is actually charged *after* booking. Don't let the preview and the confirmed total drift apart.

### 5. A short write-up (`NOTES.md`)
Please include a `NOTES.md` with five quick things — keep it brief, no essays:

- **Explain one part of your solution.** Pick any one of the four tasks above and, in a few sentences, say how you approached it and why.
- **Show your conflict logic working.** Against the existing Jan 10–15 booking, give two concrete examples — just the dates — that your implementation correctly **blocks**, and one **legitimate same-day turnover** that it correctly **allows**. One line each is fine.
- **Your maintenance-equipment choice.** One sentence on whether you hid maintenance equipment entirely or showed it disabled, and why (Task 3).
- **One thing you'd flag in code review.** Name one pre-existing weakness or risk in this codebase *outside* the four tasks above — something you noticed while reading but weren't asked to fix. One or two sentences; **don't fix it.** (There are several. We'll probably chat about yours in the follow-up call.)
- **AI use (this won't count against you).** Tell us roughly what you used AI tools for, if anything — and, importantly, **how you checked that its output was correct.** Be specific: "I tested it" is less convincing than the actual dates, requests, or commands you tried. We use AI here every day; we're just looking for people who understand what they ship, not people who avoided the tools.

---

## What to send back

- The fixed code, as a git repo with at least **one commit per task or per function touched (as appropriate)** (Tasks 1-4 above, plus anything else you find and fix along the way). We read the commit history as part of the review, not just the final diff, so please write descriptive commit messages.
- Your `NOTES.md` (the five short items from Task 5).

Passing the assessment leads to a follow-up call. In that call, **we pick one of your fixes** (not you) and ask you to walk us through it — what the code does, why it's correct, what inputs would break it — and then we extend your submitted code together, live. Using AI to help you build this is completely fine; submitting code you can't explain is not. If you can navigate and defend every line of your own submission cold, the call will be easy.

Good luck, and thank you!

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
`dates_overlap`, `find_conflicting_booking`, and `rental_days` in `app.py` are left unimplemented (they currently `raise NotImplementedError`). Implement them against the business rules described in the comment at the top of `app.py` — including the same-day-turnover exception. *(There's already a booking for the Canon DSLR Camera from Jan 10–15 in the data — a good fixture to test against, e.g. an existing booking of Jan 10–15 should still permit a new booking of Jan 15–18 or Jan 6–10, but not Jan 8–12 or Jan 14–16.)*

### 2. Implement pricing
`calculate_total` in `app.py` is also unimplemented. Rentals are billed per the business rules at the top of the file — inclusive day counting, plus the long-rental discount. *(e.g. Jan 1–7 should come out discounted; Jan 1–6 shouldn't.)*

### 3. Add a rule: no booking equipment under maintenance
Equipment can have a status of `maintenance` (the HD Projector is one). Right now it can still be booked and still shows up as available. **Add the rule that maintenance equipment cannot be booked**, and make sure it no longer appears as available. Think about all the places this rule needs to apply.

There's more than one reasonable way to handle this in the UI — e.g. hide maintenance equipment from the list entirely, or show it disabled with a reason. Pick one and add a one-sentence justification for your choice to `NOTES.md` (see Task 5).

### 4. The frontend price bug
On the booking page, change the **start** date and the total updates. Change the **end** date and it... doesn't always. Find and fix it so the total stays correct.

Once you've added the 7-day discount from Task 2, double-check this page too: the total shown *before* booking should always match what the customer is actually charged *after* booking. Don't let the preview and the confirmed total drift apart.

### 5. A short write-up (`NOTES.md`)
Please include a `NOTES.md` with four quick things — keep it brief, no essays:

- **Explain one part of your solution.** Pick any one of the four tasks above and, in a few sentences, say how you approached it and why.
- **Show your conflict logic working.** Against the existing Jan 10–15 booking, give two concrete examples — just the dates — that your implementation correctly **blocks**, and one **legitimate same-day turnover** that it correctly **allows**. One line each is fine.
- **Your maintenance-equipment choice.** One sentence on whether you hid maintenance equipment entirely or showed it disabled, and why (Task 3).
- **AI use (this won't count against you).** Tell us roughly what you used AI tools for, if anything — and, importantly, **how you checked that its output was correct.** We use AI here every day; we're just looking for people who understand what they ship, not people who avoided the tools.

---

## What to send back

- The fixed code (a git repo — small commits with clear messages are appreciated).
- Your `NOTES.md` (the four short items from Task 5).

Passing the assessment leads to a follow-up call. We'll ask you to explain one of your fixes, then collaborate on adding a small feature, so approach each fix in a way you can clearly understand and discuss.

Good luck, and thank you!

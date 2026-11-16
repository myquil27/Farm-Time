# Gather the Party

A D&D session planner for John, Michael, Matt & Erin, Chris, and Ryan & Lynda.
Everyone opens a web link, enters the party code once, marks the days and times they
can play, and the page ranks the best days for the next session.

## What it does

- **My days**: pick your name, then tap days on a calendar to mark them **Can play**,
  **Maybe** or **Can't**, for the **afternoon** (about 1–5 pm), **evening** (about 6–10 pm)
  or both. Tap a weekday name (like *Sat*) to mark every one left in that month.
- **Best days**: the top six afternoons and evenings over the next four months, ranked by how
  many people can play, then maybes. Each gets a d20 "party roll"; a full party is a
  **Natural 20**. It also lists who hasn't answered yet.
- **Party calendar**: a month view showing how many people can make each afternoon and
  evening. Tap a day to see everyone's answers.
- **Schedule** a session from any of those: set the day, start time, where, and notes. It shows
  at the top of the page, and **Add to my calendar** downloads it for any calendar app.

Want to look around before it's set up? Open `index.html?demo` for made-up answers that are
saved only on your device.

## How it's built

| File | What it is |
| --- | --- |
| `index.html` | The whole website. |
| `config.js` | Your Firebase connection settings. The only file you edit. |
| `setup.html` | Owner-only helper: choose the party code and get the database rules for it. |
| `firestore.rules` | Rules template that `setup.html` fills in with your code. |

It works the same way as Farm Time: **Firebase Firestore** holds the answers, **GitHub Pages**
hosts the site, and nobody needs an account. The party code is turned into a long scrambled ID,
and the database rules only allow that one ID. It uses its **own Firebase project**, separate
from Farm Time. Each Firebase project has a single set of rules, so sharing one would let either
setup page overwrite the other's rules.

## One-time setup

### 1. Create a second Firebase database (about 5 minutes)

1. Go to <https://console.firebase.google.com> and click **Create a project**. Name it
   `gather-the-party` and turn off Google Analytics.
2. **Build → Firestore Database → Create database**, pick a location, choose
   **Start in production mode**, and click **Create**.
3. Gear icon → **Project settings** → **Your apps** → web icon `</>`. Name it
   `Gather the Party` and click **Register app**.
4. Copy the `firebaseConfig` values into [`config.js`](config.js) in this folder, then commit.

### 2. The website

Nothing extra to do. Once this folder is on the branch GitHub Pages serves (`main`), the site is at:

```
https://myquil27.github.io/Farm-Time/dnd/
```

### 3. Set the party code

1. Open `https://myquil27.github.io/Farm-Time/dnd/setup.html`.
2. Type the party code twice (at least 8 characters, e.g. `goblin tavern dice 20`).
3. Click **Make my database rules**, then **Copy rules**.
4. In the **Gather the Party** Firebase project (not Farm Time): **Firestore Database → Rules**,
   replace everything, click **Publish**.
5. Send the link and the code to the group. On a phone, **Share → Add to Home Screen** makes
   it open like an app.

## Good to know

- Anyone with the code can mark days for anyone in the party, so share it only with the group.
- To add or rename a player, edit the `PARTY` list near the top of the script in `index.html`
  **and** the player list in `firestore.rules`, then repeat step 3.
- Each person's answers from more than a month ago are tidied away automatically.

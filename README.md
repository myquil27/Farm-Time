# Farm Time

A shared family log for the farm: who's going up, when, and what for.
Family members open a web link, enter the family code once, and can see who's
at the farm today, browse upcoming visits on a list or calendar, and plan their own.

## How it's built

| File | What it is |
| --- | --- |
| `index.html` | The whole website (design, calendar, trip form). |
| `config.js` | Your Firebase connection settings. The only file you edit. |
| `firestore.rules` | Database rules that enforce the family code. Pasted into Firebase. |
| `farm-time.html` | The earlier claude.ai version (needs a Claude account). Not used by the website. |

Trips are stored in **Firebase Firestore** (Google's free database), and the site is
hosted for free on **GitHub Pages**. No one needs an account. The family code is turned
into a long scrambled ID that names your family's folder in the database. The database
refuses to list folders, so without the code there is no way to find your trips.

The page also keeps a copy on each phone, so it opens and accepts new trips even with
weak signal at the farm. Changes sync when the signal comes back.

## One-time setup

### 1. Create the Firebase database (about 5 minutes)

1. Go to <https://console.firebase.google.com> and sign in with any Google account.
2. Click **Create a project**, name it `farm-time`, and turn off Google Analytics (not needed).
3. In the left menu open **Build → Firestore Database → Create database**.
   Pick a location near you, choose **Start in production mode**, and click **Create**.
4. Open the **Rules** tab, delete what's there, paste the entire contents of
   [`firestore.rules`](firestore.rules), and click **Publish**.
5. Click the gear icon → **Project settings**. Under **Your apps**, click the web icon `</>`,
   name it `Farm Time` (leave "Firebase Hosting" unchecked), and click **Register app**.
6. Copy the values from the `firebaseConfig` block it shows (`apiKey`, `authDomain`,
   `projectId`, `storageBucket`, `messagingSenderId`, `appId`) into [`config.js`](config.js).
   These values are not secret; they only say which database to talk to.

### 2. Put the site online with GitHub Pages

GitHub Pages is free for **public** repositories. A private repository needs a paid
GitHub plan for Pages. The code contains no passwords or trip data, so making it
public is safe: **Settings → General → Danger Zone → Change visibility → Public**.

Then: **Settings → Pages → Build and deployment → Source: Deploy from a branch**,
choose the branch with these files (`main` once merged) and `/ (root)`, and click **Save**.
After a minute or two the site is live at:

```
https://myquil27.github.io/Farm-Time/
```

### 3. Start your family log

1. Open the site and type a family code that's hard to guess, at least 8 characters.
   Three words and a number works well, for example `rusty tractor creek 52`.
2. Click **Open the log**, then **Start a new family log**.
3. Send the link and the code to your family. Capital letters and extra spaces in the
   code don't matter. Each person enters it once per phone or computer. On a phone,
   **Share → Add to Home Screen** makes it open like an app.

## Good to know

- Anyone with the code can add, change, or delete trips. If the code gets out, start a
  new log with a new code and share that instead (trips don't move over automatically).
- "Use a different family code" at the bottom of the page signs that device out of the log.
- Firebase's free plan allows 50,000 reads and 20,000 writes per day, far more than a family needs.

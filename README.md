# WPS Clue

The companion website for our school's Clue week, *What Did the Butler See?*

- **Public site:** a radio-show masthead with a five-day broadcast dial, the evidence board, a case log of every clue and witness statement, a hall of fame, and the class answer sheet. Teachers submit answers right on the page with no account needed.
- **Producer desk:** sign in with Google to release each broadcast after it airs, score answer sheets (closest tiebreaker sorts to the top), crown winners, play sound effects from a soundboard, and set up photos and posters.

Answers and unreleased clues are never in this repo. They live in Firestore and only producers can read them.

## Files

| File | Goes in the repo? | What it is |
|---|---|---|
| `index.html` | Yes | The whole site |
| `logo.jpg`, `favicon.ico`, `favicon-32.png`, `icon-192.png`, `apple-touch-icon.png` | Yes | Winchester Clue logo and browser icons. Keep them next to `index.html`. |
| `firestore.rules` | Yes (reference) | Security rules to paste into Firebase |
| `.gitignore` | Yes | Keeps the case file out of the repo |
| `clue-casefile.json` | **No** | Clue wording and the answer key. Load it from the producer desk. |

## Setup (about 15 minutes)

### 1. Create a Firebase project
1. Go to [console.firebase.google.com](https://console.firebase.google.com) and add a project (for example `wps-clue`). Google Analytics is not needed.
2. **Build > Firestore Database > Create database.** Choose production mode and a Canadian region (`northamerica-northeast1`, Montréal).
3. **Build > Authentication > Get started > Sign-in method > Google > Enable.**
4. **Authentication > Settings > Authorized domains > Add domain:** add your GitHub Pages domain (for example `yourname.github.io`).

### 2. Paste the security rules
**Firestore Database > Rules:** replace everything with the contents of `firestore.rules`, then **Publish**.

### 3. Make yourself a producer
**Firestore Database > Data > Start collection:**
- Collection ID: `producers`
- Document ID: the Google email you'll sign in with (for example `you@gmail.com`)
- Add any field, such as `name` = your name, then Save.

Add one document per extra producer (the principal, for example).

### 4. Connect the site
**Project settings (gear icon) > Your apps > Web (`</>`)**: register an app, then copy the `firebaseConfig` object. Paste it over the placeholder at the top of the `<script type="module">` in `index.html`. The web config is not a secret.

### 5. Publish on GitHub Pages
Commit `index.html`, the logo and icon files, `firestore.rules`, `README.md` and `.gitignore`. In the repo, go to **Settings > Pages**, set the source to your branch, and save.

### 6. Load the case file
Open the site, click **Producer sign-in** in the footer, and sign in. Open **Producer desk > Setup** and choose `clue-casefile.json`. Then fill in the school name, the Day 1 date and the announcement times, and add photos of your four suspects and four locations.

Upload the two picture puzzles (the off-and-ice poster for the Office, and the staff-and-broom poster for the Staffroom) under **Picture puzzles**. They stay hidden until you release that morning's broadcast.

## During the week
- **Run of show** lists every broadcast with its scheduled time and a daily to-do list. Release each broadcast once it has aired. Anything past its time shows as **Due**.
- **Answers and winners** sorts each day's answers, with correct answers first and the closest tiebreaker first. Click **Crown** to announce a winner on the site. Type in paper sheets here too.
- **Episode videos**: upload each recording to Google Drive, share it as "anyone in Durham DSB with the link can view", and paste the link into that broadcast's box in **Run of show**. The video stays hidden until you release the broadcast, then plays right in the case log. YouTube (unlisted) links work too.
- **Soundboard**: load the sound-effect files once from your download page, then play them with keys 1 to 6. The files stay in that computer's browser.
- Tiebreakers are secret numbers only you know. Enter them in **Setup > Secret settings**: make up the Day 2 teacup seconds, count your steps from the front doors to the library for Day 3, and on Day 3 time 3 laps of the front foyer for Day 4. Any correct class can be crowned, so you can spread the wins around.
- To practise first, release a few broadcasts, then use **Rehearsal reset** at the bottom of Run of show.

Answer sheets close automatically when you release that day's answers, so late entries can't come in after the reveal.

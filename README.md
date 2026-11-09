# Score Board

A score tracker for game nights that runs in your browser. It's a single HTML file with no install, no account and no server.

It has two modes:

- **Screw**: built for the card game Screw (SKRU). It handles the SKRU caller penalty, the double-score final round and who goes first each round.
- **Normal Game**: for dominoes, card games or anything where you add up points every round. There's no round limit; you end the game when you're done.

Your game is **saved automatically after every change** (even scores you've typed but not confirmed). If the page is refreshed, the browser closes or you lose internet, open the page again and tap **Resume**.

---

## Using it

1. Open the page and pick **Screw** or **Normal Game**.
2. Enter a game name and the players (2–10).
3. Enter each player's score every round and confirm.
4. Use **Undo / Redo** to fix mistakes, and **TXT / JSON** to download the scoreboard.

### Normal Game

- Type each player's points for the round and tap **Add Round** (or press Enter through the boxes).
- A blank box counts as 0. Negative and decimal numbers are allowed.
- The Total column is the running sum of every round.
- Tap **End Game** to see final totals. **Keep Playing** reopens the game if you ended it too early.

### Screw rules (as scored by the app)

- The game is **5 rounds**. The **lowest total wins**.
- Each round, select **who called SKRU** (required).
- If the SKRU caller **did not** have the lowest score that round, their score is **doubled**.
- After penalties, the **lowest score in the round becomes 0**.
- **Round 5 is a double round**: every score is ×2 and the SKRU penalty is ×4 instead of ×2. The lowest still becomes 0.
- **Who starts:** in round 1 the app picks a random player. After that, the lowest scorer of the previous round starts. If there's a tie and the SKRU caller is one of the tied players, the SKRU caller starts. Otherwise the app picks at random among the tied players.
- **Skip** moves to the next round without recording scores.

---

## Saving and resuming

| Where | What's stored | Why |
| --- | --- | --- |
| `localStorage` | Full game, typed-but-unconfirmed scores, undo/redo history | Main save, no size worries |
| Cookies (`sb_session_*`, `sb_last`) | Full game and typed scores | Backup copy in case local storage is cleared or blocked |

- Both are written on every change. When the page opens, it uses whichever copy is newest.
- Everything stays **in your browser on your device**. Nothing is uploaded anywhere, and no analytics or tracking are used. The only network request is for the Google Fonts.
- Saves belong to one browser on one device. To move a game to another phone or computer, use **⬇ JSON**, then **Restore a game from a saved .json file** on the start screen of the other device.
- Private/incognito windows forget everything when closed.
- Cookies don't work when the file is opened straight from disk (`file://`) in some browsers. The `localStorage` save still works there, and both work when the page is hosted (for example on GitHub Pages).
- Save files from the older **SKRU v3** tracker are picked up automatically as Screw games.

---

## Hosting it on GitHub Pages

1. Create a new **public** repository on GitHub and upload `index.html`, `README.md` and `LICENSE` (or push them with git).
2. In the repository, go to **Settings → Pages**.
3. Under **Build and deployment**, choose **Deploy from a branch**, pick `main` and `/ (root)`, then click **Save**.
4. After a minute your site is live at `https://<your-username>.github.io/<repo-name>/`.

To run it locally, just open `index.html` in a browser. To test the cookie save too, serve the folder instead, for example:

```bash
python -m http.server 8000
# then open http://localhost:8000
```

---

## Project files

| File | Purpose |
| --- | --- |
| `index.html` | The whole app (HTML, CSS and JavaScript in one file) |
| `README.md` | This file |
| `LICENSE` | MIT licence |

---

## License

Released under the [MIT License](LICENSE). You're free to use, copy, change and share this code, including commercially, **as long as you keep the copyright notice and licence text** (that's the attribution).

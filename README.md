# Shelf

A private book tracker that runs in your phone's browser. No account is needed to use it, and there is nothing to pay for.

Live version: https://annoyingkay.github.io/Shelf/

## What it does

- Keeps a library of books with status (want to read, reading, finished), reading dates, rereads, ratings, reviews, notes and quotes.
- Adds books by scanning the barcode, searching online (Open Library) or typing them in.
- Records format, pages, series, tags, edition, physical release date, copies owned, date of purchase and price paid.
- Marks books "On repeat" for children's books or favourites read again and again. These are kept out of goals, stats and trophies.
- Shows reading stats for a year or for all years, with the list of books read, books read more than once, a reading goal, and a list of finished books that have no finish date. A second Library view covers everything collected: status, ownership, formats, genres, languages, authors, series, who added each book, repeated titles and missing details. A finished book needs a finish date to count towards stats, goals and trophies. Trophies already earned are kept.
- Awards ranks and trophies, with a bell for notices. Ranks come from books finished with a finish date. Library trophies count what you add, rate and review. Finish trophies need a finish date. Each of Kay's favourite books has a sticker, kept in its own Stickers tab inside Trophies. Stickers do not count towards ranks.
- Shows four library views (list, compact, grid small, grid big), and a Genre filter.
- Marks books you may or may not still own: an ownership note, the source a book came from, and a To confirm filter.
- Fills in covers, pages, ISBN and genres online for the whole library in one pass. A full match on title, author and language is applied. Everything else, and every comic and manga, asks you first. Typed details are never overwritten.
- Offers themes. Some are open from the start and the rest unlock as you read, depending on what you read. Hallowe'en and Yule stay unlocked once earned.
- Seasonal themes unlock by opening Shelf during their month and stay unlocked once earned: Sobremesa (October), St Brigid and St Valentine (February), St Patrick (March), as well as Hallowe'en and Yuletide.
- Shows a small daily greeting on the Library page, once a day and once across your devices. Most days in the current batch carry a small original drawing and a dry line about the date, and quiet days get a plain greeting.
- One bell for notices, split into Activity (trophies, ranks, titles, themes, households) and News (welcome and update notes), each type with its own fixed icon.
- Imports from Goodreads CSV and exports a CSV or a JSON backup.
- Works offline once installed, and can be added to the home screen.

## Where your data lives

Everything is stored on your device first. Sync is optional.

If you switch on sync, books, goals, trophies, titles and notices are stored in your own account in Firebase (Firestore) and kept in step across your devices. Each person sees only their own data, apart from a shared household library described below.

## Households

A household lets partners, family or friends share one library.

- Anyone with a verified email can start a household and invite others by email. A person can be in one household. The limit is eight people.
- Everyone can add or scan books. Titles, authors, covers, tags, formats, editions and release dates are shared.
- Status, dates, ratings, reviews, notes, copies, purchase dates, trophies, stats and themes stay personal.
- A shared book counts towards your trophies, stats and theme unlocks only once you add your own status, dates or rating. Joining an existing library does not unlock a pile of trophies.
- Deleting a shared book removes it for everyone, after a confirmation.
- Leaving keeps the books you have used as private books and removes the shared ones you never touched.
- Each household has a name. Members see each other's cards: nickname, rank, title, trophy count and a card colour taken from the themes. Each person can pick their colours or hide everything except their nickname.
- Adding a book that is already in the library asks whether it is a repeat entry or should be cancelled.
- Each book remembers who added it. Existing books use the best record available, so older ones can be a best guess.
- A Goodreads import adds your own status, rating and dates to shared books you have not marked yet.

## Files

| File | Purpose |
| --- | --- |
| `index.html` | The whole app: markup, styles and script. |
| `sw.js` | Service worker for offline use. The cache name changes with each release. |
| `firebase-config.js` | Your Firebase project settings. Only needed for sync. Not replaced when updating. |

## Daily greetings

The greetings, drawings and `DOODLE_END` date live near the end of the script in `index.html`. Each batch covers about two months. A weekly GitHub workflow (`.github/workflows/doodle-reminder.yml`) reads `DOODLE_END` and opens an issue when fewer than 14 days remain. Add the next batch, change the `DOODLE_END` date, upload `index.html`, then close the issue.

## Updating

1. Replace `index.html` and `sw.js` in the repository. Leave `firebase-config.js` alone.
2. Wait a minute for GitHub Pages to publish.
3. Open the app and reload it once or twice so the new service worker takes over.

Export a backup from Settings before a big update.

## Setting up sync (optional)

1. Create a Firebase project on the free Spark plan.
2. Under Authentication, turn on Email/Password and Google sign in.
3. Under Firestore Database, create a database and paste the contents of `firestore.rules` from the Libraries repository into the Rules tab. Replace the owner ID in the rules with your own account ID, which Settings shows under Advanced.
4. Add your site to Authentication, Settings, Authorised domains (for example `annoyingkay.github.io`).
5. In Google Cloud, under Credentials:
   - On the API key, add website restrictions for your GitHub Pages address and for `your-project.firebaseapp.com/*` and `your-project.web.app/*`.
   - On the OAuth web client, add your GitHub Pages origin under Authorised JavaScript origins.
6. Put your Firebase settings in `firebase-config.js` and export your owner ID from the same file.

The Firebase API key is public by design. Access is controlled by the security rules and the restrictions above, not by hiding the key.

## Privacy

There is no tracking and no advertising. Book lookups go to Open Library and Google Books. Cover images are loaded from the address stored on each book. If sync is off, nothing leaves your device apart from those requests.

## Notes

- The console style themes and the Crystal Chronicle theme are original designs. They are not affiliated with any game maker.
- Tested in recent Chrome and Edge. Barcode scanning needs a browser that supports it and a camera.

## Version history

Each release adds a line here. The version number shows at the bottom of Settings.

| Version | What changed |
| --- | --- |
| 60 | Author autocomplete on the book form: type in the Author box and a dropdown lists authors already in your library (accent insensitive), most recently read first, with a switch to A to Z that is remembered. |
| 59 | Add or fill a book from an Amazon link. The product code (ASIN) is read from the link. Paperback and hardback codes are ISBN-10 and are looked up in Open Library and Google Books. Kindle codes are tried in Open Library; if unknown, the link is saved on the book. Year fills the release date when blank. |
| 58 | Household bookcase: book titles are larger and easier to read on the spines, and each member gets their own shelf. |
| 57 | Time flairs for every theme (one hour in a theme unlocks its flair). New library trophies: Proper Collection (books owned), Series Collector, Quarter Century, Century Shelf, Five Hundred Deep, plus Collector and Shelf Stacker flairs. Household page has a bookcase: each member picks five books, shown as unique decorated spines. |
| 56 | More cats on Cosy Cat (header, cards, peeking cat on the tab bar, patterned background). Meadow redrawn as a Ghibli inspired hillside scene. New original Storybook fairy tale theme with its own ranks and trophy. Time flairs: spend 10 hours in Cosy Cat, Meadow or Storybook to unlock Cat Whisperer, Hilltop Dweller or Happily Ever After. |
| 55 | Price paid and currency on each book, next to date of purchase. Library stats show what you spent. A JSON import adds purchase details to books already on the shelf. |
| 54 | Owner tools can give several flairs and themes at once. Reading stats gain an All years button, a list of books read for the chosen period and a Read more than once list. Library stats show who added each book and repeated titles. Books remember who added them. |
| 53 | Trophies reinstated: library trophies (Moving In, Shelf Builder, Fair Critic, Pen Pal and more) and finish trophies that need a finish date. Announcement and a trophy count notice. |
| 52 | Stats has a Library view next to Reading. |
| 51 | A Google sign in counts as verified for households. Household section shows the verify buttons. |
| 50 | Household actions say what happened or why nothing did. A stuck busy flag clears itself. |
| 49 | Fixed the Join household button, which read the wrong data and did nothing. |
| 48 | Goodreads import fills in your own data on shared books you have not marked yet. |
| 47 | Stickers replace the Kay's Favourites trophies. A Stickers tab sits inside Trophies and stickers appear on household cards. |
| 46 | Online pass for covers and details, with confirmation for comics and manga. Genre filter in the library. |
| 45 | Ownership notes and sources, To confirm filter, JSON import skips books already in the library. |
| 44 | Settings reorganised: sync card with backup, goal in Profile, Advanced box. Four library views. Service worker cache fix. |
| 43 | The First One trophy only counts books with a finish date. |
| 41 | Welcome only notice for new users after registering, a nudge to register when adding books without an account. |
| 40 | Ranks come from books finished with a finish date. Milestone trophy for every rank. Generic trophies removed (reinstated in 53). |

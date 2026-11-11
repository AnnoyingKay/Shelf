Welcome to by Shelf trial!

Shelf

A private book tracker that runs in your phone's browser. No account is needed to use it, and there is nothing to pay for.

Live version: https://annoyingkay.github.io/Shelf/

What it does
Keeps a library of books with status (want to read, reading, finished), reading dates, rereads, ratings, reviews, notes and quotes.
Adds books by scanning the barcode, searching online (Open Library) or typing them in.
Records format, pages, series, tags, edition, physical release date, copies owned and date of purchase.
Marks books "On repeat" for children's books or favourites read again and again. These are kept out of goals, stats and trophies.
Shows yearly and monthly stats, a reading goal, and a list of finished books that have no finish date.
Awards trophies and ranks, with a bell for notices.
Offers themes. Some are open from the start and the rest unlock as you read, depending on what you read. Hallowe'en and Yule stay unlocked once earned.
Imports from Goodreads CSV and exports a CSV or a JSON backup.
Works offline once installed, and can be added to the home screen.
Where your data lives

Everything is stored on your device first. Sync is optional.

If you switch on sync, books, goals, trophies, titles and notices are stored in your own account in Firebase (Firestore) and kept in step across your devices. Each person sees only their own data, apart from a shared household library described below.

Households

A household lets partners, family or friends share one library.

Anyone with a verified email can start a household and invite others by email. A person can be in one household. The limit is eight people.
Everyone can add or scan books. Titles, authors, covers, tags, formats, editions and release dates are shared.
Status, dates, ratings, reviews, notes, copies, purchase dates, trophies, stats and themes stay personal.
A shared book counts towards your trophies, stats and theme unlocks only once you add your own status, dates or rating. Joining an existing library does not unlock a pile of trophies.
Deleting a shared book removes it for everyone, after a confirmation.
Leaving keeps the books you have used as private books and removes the shared ones you never touched.
Adding a book that is already in the library asks whether it is a repeat entry or should be cancelled.
Files
File	Purpose
index.html	The whole app: markup, styles and script.
sw.js	Service worker for offline use. The cache name changes with each release.
firebase-config.js	Your Firebase project settings. Only needed for sync. Not replaced when updating.
firestore.rules	Security rules to paste into Firestore.
Updating
Replace index.html and sw.js in the repository. Leave firebase-config.js alone.
Wait a minute for GitHub Pages to publish.
Open the app and reload it once or twice so the new service worker takes over.

Export a backup from Settings before a big update.

Setting up sync (optional)
Create a Firebase project on the free Spark plan.
Under Authentication, turn on Email/Password and Google sign in.
Under Firestore Database, create a database and paste the contents of firestore.rules into the Rules tab. Replace the owner ID in the rules with your own account ID, which Settings shows under Account ID.
Add your site to Authentication, Settings, Authorised domains (for example annoyingkay.github.io).
In Google Cloud, under Credentials:
On the API key, add website restrictions for your GitHub Pages address and for your-project.firebaseapp.com/* and your-project.web.app/*.
On the OAuth web client, add your GitHub Pages origin under Authorised JavaScript origins.
Put your Firebase settings in firebase-config.js and export your owner ID from the same file.

The Firebase API key is public by design. Access is controlled by the security rules and the restrictions above, not by hiding the key.

Privacy

There is no tracking and no advertising. Book lookups go to Open Library. Cover images are loaded from the address stored on each book. If sync is off, nothing leaves your device apart from those requests.

Notes
The console style themes and the Crystal Chronicle theme are original designs. They are not affiliated with any game maker.
Tested in recent Chrome and Edge. Barcode scanning needs a browser that supports it and a camera.

# Balance sheet: setup guide

This is your balance sheet as a standalone app. It installs on your phone and computer, works offline, and syncs through your own free Firebase account. One-time setup takes about 15 minutes.

Files in this folder:

- `index.html`: the app
- `firebase-config.js`: your Firebase settings (you fill this in, step 2)
- `manifest.webmanifest`, `sw.js`, `icons/`: what makes it installable and work offline
- `firestore.rules`: security rules so only you can read your data

## Step 0: Save your current data

Open your current balance sheet in Claude, go to **Settings → Download backup**, and keep the `.json` file. You'll restore it in step 4.

## Step 1: Put the app online (GitHub Pages, free)

1. Sign in at github.com (create a free account if needed).
2. Click **+ → New repository**. Name it `balance-sheet`, set it to **Public** (required for free Pages; your data is not in the repo, only the app code), and click **Create repository**.
3. Click **uploading an existing file** and drag in everything from this folder, including the `icons` folder. Click **Commit changes**.
4. Go to **Settings → Pages**. Under **Branch**, choose `main` and `/ (root)`, then **Save**.
5. After a minute, your app is at `https://YOUR-USERNAME.github.io/balance-sheet/`.

## Step 2: Create your Firebase project (free)

1. Go to console.firebase.google.com and sign in with your Google account.
2. Click **Create a project**, name it (for example `balance-sheet`), and turn **off** Google Analytics. Create it.
3. **Sign-in:** go to **Build → Authentication → Get started → Google**, switch it **on**, pick your email as the support email, and **Save**.
4. **Allow your site:** in **Authentication → Settings → Authorized domains**, click **Add domain** and add `YOUR-USERNAME.github.io`.
5. **Database:** go to **Build → Firestore Database → Create database**. Choose a location close to you (for Pakistan, `asia-south1 (Mumbai)` is closest) and **production mode**.
6. **Security rules:** in Firestore, open the **Rules** tab, replace everything with the contents of `firestore.rules`, and click **Publish**.
7. **Get your config:** click the gear icon → **Project settings**. Under **Your apps**, click the web icon `</>`, give it a nickname, and click **Register app** (skip Hosting). Copy the values inside `firebaseConfig = { ... }`.

## Step 3: Connect the app to Firebase

1. In your GitHub repo, open `firebase-config.js` and click the pencil icon to edit.
2. Replace the placeholder values with the ones you copied in step 2.7.
3. Click **Commit changes**. Wait a minute for GitHub Pages to update.

The API key in this file is not a password. It only identifies your project. Your data is protected by Google sign-in and the rules from step 2.6.

## Step 4: Sign in and restore your data

1. Open `https://YOUR-USERNAME.github.io/balance-sheet/` and click **Sign in with Google**.
2. Go to **Settings → Restore from backup** and pick the file from step 0.
3. Your months, bills, debts and sections are back, and now sync across devices.

## Step 5: Install it

- **Computer (Chrome or Edge):** click **Install app** in the app's header, or the install icon in the address bar.
- **Android (Chrome):** tap **Install app** in the header, or ⋮ → **Install app**.
- **iPhone (Safari):** tap Share → **Add to Home Screen**.

Sign in with the same Google account on each device.

## Good to know

- **Offline:** the app opens and saves without internet. Changes sync automatically when you're back online, and the status at the top shows "Saved offline" until then.
- **Updates:** if you change the app files later, edit `sw.js` and change `balance-sheet-v1` to `balance-sheet-v2` so phones pick up the new version.
- **Backups:** Settings → Download backup still works. Keep one every few months.
- **Cost:** a personal app like this stays well within Firebase's free plan.

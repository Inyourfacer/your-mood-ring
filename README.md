# your-mood-ring

A private daily mental and physical health check-in that runs entirely on GitHub. It's free, there's no server, and no computer has to stay on.

- **A home-screen app** on your phone with a one-minute check-in (mood, stress, energy, sleep, exercise, habits, notes) and a dashboard of trends.
- **A daily reminder** sometime in the evening window you choose, only if you haven't checked in yet.
- **Encrypted with your passphrase** on your device before anything is uploaded. Your repo is public, but it only ever holds scrambled data that only you can unlock.

This is a template. Each person makes their own copy, and their data lives in their own repo.

## Set up your own copy (about 15 minutes)

You need a GitHub account and an iPhone on iOS 16.4 or newer. Android and desktop browsers work too.

**1. Make your copy**
1. Click **Use this template → Create a new repository** at the top of this page.
2. Give it any name, choose **Public**, and click **Create repository**.

**2. Turn on the website**
- In your new repo, go to **Settings → Pages**. Set Source to **Deploy from a branch**, Branch to **main** and **/ (root)**, and click **Save**.
- After a minute or two, your app is at `https://<your-username>.github.io/<repo-name>/`.

**3. Set it up on a computer.** Open `https://<your-username>.github.io/<repo-name>/setup.html` and do:
1. **Token:** create a fine-grained token for *just this repo* with **Contents: Read and write**, then paste it in.
2. **Passphrase:** choose four or more random words. Save them in a password manager first. **If you lose the passphrase, your data can't be recovered.**
3. **Schedule:** your time zone is filled in for you. Pick your reminder window.
4. **Notification keys:** click **Generate keys**, copy the private key, and add it as a repo secret named `VAPID_PRIVATE_KEY` (Settings → Secrets and variables → Actions).

**4. Set it up on your iPhone**
1. In **Safari**, open your app's address. Tap **Share → Add to Home Screen**.
2. Open the app **from the Home Screen** (not Safari) and tap **⚙**.
3. **Step 1:** the phone needs its own token. Make one in Safari by typing `github.com/settings/personal-access-tokens/new`. The GitHub app can't make tokens.
4. **Step 2:** enter your passphrase. **Step 5:** tap **Turn on notifications**, then **Allow**.

**5. Test it.** Go to **Actions → Daily reminder → Run workflow**. A notification should arrive within a minute or two.

## What's public and what isn't

| Public | Private |
|---|---|
| The code and the question list in `config.json` | Every answer and note (encrypted with AES-256-GCM) |
| Your time zone and reminder window | Your passphrase, which is never stored or uploaded |
| Which days you checked in (commit messages "Check-in for YYYY-MM-DD") | The `VAPID_PRIVATE_KEY` repo secret |
| Your devices' push addresses (useless without the private key) | Your GitHub tokens, which stay on each device |

## Customizing

- **Questions:** edit `config.json`. Types are `scale`, `number`, `tags`, `yesno` and `text`. Keep each `id` the same once it has data. Add `"lower_is_better": true` for measures like stress so the dashboard's better/worse labels read correctly.
- **Reminder window:** change it on the Setup page.
- **Timing:** GitHub runs scheduled jobs irregularly, so the reminder comes at the first run inside your window, not at an exact time. A window of about five hours is the most dependable. A day can still be missed if no run lands in the window. The frequent short runs on the Actions tab are normal.

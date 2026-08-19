# Presentations — Team meeting SPA

Single-file meeting agenda & realtime mini-app for quick team sessions.

- Live demo: https://presentations-558b1.web.app
- Firebase project: `presentations-558b1`

Files included

- `post_summer_fun_team_meeting_7ppl_60min.html` — single-file SPA (agenda, timer, challenge cards, vibes) with Firebase Realtime Database sync and Google sign-in UI.
- `database.rules.json` — Realtime Database rules (reads open, writes require authentication for `vibes` and `challenge`).

Quick notes

- The app uses Firebase compat SDKs (v9.22.0) and signs users in anonymously by default. Google Sign-In button is available for authenticated actions.
- To allow users to sign in with Google, enable the Google provider in Firebase Console → Build → Authentication → Sign-in method.
- Admin controls: the UI checks for the admin email `barzegar.sima.barzegar@gmail.com` and for UIDs listed under `/admins`. You can add admin UIDs to `/admins/<uid> = true` via the Firebase Console or REST/CLI.

Deploying

1. Install `firebase-tools` and login:

```bash
npm install -g firebase-tools
firebase login
```

2. Deploy hosting and database rules (from this repo root):

```bash
firebase deploy --only hosting,database --project presentations-558b1
```

CI / Auto-deploy with GitHub Actions

This repository includes a GitHub Actions workflow at `.github/workflows/firebase-deploy.yml` that deploys `hosting` on every push to `main`.

Before the workflow can deploy, add a repository secret named `FIREBASE_TOKEN` containing a CI token generated from the Firebase CLI:

```bash
# on your machine, authenticated with the same Firebase account
firebase login:ci
# copy the token printed by the command and add it as the repo secret
```

To add the secret:

1. Go to your GitHub repository → Settings → Secrets & variables → Actions → New repository secret
2. Name: `FIREBASE_TOKEN`
3. Value: paste the token from `firebase login:ci` and save

After that, pushes to `main` will automatically deploy the `presentations-558b1` hosting site.

Security

- Current DB rules allow authenticated users to write `vibes` and `challenge`.
- If you want only admins to write, revert `database.rules.json` to restrict writes to `root.child('admins').child(auth.uid).val() === true` (or to specific email checks) and redeploy rules.

If you want, I can also configure the workflow to use a service-account `FIREBASE_SERVICE_ACCOUNT` JSON secret instead (recommended for multi-user CI). Just say which you prefer and I will update the workflow and README accordingly.

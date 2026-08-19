# Post-summer Team Meeting (7 ppl, 60 min)

A lightweight, in-person agenda and interactive page to run a 60-minute team kickoff after summer.

What’s included
- `post_summer_fun_team_meeting_7ppl_60min.html`: single-file HTML with styles and small JS to run a timed agenda, pick a challenge, and collect team "vibes".

Quick start
1. Open the file in your browser (double-click or right-click → Open with → your browser).
2. Click **Start** to run the 60-minute timer. Use the phase headers to expand/collapse sections.
3. Interact with the challenge cards and vibe buttons during the meeting.

Notes
- The file is self-contained; no server is required.
- If you want this on GitHub Pages, you can push the file to a repository and enable Pages for the branch.

Auto-deploy (secure)

This repository includes a GitHub Actions workflow that deploys the Firebase Hosting site on push to `main`. For secure CI deploys we prefer a service-account JSON secret instead of a long-lived CLI token.

Create and add the secret:

1. In the Firebase Console → Project Settings → Service accounts, create a new service account or use the existing one. Grant it the **Editor** role for the project (or narrower roles if you prefer).
2. Generate a new private key (JSON) and save the JSON content.
3. In GitHub, go to your repository → Settings → Secrets & variables → Actions → New repository secret.
   - Name: `FIREBASE_SERVICE_ACCOUNT`
   - Value: paste the full JSON content and save.

The workflow writes the secret to `firebase-service-account.json` during the run and sets `GOOGLE_APPLICATION_CREDENTIALS` so the Firebase CLI can authenticate using the service account.

If you prefer using `firebase login:ci` tokens instead, the older workflow still works with a secret named `FIREBASE_TOKEN`.

Contact
- File edited and maintained by the repository owner.

License
- Use freely within your organization. No license file included — add one if you need a specific open-source license.

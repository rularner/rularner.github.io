# rularner.github.io

This repo backs `https://rularner.github.io/` and hosts the static files needed
for the SF Transit Watch app's Universal Link flow ("tap a link to register
your 511 API key").

## What each file does

- `apple-app-site-association` — the Apple App Site Association (AASA) file.
  Tells iOS/watchOS that `rularner.github.io` is authorized to hand URLs to
  the SF Transit Watch watch app. Served at the domain root with
  `Content-Type: application/json` (GitHub Pages does this automatically for
  a file named without an extension).
- `sftransitwatch/key/index.html` — a friendly fallback page for anyone who
  lands on `https://rularner.github.io/sftransitwatch/key?k=…` without the
  universal link triggering (e.g. tapping it on a Mac, or before the device
  has fetched the AASA file). On a watch with the app installed, this HTML
  is never seen — watchOS opens the app directly.

## Verifying the deployment

1. `curl -i https://rularner.github.io/apple-app-site-association`
   - Expect HTTP 200 and `Content-Type: application/json`.
2. Install a build of the watch app that includes the Associated Domains
   entitlement (`applinks:rularner.github.io`).
3. Send yourself a Messages link in this form (replace `TEST_KEY` with any
   non-empty token):

   ```
   https://rularner.github.io/sftransitwatch/key?k=TEST_KEY
   ```

4. Open the message on your Apple Watch and tap the link. The watch app
   should open and save `TEST_KEY`.

## If it isn't working

- watchOS caches AASA aggressively. Delete and reinstall the watch app to
  force a refetch.
- Make sure the AASA is pure JSON with no BOM or trailing whitespace issues.
  Apple's `swcutil dl -d rularner.github.io` from a Mac can help debug.
- The `appIDs` entry must be `<TEAM_ID>.<BUNDLE_ID>`, i.e.
  `7W4U5RR9QZ.org.larner.SFTransitWatch.watchkitapp`. If you change team ID
  or bundle ID, update the AASA file too.

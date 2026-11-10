# GodFit
A free English-language, mobile-first fitness PWA.

## What works
- 3-day A/B/C full-body gym training plan, using machines and beginner-friendly load targets
- Exercise technique steps and links to YouTube searches for demonstration videos
- Per-set weight/repetition logging and rest countdown timer
- Personal workout history, training-volume chart, body weight/waist records
- Export/restore JSON backup
- Copy a ChatGPT coaching request and import a validated custom plan JSON
- Home Screen installation and offline app shell after first successful visit

## Known limitations
- No native Apple Watch app, watchOS notifications or HealthKit access.
- ChatGPT Plus does not cover OpenAI API charges. AI Coach is a free manual handoff, not embedded API chat.
- Video buttons open YouTube search, not a licensed or verified in-app video player.
- Records use localStorage per browser/device; no automatic sync.
- A hosting service is needed before installing on iPhone as an app; opening index.html via file:// won't enable service worker installation.

## Free deployment with GitHub Pages
1. Create a new public GitHub repository called `godfit`.
2. Upload the contents of this folder to the repository root (not inside another nested folder).
3. In repository Settings → Pages → Build and deployment, select 'Deploy from a branch', `main`, `/ (root)` and save.
4. Open `https://YOUR_USERNAME.github.io/godfit/` in Safari on the iPhone.
5. Share → Add to Home Screen → Add.

GitHub Pages repositories are public on GitHub Free: don't upload personal workout backups, credentials or API keys. The app's tracked data stays on the browser device; it is NOT put into your public GitHub repository.

## Custom workout JSON schema
```json
{"name":"My Gym Plan","days":[{"id":"A","name":"Full Body A","focus":"Strength","exercises":[["leg_press",3,12,90],["chest_press",3,10,90]]}]}
```
Each tuple: [exerciseId, sets, reps_or_seconds, restSeconds]. Known IDs appear in the Coach prompt within the app. Import is validated before saving.

## GodFit v1.1 update (warm-ups, cool-downs, experimental watch alerts)

- The Plan screen now shows a day-specific warm-up and cool-down for Full Body A, B and C.
- An active Workout includes checkable warm-up and cool-down steps; completion is saved in the active workout and its history.
- Settings → Enable rest alerts allows an opt-in notification at the end of a rest timer, when iOS permits notifications.
- The rest alert may appear on a paired Apple Watch when the iPhone is locked; this is **not** an Apple Watch app or a reliable background countdown. iOS can suspend the web app while backgrounded.
- Current workout data uses the same `godfit_v1` local storage key and is retained by the update. **Export a backup before updating.**

### Upgrade GitHub Pages

Upload the new `index.html` and `sw.js` files to the root of the existing `godfit` repository, replacing those two files and committing the changes. The service worker cache version is bumped to `godfit-v1.1.0`. Reopen/relaunch the Home Screen app, and if needed fully close and reopen it to activate the updated service worker.

### Additional Apple Watch facts

A dedicated watchOS UI (live set count, countdown, and completing a set on the watch) needs a native watchOS companion built with Xcode. Apple's free Personal Team allows limited on-device testing but provisioning profiles expire after 7 days; it does not provide an independently maintained no-cost public app deployment path.

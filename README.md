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

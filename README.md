# 🎨 PicturePass 🎨

A browser-based, Telestrations-style drawing & guessing game. Built with Firebase Realtime Database and served on GitHub Pages. No sign-in UI—players are authenticated anonymously behind the scenes.

**Live site:** https://picturepass.github.io/  
**Repo:** https://github.com/PicturePass/picturepass.github.io

---

## Features
- Create/join rooms with short codes
- Alternating draw (80s) ↔ guess (40s) rounds
- Auto-submit on timer end
- Results chain at the end
- Optional community doodle while you wait
- Anonymous Auth (silent) + secured DB rules

## Tech Stack
- HTML/CSS/JS (vanilla)
- Firebase (Compat SDK): App, Auth (anonymous), Realtime Database
- Hosting: GitHub Pages

## Quick Start (local)
1. Clone the repo and open `index.html` (or use a simple static server).
2. In your Firebase project, copy the Web App config into `firebaseConfig` in `index.html`.
3. **Authentication → Sign-in method:** enable **Anonymous**.
4. **Authentication → Settings → Authorized domains:** add:
   - `picturepass.github.io`
   - `localhost` and `127.0.0.1` (for local testing)
5. **Google Cloud Console → APIs & Services → Credentials → your Web API key**
   - **Application restrictions:** *HTTP referrers (web sites)*
   - Add: `https://picturepass.github.io/*`, `http://localhost/*`, `http://127.0.0.1/*`

## Realtime Database Rules
Publish in **Realtime Database → Rules**:
```json
{
  "rules": {
    ".read": false,
    ".write": false,
    "rooms": {
      "$roomId": {
        ".read": "auth != null",
        ".write": "auth != null"
      }
    }
  }
}

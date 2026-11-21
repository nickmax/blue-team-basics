# Blue Team Basics — ISTE 140 Assignment 3

A four-page cybersecurity site (one team home page plus three member guides) built with **CSS Grid only**. Every layout in the project uses `display: grid` — there is no flexbox and no float anywhere.

**Repository:** <https://github.com/nickmax/blue-team-basics>
**Live preview (GitHub Pages):** <https://nickmax.github.io/blue-team-basics/>
**Course submission URL (Banjo):** to be added — see [Deploy to Banjo](#deploy-to-banjo)

> The GitHub Pages link is for teammates to preview work. The assignment submission still requires the `people.rit.edu` URL.

---

## 1. Quick start (teammates — read this first)

You need Git installed. You do **not** need a GitHub account to read the code, but you do need one to push changes.

```sh
# 1. Clone the repo
git clone https://github.com/nickmax/blue-team-basics.git
cd blue-team-basics

# 2. Preview the site locally
python3 -m http.server 8000
```

Open <http://localhost:8000/index.html>.

Do not double-click the HTML files. Opening them through `file://` breaks video captions in some browsers; the local server behaves like the real host.

If you use VS Code, the **Live Server** extension does the same thing.

---

## 2. Who owns what

| File | Owner | Topic | Layout option | Required media |
| --- | --- | --- | --- | --- |
| `index.html` + `assets/css/index.css` | Whole team (one person commits) | Team home page, links to all three guides | Hero grid + 3-card guide grid | — |
| `nick.html` + `assets/css/nick.css` | Nick Mathenge | Phishing and social engineering | **Option 1**: nav left, main right | **Audio** |
| `joshua.html` + `assets/css/joshua.css` | Joshua Twagirashema | Passwords and MFA | **Option 2**: main left, sidebar right | **Video** |
| `ibrahim.html` + `assets/css/ibrahim.css` | Ibrahim Fadil | Endpoint protection and malware | **Option 3**: nav, main, sidebar | — |

**Rule of thumb:** edit only your own HTML file and your own stylesheet. If you need a change to `index.html` (your name in the team list, for example), make it and say so in the commit message so nobody's work is overwritten.

---

## 3. How to make and push a change

Work on a branch, then open a pull request. This keeps `main` clean and makes it obvious who changed what.

```sh
# Start from the latest version
git pull origin main

# Create a branch named after your page
git switch -c nick/phishing-copy

# Edit your files...
git add nick.html assets/css/nick.css assets/media/phishing_voicemail.m4a
git commit -m "nick: rewrite intro and replace voicemail"

git push -u origin nick/phishing-copy
```

Then open the repo on GitHub and click **Compare & pull request**. Ask one teammate to review, then merge.

**Small fixes** (a typo, a broken link) can go straight to `main`:

```sh
git add .
git commit -m "fix: ibrahim footer link"
git pull --rebase origin main
git push origin main
```

Before you push, always run `git pull --rebase origin main`. If two people edit the same file you will get a conflict; the safest habit is to touch only your own files.

### Commit message style

Use a short prefix so the history is readable:

- `nick:` — changes to the phishing page
- `joshua:` — changes to the passwords page
- `ibrahim:` — changes to the endpoints page
- `index:` — home page
- `fix:` — corrections that are not content
- `docs:` — README only

---

## 4. What every page must keep

Do not remove these; they are graded.

- **`.cards` rule**, exactly this, in each member stylesheet:

  ```css
  .cards {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
    gap: 16px;
  }
  ```

  The comment above it must explain what changing `200px` to `300px` does.

- **Four cards per member page**, each with an image, a heading and one or two sentences.
- **`alt` text on every `<img>`** — describe the image, do not write "image".
- **One external stylesheet per page** — no `<style>` blocks, no inline `style=""`.
- **At least 100 words of original copy per page**, in your own voice.
- **HTML and CSS top comments** with page name, student name, student ID, team number and topic.
- **A one-line comment above every CSS rule.**
- **CRAP comments** — at least one each for Contrast, Repetition, Alignment and Proximity.
- **Two finishing touches** on the cards: rounded corners with a soft shadow, and a card that grows a little on hover.
- **Lowercase file names, underscores for multi-word assets** (`mfa_demo.mp4`, not `MFA Demo.mp4`).
- **No flexbox, no floats.** If you need alignment inside a card, use a nested grid.

Quick check before committing:

```sh
grep -rniE "flex|float" --include="*.html" --include="*.css" .
```

It should print nothing.

---

## 5. Personalise your page

### All members

1. Replace every remaining placeholder:
   - `[Team Number]` — all four HTML files, all four CSS files, and `index.html`.
   - `[Student ID 1]` — `nick.html` and `assets/css/nick.css` (Nick Mathenge).
   - `[Student ID 2]` — `joshua.html` and `assets/css/joshua.css` (Joshua Twagirashema).
   - `[Student ID 3]` — `ibrahim.html` and `assets/css/ibrahim.css` (Ibrahim Fadil).
   - Names are already filled in on `index.html`, the member pages and `index.css`.
2. Read the CSS comments and check you can explain each rule. If a comment does not sound like you, rewrite it in your own words.
3. Rewrite one card in your own voice. The current copy is a starting point.

### Member 1 — audio

- Replace `assets/media/phishing_voicemail.m4a` with your own voicemail-style recording (QuickTime, Audacity, or Voice Memos → export M4A).
- Keep the file name, or update `<audio src>` in `nick.html`.
- Add a line under the player if you want to credit the speaker.

### Member 2 — video

- Replace `assets/media/mfa_demo.mp4` with your own screen recording or narrated slides.
- Keep the file name, or update the `<video src>` in `joshua.html`.
- Re-time `assets/media/mfa_demo.vtt` so the three cues match what is said.
- If the first slide changes, update `assets/img/mfa_poster.svg` so the poster still matches the video.

### Member 3 — endpoints

- Three columns get tight on a small screen. Open the page at 1024 px after edits and check the sidebar is still readable.

> **The included audio and video are placeholders** generated for layout testing. They must be replaced with the team's own recordings before submission.

---

## 6. Validation

**Checked 21 Nov 2026** — all four pages pass the W3C HTML validator with no errors. The CSS passes `csstree-validator` with no errors; re-run the W3C CSS validator once before you submit, because the hosted checker was rate limiting during this pass.

- **No non-grid layout declarations** in any HTML or CSS file — confirmed by `grep -rniE "flex|float"`.
- **All local paths resolve** — images, audio, video, captions and stylesheets.
- **Cards at 1440 px** — 3 per row on the two narrow layouts, 2 per row on the three-column layout, all from the `auto-fit` rule alone.
- **Media** — placeholder audio/video still in place; replace them before submission.

Re-run after personalising:

- HTML: <https://validator.w3.org/nu/>
- CSS: <https://jigsaw.w3.org/css-validator/>

---

## 7. Deploy to Banjo

1. Upload the complete folder to your `people.rit.edu` space.
2. Folder permissions `755`, file permissions `644`:

   ```sh
   find . -type d -exec chmod 755 {} \;
   find . -type f -exec chmod 644 {} \;
   ```

3. The home page must be reachable at a URL beginning with `https://people.rit.edu/`.
4. Confirm the live site matches the submitted zip exactly.
5. Paste the full live link into myCourses (not only into the zip or PDF).

### Optional: GitHub Pages preview

The repo is public, so Pages can serve it for free:

1. Repo → **Settings** → **Pages**
2. Source: **Deploy from a branch** → Branch: `main` → Folder: `/ (root)` → **Save**
3. Wait about a minute, then open <https://nickmax.github.io/blue-team-basics/>

Use this to review each other's work, not as the submitted URL.

---

## 8. Project structure

```
blue-team-basics/
├── index.html
├── nick.html                      # phishing + audio
├── joshua.html                    # passwords/MFA + video
├── ibrahim.html                   # endpoints
├── README.md
└── assets/
    ├── css/
    │   ├── index.css
    │   ├── nick.css
    │   ├── joshua.css
    │   └── ibrahim.css
    ├── img/                        # 19 original SVG illustrations
    │   ├── favicon.svg
    │   ├── thumb_phishing.svg  thumb_passwords.svg  thumb_endpoints.svg
    │   ├── flag_attachment.svg  flag_authority.svg  flag_link.svg  flag_urgency.svg
    │   ├── pass_length.svg  pass_mfa.svg  pass_reuse.svg  pass_vault.svg
    │   ├── mfa_poster.svg  mfa_slide2.svg  mfa_slide3.svg
    │   ├── endpoint_updates.svg  endpoint_edr.svg  endpoint_backup.svg  endpoint_usb.svg
    └── media/
        ├── phishing_voicemail.m4a  # placeholder — replace
        ├── mfa_demo.mp4           # placeholder — replace
        └── mfa_demo.vtt           # captions — re-time
```

---

## 9. Submission checklist

- [ ] Team number, names and IDs filled in on the homework document.
- [ ] Team number, names and IDs filled in on the site pages and CSS headers.
- [ ] Placeholder audio replaced with Member 1's recording.
- [ ] Placeholder video and captions replaced with Member 2's recording.
- [ ] `HW3_Team_#.pdf` contains the live link and one wide screenshot per member.
- [ ] `sitename_team#.zip` contains the site, the homework document and the PDF.
- [ ] Site uploaded to Banjo and the live `index.html` link tested in a private browser window.
- [ ] Full live link pasted in the myCourses submission comment.
- [ ] Every member can explain their grid container, the card grid, their CRAP comments, and one live value change.

---

## 10. Troubleshooting

**Video has no captions.** You opened the file directly instead of through a server, or the `.vtt` path is wrong. Run `python3 -m http.server 8000` and reload.

**Cards look cramped on a laptop.** That is expected — the required rule keeps a 200px minimum, so a 13" screen shows three per row. Do not add a media query that hides the rule; explain it instead.

**`git push` rejected.** Someone pushed before you: `git pull --rebase origin main`, resolve any conflict, then push again.

**Images or audio 404 after renaming.** File names are case-sensitive on the server. Use lowercase and underscores, and match the path in HTML exactly.

**Permission errors on Banjo.** Re-run the `chmod` commands from section 7. Directories must be `755`; files must be `644`.

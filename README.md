# Insert Fit Finder — Pristine Sweeps

Enter a fireplace opening measured at the facing, get the wood inserts that fit.

Live at: `https://YOUR-USERNAME.github.io/insert-fit-finder/`
(fill in once published)

---

## Publishing this — click by click

You have GitHub Desktop, so none of this needs the command line.

### 1. Make the repository

1. Open **GitHub Desktop**
2. **File → New Repository**
3. Name: `insert-fit-finder`
4. Local path: anywhere **outside Dropbox** — `Documents` is fine.
   Git and Dropbox fight over the hidden `.git` folder and it causes sync
   errors. Keep them apart.
5. Leave "Initialize with README" **unticked** — this file is the README
6. Click **Create Repository**

### 2. Add the files

Copy all six files from this folder into the repository folder GitHub
Desktop just made:

```
index.html      the app
manifest.json   makes it installable on the phone
sw.js           offline cache
icon-180.png    home-screen icon, iPhone
icon-192.png    home-screen icon, Android
icon-512.png    high-resolution icon
README.md       this file
```

GitHub Desktop will show them as changes.

### 3. Publish

1. Bottom left, type a summary: `Initial version`
2. Click **Commit to main**
3. Top right, click **Publish repository**
4. **Untick "Keep this code private"** — GitHub Pages needs a public repo
   on the free plan
5. Click **Publish repository**

### 4. Turn on Pages

1. In GitHub Desktop: **Repository → View on GitHub**
2. On the website, click **Settings** (top right of the repo)
3. Left sidebar, click **Pages**
4. Under "Build and deployment" → Source, choose **Deploy from a branch**
5. Branch: **main**, folder: **/ (root)**. Click **Save**
6. Wait 1–2 minutes. Refresh. The URL appears at the top of that page.

### 5. Put it on the phone

1. Open the URL in **Safari** on the iPhone
2. Tap the **Share** button (square with the arrow)
3. Scroll down, tap **Add to Home Screen**
4. Name it `Fit Finder`, tap **Add**

It now behaves like an app — full screen, its own icon, and it works with
no signal once it has loaded a first time.

---

## Changing it later

Edit `index.html`, then in GitHub Desktop: commit, then **Push origin**.
Live within a minute or so.

**Important:** if you change `index.html`, also bump the version in
`sw.js` — change `fitfinder-v5` to `fitfinder-v6`. Phones cache
aggressively; without that bump they may keep showing the old version.

---

## What's in the data, and what isn't

Every figure came from manufacturer installation manuals and spec sheets,
**not** product pages. The pages were checked and found to disagree with
the documents on several models — Regency I1150 reads 1.3 g/hr and 71%
HHV on the page but 1.7 and 70% on the sheet, and Osburn's 1700-I and
3500-I pages both overstate the minimum chimney height. Quote the
document.

**BTU** shows the EPA-tested figure where published, with the advertised
maximum struck through. They diverge by up to half — Regency CI2700 is
78,000 advertised against 27,000 tested.

**Known gaps, deliberately visible rather than hidden:**

- **Rear body widths are unverified.** Read off unlabelled dimension
  drawings, not confirmed against a unit. Treated as a prompt to check,
  never as a pass.
- **Regency publishes no plan view**, so no rear width exists for those
  models in any document.
- **Alterra CI1150** — the US site links the Canadian spec sheet, which
  states the model cannot be sold in the USA. No US dimensions found.
- **Alterra Pro i3000** — no opening dimensions published. Surround
  pricing is complete from the 2025 dealer sheet.
- **Osburn MATRIX 1900** — the page says 25" opening width, the manual
  reads 26", and the drawing shows a 28¼" body. Unresolved.
- **Surround pricing** is complete for the i3000 only, pending the 2026
  Regency price sheet.

**Height and depth are hard fails. Width carries a 4" allowance**
(one 2" firebrick course off each side wall) and is flagged for
inspection rather than excluded. Manufacturers explicitly warn against
removing brick or mortar from a masonry fireplace — those flags mark a
job for inspection, not a green light.

Source of truth for the data: `/Pristine Sweeps/Inserts/insert-specs.csv`

Compiled 11 August 2026.

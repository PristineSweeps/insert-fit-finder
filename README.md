# Insert Fit Finder — Pristine Sweeps

Enter a fireplace opening measured at the facing, get the wood inserts that fit.

Live: `https://pristinesweeps.github.io/insert-fit-finder/`

---

## Changing the data — no code needed

**All the stove data lives in two CSV files.** Open them in Numbers, Excel,
or any text editor. You never need to touch `index.html` to add a model,
correct a dimension, or add a surround.

| File | What's in it |
|---|---|
| `models.csv` | One row per model. 40 columns. |
| `surrounds.csv` | One row per surround option. Linked to models by name. |

### To publish a change

1. Edit the CSV and save
2. **Bump the version in `sw.js`** — change `fitfinder-v17` to `v18`
3. GitHub Desktop: commit, then Push origin

Step 2 matters. Phones cache hard, and without the bump yours will keep
showing the old data while you wonder why nothing changed.

### models.csv columns

Leave any cell blank if you don't have it. Blank means "not recorded" and
the tool handles it — it never guesses.

**Identity**
`brand`, `model`, `market` — `model` must match exactly in `surrounds.csv`.

**Manufacturer minimums — these govern every fit decision**
`min_open_w`, `min_open_h`, `min_open_d`, `min_open_d_offset`

A row with `min_open_w` blank is treated as "dimensions not published" and
appears in its own group rather than being silently dropped.

**Stove body — the wiggle room**
`body_w_facing`, `body_w_rear`, `feet_w`, `feet_from_rear`,
`body_d`, `body_h_facing`, `body_h_rear`, `body_h_no_tabs`,
`collar_edge_from_facing`, `taper`, `faceplate_w`, `glass_w`, `glass_h`

- `feet_w` — the feet are often the widest point. The tool reports them
  separately because a channel cut for the feet is a smaller job than
  opening a back wall.
- `body_h_no_tabs` — body height ignoring flue collar tabs, where it can be
  squeezed in.
- `collar_edge_from_facing` — facing to the *near edge* of the flue collar.
  Drives the offset adaptor check. Compute it as
  `body_d − collar_from_rear − 3` for a 6" collar.
- `rear_w_unverified` — rear widths read off drawings that have not been
  confirmed. Advisory only; never rules a model out.

**Performance**
`firebox_cuft`, `btu_advertised`, `btu_tested`, `hhv`, `lhv`,
`emissions_g_hr`, `burn_hr`, `tax_credit` (`yes`/`no`/`unknown`)

Put the EPA-tested figure in `btu_tested`. If both are present the card
shows the tested one with the advertised struck through.

**Install**
`hearth_front`, `hearth_side`, `weight_lb`, `msrp`

Hearth defaults to 16" front / 8" side if left blank.

**Links and notes**
`product_url`, `brochure_url`, `manual_url`, `spec_url`, `flag`, `note`,
`data_status`

`flag` shows as an amber warning on the card. Use it for anything that
should stop someone quoting the row blind.

### surrounds.csv columns

`model`, `surround`, `width`, `height`, `cuttable` (`yes`/blank), `price`, `detail`

The card shows only the **smallest surround that covers the opening**;
the rest are in the expanded view. If none covers it, the model is flagged
rather than excluded — raising the floor, refacing, or a custom surround
can still work.

---

## How the fit logic works

**The manufacturer's published minimum comes first.** Every decision tests
against the manual or spec sheet. Body dimensions, the brick allowance,
feet widths and squeeze heights are *wiggle room* — shown as flags, never
used to loosen the published minimum.

**Height and width at the facing are hard cutoffs.** Nothing can be gained
at the face.

**The 4" allowance applies to the rear and to depth.** Fireboxes taper
inward, so the rear is the pinch point and brick can be removed or
reoriented there.

**Depth is checked twice.** If the top depth clears the insert it's a clean
fit. If only the bottom clears it, that gap is back-wall slope, not solid
wall — flagged for a detailed check, since demoing just the slanted portion
often clears it.

**Offset flue adaptor** is flagged only when the lintel reaches past the
flue collar *and* there's under 6" above the lintel.

**Manufacturers warn against removing brick or mortar from a masonry
fireplace.** These flags mark a job for inspection and judgement, not a
green light.

---

## Known gaps

- **Rear body widths are unverified** except MATRIX 1900, MATRIX 2700 and
  INSPIRE 2000-I. Read off unlabelled drawings; treated as advisory.
- **Regency publishes no plan view**, so no rear width exists in any Regency
  document. Needs a tape measure or the rep.
- **Alterra CI1150** — the US site links the Canadian spec sheet, which
  states the model cannot be sold in the USA.
- **Alterra Pro i3000** — no opening dimensions published. Surround pricing
  is complete from the 2025 dealer sheet.
- **Osburn MATRIX 1900** — page says 25" opening width, manual says 26".
  The tool uses 26". Body measures 25" at the facing.
- **Surround pricing** complete for the i3000 only, pending the 2026 Regency
  price sheet.

Product pages were found to disagree with the manufacturers' own documents
on several models. Quote the document.

Source of truth for the wider dataset:
`/Pristine Sweeps/Inserts/insert-specs.csv`

---

## Publishing from scratch

If this ever needs republishing: GitHub Desktop → File → New Repository,
put it **outside Dropbox**, copy these files in, commit, Publish repository
with "Keep this code private" **unticked**, then on github.com go to
Settings → Pages → Deploy from a branch → `main` → `/ (root)` → Save.

On the phone: open the URL in Safari → Share → Add to Home Screen. It then
works offline once loaded.

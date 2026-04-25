# STL Library Manager — Organize Patreon & Warhammer 40k Collections

Managing STL files is easy when you have ten of them. It stops being easy around the time you hit your third year of Patreon or Kickstarter subscriptions.

---

## What actually goes wrong at scale

### You can't find anything

Your files are spread across hundreds of folders, each named after a month or a campaign. You remember downloading a specific orc warrior six months ago. You have no idea which folder it's in.

### Everything is duplicated

Creators release the same model in multiple versions — supported, unsupported, presupported, revised. Each version is a separate download. Each download lives in its own folder. You are storing the same geometry four times.

### Browsing means extracting

To see what's inside a ZIP or RAR, you extract it. To preview a model, you open a slicer or a separate viewer. A simple "what did I download this month" check turns into a ten-minute workflow.

### Your disk fills up fast

A typical collector with two to three years of Patreon subscriptions accumulates 300–400 GB of STL files — much of it redundant across releases.

---

## What a proper STL manager should do

- Index all files across all archives without requiring extraction
- Let you search by creator, tag, release name, or file name
- Preview models directly, inside the app
- Detect and eliminate duplicate geometry across releases
- Scale to hundreds of GB without slowing down

---

## How Neurochrome Vault handles this

Neurochrome Vault reads ZIP, RAR, and 7z archives directly — you can browse and preview their contents without extracting anything. When you activate the vault, it imports the files into its own deduplicated storage format, eliminating redundancy across your entire library.

The result on a real 362-release wargaming vault:

Original library size 396 GB After NCV deduplication 197 GBSpace saved **199 GB (50%)**

Half the library was duplicated geometry. NCV stored it once.

---

## Result

- Find any model in seconds, across your entire library
- No extraction workflow
- 50% less disk usage on average
- Works on USB drives, external storage, NAS

---

## Related

- [3D Viewer Performance](./3d-viewer-performance.md)
- [STL Deduplication](./deduplication-stl.md)
- [NCV Format](./ncv-format.md)

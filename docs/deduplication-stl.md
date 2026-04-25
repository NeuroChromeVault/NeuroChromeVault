# STL Deduplication — How to Stop Storing the Same Model Twice

If you download models from Patreon, you are almost certainly storing duplicates.

Not because you made a mistake. Because of how creators release files.

---

## How duplication happens

A creator releases a character model. Over the following months:

- Month 1: base model, unsupported
- Month 2: same model, presupported
- Month 4: updated version with fixed geometry
- Month 7: seasonal variant using the same base mesh

Each release is a separate download. Each download contains the full files. The base geometry — which barely changed — is stored four separate times across four separate folders or archives.

Multiply this by 50 creators over three years and you have a library where 40–60% of the disk space is redundant.

---

## File-level deduplication doesn't work here

Some tools detect duplicate files by comparing them byte-for-byte. This catches exact copies but misses the common case: files that contain the same geometry but differ in minor details — a renamed solid, a different export setting, a metadata field that changed.

Most STL duplicates across Patreon releases are not byte-for-byte identical. They are structurally the same model with small differences. File-level deduplication misses all of them.

---

## How Neurochrome Vault deduplicates

NCV operates below the file level. It analyzes the actual content of each STL and identifies shared geometry regardless of filename, folder, or minor differences in how the file was exported.

Shared content is stored once. Every release that contains it holds a reference, not a copy.

---

## Real results

On a 362-release wargaming vault with 85 creators:

Raw STL size396.88 GBOn disk after deduplication197.76 GB**Saved199 GB — 50.2%**

Loot Studios alone, 5 releases: 19 GB raw → 4.89 GB stored. **74% reduction.**

The more releases you have from the same creators, the higher the savings.

---

## Zero risk to your files

Deduplication in NCV is invisible to you. Your files open normally. Your models look exactly the same. Any file can be exported back to a standard STL at any time, bit-for-bit identical to the original.

---

## Related

- [NCV Format](./ncv-format.md)
- [STL Library Manager](./stl-library-manager.md)
- [What is Neurochrome Vault](./what-is-neurochrome.md)

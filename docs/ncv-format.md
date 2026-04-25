# NCV Format — Why Neurochrome Vault Doesn't Use ZIP or RAR

When you import files into Neurochrome Vault, they are optionally stored in the NCV format — a purpose-built storage system for STL libraries. This page explains what it is and why it exists.

---

## The problem with ZIP, RAR, and 7z

Standard archive formats compress files well. But they have a fundamental limitation: **each archive is independent**.

If you download four versions of the same model — supported, unsupported, presupported, and a revised release — and put them in four ZIP files, each ZIP stores the full geometry. You pay four times the storage cost for geometry that barely changed between versions.

There is no mechanism in ZIP, RAR, or 7z to share data between archives. Even if two archives contain byte-for-byte identical files, both store the full content independently.

---

## What NCV does differently

NCV operates at the **vault level**, not the archive level.

When you import a release, NCV analyzes its content and identifies what is genuinely new. Content that already exists in the vault — regardless of which release it came from, or what the file was named — is stored only once. Every archive that contains it just holds a reference.

Under the hood, files are split into chunks, each identified by a BLAKE3 hash. New chunks are compressed with Zstd. Chunks that already exist are reused. This is what makes 50% space savings possible on a real library.

---

## Two formats

FormatPurpose`.ncvd`Internal vault storage — deduplicated, referenced across releases`.ncv`Standalone export — self-contained, portable

`.ncvd` files are how the vault stores your library. `.ncv` files are for export and sharing — a self-contained archive that doesn't depend on the vault.

---

## What this means in practice

**Adding a new version of a model you already own** costs only the storage of what actually changed. For minor revisions, that can be close to zero.

**Real example — Well Known Creator, 5 releases:**

Original size 19 GB On disk (NCV)4.89 GB Saved **14 GB (74%)**

Three quarters of the data was geometry shared across releases. Stored once.

---

## Native archive browsing

You don't have to import everything into the vault to use Neurochrome Vault. ZIP, RAR, and 7z files can be browsed and previewed directly — no extraction, no import required. The vault and its deduplication are optional — activated when you want the storage savings.

---

## Your files are always yours

NCV does not modify your geometry. Any file stored in the vault can be exported back to a standard ZIP or STL at any time, bit-for-bit identical to the original.

---

## Related

- [STL Deduplication](./deduplication-stl.md)
- [What is Neurochrome Vault](./what-is-neurochrome.md)

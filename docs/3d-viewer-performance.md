# 3D Viewer Performance — Why STL Files Feel Slow to Open

Opening a large STL file is slow. Most of the time, it doesn't have to be.

---

## Why it feels slow

The typical workflow for previewing a model:

1. Open a ZIP or RAR archive
2. Extract the STL file
3. Open a slicer or standalone viewer
4. Wait while it loads the entire file before showing anything
5. Finally see the model

For a file in the 50–200 MB range — common for high-detail miniatures — this can take 10–30 seconds in most tools. For a library of thousands of files, this friction adds up fast.

---

## The real bottleneck

It's not always the disk. It's the approach: most viewers wait until the entire file is parsed before rendering anything. You stare at a loading screen, then the model appears all at once.

On large files, the parser can take 10–30 seconds even on fast hardware. On an external USB drive, longer.

---

## How Neurochrome Vault approaches this

NCV focuses on **time to first frame** — how quickly you see *something* on screen after clicking a model.

Instead of waiting for full parse:

- The viewer starts rendering as soon as the first chunks arrive
- You see geometry appearing progressively while the rest loads in background
- The UI stays responsive throughout

No extraction step. No separate viewer to open. Click the model, see it start appearing immediately.

---

## Measured results

Tested on Fantasy_Castle.stl — a 116 MB binary STL file, stored inside a compressed NCV archive, vault on a **USB 3.0 external drive** at \~38 MB/s:

MetricResultCold open average (N=6)**782 ms**Cached open average (N=4)**114 ms**Cache speedup**7x faster on re-open**

Under a second to first frame, on a USB drive, reading from inside a compressed archive. No extraction required.

*(App version 0.9.45, 16-core system, machine under normal load)*

---

## Why this matters for large libraries

When you are browsing a library of thousands of models, you are not loading one file. You are clicking through dozens of them, scanning for the right one. Every second of loading time per model multiplies across your workflow.

At 782 ms average, browsing feels instant. At 10–30 seconds per file, it feels like work.

---

## Related

- [STL Library Manager](./stl-library-manager.md)
- [What is Neurochrome Vault](./what-is-neurochrome.md)

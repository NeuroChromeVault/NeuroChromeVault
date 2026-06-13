# 3D Viewer Performance — Instant LODs and Background Streaming

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

Neurochrome Vault bypasses the loading loop entirely by separating **visual feedback** from **full-resolution data delivery**.

Instead of waiting for a full parse:

1. **Instant LOD Preview**: The viewer instantly renders a pre-calculated low-poly representation of the model. You see the shape, bounds, and orientation in under half a second.
2. **Background Streaming**: While you inspect the preview, rotate the camera, or read the mesh inspector stats, the Rust backend streams the full high-resolution mesh directly into the viewport.
3. **Zero Temp Files**: The data is decrypted and decompressed in memory and passed directly to the GPU via a zero-copy protocol.

No extraction step. No freezing UI. Click the model, see it immediately, and make your printing decisions while the heavy lifting happens in the background.

---

## Measured results

Tested on a 116 MB high-detail miniature STL file, stored inside a compressed NCV vault on an external USB 3.0 drive:

| Metric | Result |
|---|---|
| LOD Preview Render | **< 470 ms** |
| UI Responsiveness | **100% unblocked** |
| Temp Files Written | **0 bytes** |

Under half a second to visual feedback, reading from inside a compressed archive on a USB drive. No extraction required.

---

## Why this matters for large libraries

When you have 300+ GB of files, you spend more time looking for the right model than printing it. 

If every file takes 15 seconds to extract and open, browsing your library becomes a chore. By replacing that workflow with instant previews, Neurochrome Vault lets you visually skim through gigabytes of 3D data as fast as you would browse photos.

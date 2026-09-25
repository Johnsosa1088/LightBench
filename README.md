[README(1).md](https://github.com/user-attachments/files/32636950/README.1.md)
# Lightbench

**One image. Three practical exports. A clear record of what changed.**

Lightbench is a small, local image workbench built through collaboration between the project steward and Codex. It began with a question: *How much of an image can we carry before the image visibly breaks?* The current release lets you explore that question with adjustable JPG budgets, source-size output, and two SVG companions.

Drop in an image. Lightbench writes:

- A **JPG** using the workflow you chose.
- A **full-pixel SVG** embedding a lossless PNG of the decoded, EXIF-oriented image at its original dimensions.
- A **compact SVGZ** embedding the exact exported JPG.
- A **JSON report** recording dimensions, byte counts, SHA-256 hashes, adapters, and source provenance.

Both SVG companions are **raster-backed containers**. They scale as SVG documents; they do not create missing pixels or turn the photograph into editable vector shapes. The optional, separate `lightbench.py` command makes an *approximate* SVG out of editable color rectangles.

## Start on Windows

1. Install Python 3 for Windows with the `py` launcher.
2. Download the project files, keep them together in one folder, and run `setup_windows.bat` once.
3. Drag a supported image onto a launcher:

| Launcher | JPG dimensions | Size control |
| --- | --- | --- |
| `drop_image_here.bat` | Same as the input after EXIF orientation | Automatic quality 88; file size varies. |
| `try_jpg_budget.bat` | Same as the input after EXIF orientation | Enter a JPG cap in KiB, or press Enter for automatic quality 88. |
| `drop_small_image_here.bat` | At most 768 pixels wide; may shrink further | At most 144 KiB. |

The outputs appear beside your input, which is not modified. Each budget-labelled run produces separate output filenames for comparison. If a requested budget cannot fit the image even at JPEG quality 1, the native-size workflow reports the minimum needed and stops instead of quietly reducing its dimensions.

Supported inputs: **JPG/JPEG, PNG, WebP, BMP, single-frame GIF, and supported single-frame TIFF**. The decoder accepts RGB, RGBA, L, LA, and P modes. Animated, high-bit-depth, RAW, HEIC, SVG and PDF inputs are outside this release. Input limits are **32 MiB** and **16 million decoded pixels**. See [START_HERE_WINDOWS.md](START_HERE_WINDOWS.md) for details.

## Compare instead of guessing

Run `py -3 compare_export.py` to check the bundled example, or pass your own image path. The comparison checks output hashes, JPG budget, the exact JPG inside SVGZ, and the full-resolution decoded pixels inside SVG. It also reports error against the input at the JPG's working dimensions. Pixel error is a measurement, not a substitute for looking at text, gradients, edges, and fine texture at 100% zoom.

A smaller JPG is useful when its visible quality meets your needs. File-size comparisons across image editors depend on dimensions and encoder settings; no universal compression advantage is claimed.

## Separate shape-vector experiment

For an editable, source-conditioned approximation made of solid-color SVG rectangles:

```sh
python3 lightbench.py photo.png --width 768 --target-kib 700 --jpeg-kib 144 --out vector_result
```

This command produces a native-shape SVG, compressed SVGZ, PNG preview, optional JPG, and report. It is slower and visually different from the three drag workflows. The shapes approximate the input; they do not reconstruct unseen detail. See [LIGHTBENCH_RELEASE_README.md](LIGHTBENCH_RELEASE_README.md) and [PORT_CONTRACT.md](PORT_CONTRACT.md) for precise behavior.

## The larger workbench

Lightbench is the **first public tool** emerging from a broader CLCE Connected Workbench exploration. Earlier private experiments explored image-to-geometry conversion, layered light and color, heat and water ledgers, environmental state, and graph-based atlas scaffolding. They inform how we ask questions and keep provenance, but **they are not included or validated by this image-export release**.

Candidate follow-on releases from that work include:

| Workbench line | What it has explored | Status here |
| --- | --- | --- |
| **CLCE Connected Workbench** | Shared contracts, provenance, and controlled transformation workflows. | Separate project; not included. |
| **Lotus Heart and reservoir models** | Pulse, pressure, flow, return, and conservation in declared simulations. | Exploratory models; not physical validation. |
| **Atomic Atlas** | Graph state, transitions, and persistent ledgers. | Separate experimental architecture. |
| **Environment and layered light tools** | Water, air, heat, color, and visual layers under explicit budgets. | Candidate components; not bundled. |
| **Relational transformation core** | Portable profiles, constraints, and output checks across domains. | Separate public-core line. |

We expect to publish selected tools separately as they become self-contained, documented, and independently testable. Each future release will state its own inputs, outputs, limits, and evidence. This roadmap is an intention, not a claim that those engines already run inside Lightbench.

## Scope and attribution

Lightbench transforms images provided by the user. It does not generate new image content, restore lost detail, establish physical truth, or grant rights to redistribute an input image. The source remains yours to manage. This public core contains no private Aurelia imagery or original-source archives.

Developed collaboratively by the project steward and **Codex (OpenAI)**, with tests and boundaries recorded alongside the code. The project owner has not selected a public software license in this package; add one if you want to grant others permission to reuse or modify the code.

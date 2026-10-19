# Denia V4-polish voice release

This package contains the final V4-polish acoustic LoRA export and the source audio clips used for the Denia voice project.

## Contents

- `model/denia-v4-polish-e10-s4910-l32.pth` — V4 acoustic export, epoch 10, optimizer step 4910, LoRA rank 32 (75,552,571 bytes).
- `dataset/training_segments/` — 140 WAV clips.
- `dataset/reference_candidates/` — 8 WAV reference clips.
- `dataset/metadata/` — source indexes with local filesystem paths removed.
- `SHA256SUMS.txt` — checksums for the files in this release, excluding this checksum file.

The model export requires a compatible GPT-SoVITS V4 runtime and its base weights; those are not included here.

No license is granted by this repository. The audio and model are included under the project owner's stated authorization for public release.

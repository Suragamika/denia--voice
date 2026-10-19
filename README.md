# Denia V4-polish voice release

This package contains the final V4-polish acoustic LoRA export and the source audio clips used for the Denia voice project.

## Contents

- `model/denia-v4-polish-e10-s4910-l32.pth.part01` through `part03` — the final V4 acoustic export split into three files for upload.
- `dataset/training_segments/` — 140 WAV clips.
- `dataset/reference_candidates/` — 8 WAV reference clips.
- `dataset/metadata/` — source indexes with local filesystem paths removed.
- `SHA256SUMS.txt` — checksums for the release files, excluding this checksum file.

The model export is 75,552,571 bytes when reassembled. In PowerShell, from the repository root:

```powershell
Set-Location .\model
$parts = 1..3 | ForEach-Object { 'denia-v4-polish-e10-s4910-l32.pth.part{0:D2}' -f $_ }
$outputPath = 'denia-v4-polish-e10-s4910-l32.pth'
$output = [IO.File]::Create($outputPath)
try {
    foreach ($part in $parts) {
        $source = [IO.File]::OpenRead($part)
        try { $source.CopyTo($output) } finally { $source.Dispose() }
    }
} finally { $output.Dispose() }
Get-FileHash $outputPath -Algorithm SHA256
```

The expected SHA-256 for the reconstructed model is `699706929d2241efd6ca0358cf2717515f781b16bf6f33fdfdc84db9341dc042`.

The model export requires a compatible GPT-SoVITS V4 runtime and its base weights; those are not included here.

No license is granted by this repository. The audio and model are included under the project owner's stated authorization for public release.

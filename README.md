# Denia V4-polish Voice Release

[简体中文](#简体中文) · [English](#english) · [日本語](#日本語)

---

## 简体中文

本仓库包含 Denia V4-polish 最终声学 LoRA 导出文件及用于该语音项目的音频片段。

### 文件内容

- `model/denia-v4-polish-e10-s4910-l32.pth.part01` 至 `part03`：分成 3 个文件存放的最终 V4 声学模型。
- `dataset/training_segments/`：140 个 WAV 训练片段。
- `dataset/reference_candidates/`：8 个 WAV 参考片段。
- `dataset/metadata/`：已移除本机绝对路径的数据索引。
- `SHA256SUMS.txt`：发布文件的校验和（不含此校验文件）。

### 合并模型

模型合并方法见下方[通用合并说明](#model-reconstruction--模型合并--モデルの結合)。合并后的文件大小应为 **75,552,571 字节**，SHA-256 应为：

`699706929d2241efd6ca0358cf2717515f781b16bf6f33fdfdc84db9341dc042`

### 运行环境与许可

运行模型需要兼容的 GPT-SoVITS V4 环境及其基础权重；本仓库不包含这些文件。

仓库根目录包含一个 `LICENSE` 文件。本 README 未说明该文件对所附音频和模型权重的适用范围；公开发布授权与许可条款是两回事。

---

## English

This repository contains the final Denia V4-polish acoustic LoRA export and audio clips used for the voice project.

### Contents

- `model/denia-v4-polish-e10-s4910-l32.pth.part01` through `part03`: the final V4 acoustic model split into three files.
- `dataset/training_segments/`: 140 WAV training clips.
- `dataset/reference_candidates/`: 8 WAV reference clips.
- `dataset/metadata/`: dataset indexes with local absolute paths removed.
- `SHA256SUMS.txt`: checksums for the release files, excluding this checksum file.

### Reassemble the model

Follow the [shared model reconstruction instructions](#model-reconstruction--模型合并--モデルの結合) below. The reconstructed file should be **75,552,571 bytes** with this SHA-256:

`699706929d2241efd6ca0358cf2717515f781b16bf6f33fdfdc84db9341dc042`

### Runtime and license

The model requires a compatible GPT-SoVITS V4 runtime and its base weights; neither is included here.

A `LICENSE` file is present at the repository root. This README does not specify whether it applies to the bundled audio and model weights; public-release authorization and license terms are separate.

---

## 日本語

このリポジトリには、Denia V4-polish の最終音響 LoRA エクスポートと、音声プロジェクトで使用した音声クリップが含まれています。

### 内容

- `model/denia-v4-polish-e10-s4910-l32.pth.part01` ～ `part03`：3 つのファイルに分割された最終 V4 音響モデル。
- `dataset/training_segments/`：WAV 学習用クリップ 140 件。
- `dataset/reference_candidates/`：WAV 参照用クリップ 8 件。
- `dataset/metadata/`：ローカルの絶対パスを削除したデータセット索引。
- `SHA256SUMS.txt`：このチェックサムファイルを除くリリースファイルのチェックサム。

### モデルの結合

下記の[共通モデル結合手順](#model-reconstruction--模型合并--モデルの結合)を実行してください。結合後のファイルサイズは **75,552,571 バイト**、SHA-256 は次の値になるはずです。

`699706929d2241efd6ca0358cf2717515f781b16bf6f33fdfdc84db9341dc042`

### 実行環境とライセンス

モデルの実行には、互換性のある GPT-SoVITS V4 環境とそのベース重みが必要です。これらは本リポジトリに含まれていません。

リポジトリのルートには `LICENSE` ファイルがあります。この README では、同ファイルが同梱の音声およびモデル重みに適用される範囲を明記していません。公開の許可とライセンス条件は別のものです。

---

## Model reconstruction · 模型合并 · モデルの結合

Run this in PowerShell from the repository root:

```powershell
Set-Location .\model
$base = 'denia-v4-polish-e10-s4910-l32.pth'
$outputPath = $base
$output = [IO.File]::Create($outputPath)
try {
    foreach ($index in 1..3) {
        $part = '{0}.part{1:D2}' -f $base, $index
        $source = [IO.File]::OpenRead($part)
        try { $source.CopyTo($output) } finally { $source.Dispose() }
    }
} finally {
    $output.Dispose()
}
Get-FileHash $outputPath -Algorithm SHA256
```

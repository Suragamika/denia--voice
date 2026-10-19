# Denia V4 Voice Model and Dataset

[简体中文](#简体中文) · [English](#english) · [日本語](#日本語)

---

## 简体中文

本仓库包含 Denia V4 最终声学 LoRA 权重，以及用于该语音项目的音频片段。模型文件名中的 `v4-polish` 是原始导出标记。

### 文件内容

- `model/denia-v4-polish-e10-s4910-l32.pth.part01` 至 `part03`：拆分为 3 个文件的模型权重。
- `dataset/training_segments/`：140 个 WAV 训练片段。
- `dataset/reference_candidates/`：8 个 WAV 参考片段。
- `dataset/metadata/`：已移除本机绝对路径的数据索引。
- `SHA256SUMS.txt`：发布文件的校验和（不含此校验文件）。

### 模型校验

合并后的模型大小应为 **75,552,571 字节**，SHA-256 应为：

`699706929d2241efd6ca0358cf2717515f781b16bf6f33fdfdc84db9341dc042`

### 运行环境与许可

运行模型需要兼容的 GPT-SoVITS V4 环境及其基础权重；本仓库不包含这些文件。

仓库根目录包含 `LICENSE` 文件。本 README 未说明该许可对所附音频和模型权重的适用范围。

---

## English

This repository contains the final Denia V4 acoustic LoRA weights and audio clips used for the voice project. The model filename uses the original export tag `v4-polish`.

### Contents

- `model/denia-v4-polish-e10-s4910-l32.pth.part01` through `part03`: the model weights split into three files.
- `dataset/training_segments/`: 140 WAV training clips.
- `dataset/reference_candidates/`: 8 WAV reference clips.
- `dataset/metadata/`: dataset indexes with local absolute paths removed.
- `SHA256SUMS.txt`: checksums for the release files, excluding this checksum file.

### Model checksum

The reconstructed model should be **75,552,571 bytes** with this SHA-256:

`699706929d2241efd6ca0358cf2717515f781b16bf6f33fdfdc84db9341dc042`

### Runtime and license

The model requires a compatible GPT-SoVITS V4 runtime and its base weights; neither is included here.

A `LICENSE` file is present at the repository root. This README does not specify whether that license applies to the bundled audio and model weights.

---

## 日本語

このリポジトリには、Denia V4 の最終音響 LoRA 重みと、音声プロジェクトで使用した音声クリップが含まれています。モデルのファイル名には、元のエクスポート識別子 `v4-polish` が使われています。

### 内容

- `model/denia-v4-polish-e10-s4910-l32.pth.part01` ～ `part03`：3 つのファイルに分割されたモデル重み。
- `dataset/training_segments/`：WAV 学習用クリップ 140 件。
- `dataset/reference_candidates/`：WAV 参照用クリップ 8 件。
- `dataset/metadata/`：ローカルの絶対パスを削除したデータセット索引。
- `SHA256SUMS.txt`：このチェックサムファイルを除くリリースファイルのチェックサム。

### モデルのチェックサム

結合後のモデルは **75,552,571 バイト**で、SHA-256 は次の値になるはずです。

`699706929d2241efd6ca0358cf2717515f781b16bf6f33fdfdc84db9341dc042`

### 実行環境とライセンス

モデルの実行には、互換性のある GPT-SoVITS V4 環境とそのベース重みが必要です。これらは本リポジトリに含まれていません。

リポジトリのルートには `LICENSE` ファイルがあります。この README では、同ライセンスが同梱の音声およびモデル重みに適用されるかどうかを明記していません。

---

<a id="reconstruct-model"></a>
## Reconstruct the model · 模型分片合并 · モデルファイルの結合

From the repository root, run the following in PowerShell. / 在仓库根目录用 PowerShell 执行以下命令。 / リポジトリのルートで PowerShell から次のコマンドを実行してください。

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

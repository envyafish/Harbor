# 手动下载生成字幕模型 / Sidecar

适合网络慢、HuggingFace 不稳定、或想提前离线准备的情况：在浏览器或其它机器下好文件，再拷进 Harbor 的数据目录。文件齐全且校验通过后，Harbor 会**跳过自动下载**。

> **适用平台：** Apple Silicon Mac、Windows x64。  
> **注意：** 放置前请先**完全退出 Harbor**，拷完再打开。文件名或目录不对会导致重新下载或校验失败。

Sidecar 发布页（公开）：[Harbor · ct2-sidecars-v1](https://github.com/envyafish/Harbor/releases/tag/ct2-sidecars-v1)

---

## 1. 找到数据目录

| 系统 | 路径 |
|------|------|
| macOS | `~/Library/Application Support/com.tunan.harbor/` |
| Windows | `%APPDATA%\com.tunan.harbor\`（一般是 `C:\Users\<你>\AppData\Roaming\com.tunan.harbor\`） |

下文用 `{app_data}` 表示该目录。

```text
{app_data}/
  tools/           ← 工具程序（ffmpeg、whisper-cli、翻译组件等）
  models/          ← 模型文件
  generated-subs/  ← 生成好的字幕（不必手动放）
```

---

## 2. 目录总览

```text
{app_data}/
  tools/
    ffmpeg                 # Windows 为 ffmpeg.exe
    whisper/
      whisper-cli          # Windows 为 whisper-cli.exe
      …同目录依赖库…
    whisper-cpu/           # Windows：CPU 识别
    whisper-vulkan/        # Windows：Vulkan 识别
    whisper-cuda/          # Windows：CUDA 识别
    ct2-mt/
      ct2-mt               # Windows 为 ct2-mt.exe
    ct2-whisper-ja-cpu/    # 可选：日语直译（CPU）
    ct2-whisper-ja-cuda/   # 可选：日语直译（CUDA，仅 Windows）
  models/
    whisper/
      ggml-*.bin
      ggml-*.sha256        # 建议一并放置（见第 3 节）
    opus-mt-en-zh-ct2/     # 英→中翻译
    opus-mt-ja-en-ct2/     # 日→英翻译（日语音轨用）
    nllb-200-distilled-600M-ct2/   # 可选：NLLB 翻译
    whisper-ja-zh-chickenrice-ct2/ # 可选：日语直译模型
```

---

## 3. Whisper 模型（最常手动放）

设置里选的识别档位对应下列文件，放到：

```text
{app_data}/models/whisper/
```

| 设置档位 | 文件名 | 约大小 |
|----------|--------|--------|
| base | `ggml-base.bin` | ~140MB |
| small（默认） | `ggml-small.bin` | ~460MB |
| medium | `ggml-medium.bin` | ~1.5GB |
| large | `ggml-large-v3.bin` | ~3GB |
| turbo | `ggml-large-v3-turbo.bin` | ~1.6GB |

下载地址：

```text
https://huggingface.co/ggerganov/whisper.cpp/resolve/main/<文件名>
```

例（small）：  
https://huggingface.co/ggerganov/whisper.cpp/resolve/main/ggml-small.bin

### 建议同时写校验文件

把 `.bin` 换成 `.sha256`，内容为**一整行小写 SHA256**（与下表一致）：

| 模型文件 | 校验文件 |
|----------|----------|
| `ggml-small.bin` | `ggml-small.sha256` |
| `ggml-medium.bin` | `ggml-medium.sha256` |
| … | … |

```bash
# macOS
cd "$HOME/Library/Application Support/com.tunan.harbor/models/whisper"
shasum -a 256 ggml-small.bin
echo -n '1be3a9b2063867b937e64e2ec7483364a79917e157fa98c5d94b5c1fffea987b' > ggml-small.sha256
```

```powershell
# Windows
$dir = "$env:APPDATA\com.tunan.harbor\models\whisper"
Get-FileHash "$dir\ggml-small.bin" -Algorithm SHA256
Set-Content -Path "$dir\ggml-small.sha256" -NoNewline -Value "1be3a9b2063867b937e64e2ec7483364a79917e157fa98c5d94b5c1fffea987b"
```

| 文件 | SHA256 |
|------|--------|
| `ggml-base.bin` | `60ed5bc3dd14eea856493d334349b405782ddcaf0028d4b5df4088345fba2efe` |
| `ggml-small.bin` | `1be3a9b2063867b937e64e2ec7483364a79917e157fa98c5d94b5c1fffea987b` |
| `ggml-medium.bin` | `6c14d5adee5f86394037b4e4e8b59f1673b6cee10e3cf0b11bbdbee79c156208` |
| `ggml-large-v3.bin` | `64d182b440b98d5203c4f9bd541544d84c605196c4f7b845dfa11fb23594d1e2` |
| `ggml-large-v3-turbo.bin` | `1fc70f774d38eb169993ac391eea357ef47c88757ef72ee5943879b7e8e2bc69` |

哈希不对时 Harbor 会删掉旧文件再重新下载。

---

## 4. ffmpeg

放到：

```text
{app_data}/tools/ffmpeg          # macOS
{app_data}/tools/ffmpeg.exe      # Windows
```

来源：[ffmpeg-static b6.0](https://github.com/eugeneware/ffmpeg-static/releases/tag/b6.0)

| 平台 | 下载文件名 | 放到本地后的名字 | SHA256 |
|------|------------|------------------|--------|
| macOS Apple Silicon | `ffmpeg-darwin-arm64` | `ffmpeg` | `a90e3db6a3fd35f6074b013f948b1aa45b31c6375489d39e572bea3f18336584` |
| macOS Intel | `ffmpeg-darwin-x64` | `ffmpeg` | `cfe20936c83ecf5d68e424b87e8cc45b24dd6be81787810123bb964a0df686f9` |
| Windows x64 | `ffmpeg-win32-x64` | `ffmpeg.exe` | `e9fd5e711debab9d680955fc1e38a2c1160fd280b144476cc3f62bc43ef49db1` |

macOS：

```bash
chmod +x "{app_data}/tools/ffmpeg"
xattr -dr com.apple.quarantine "{app_data}/tools/ffmpeg"   # 若提示无法打开
```

若本机已安装可用的 `ffmpeg`，也可不手动放置，让 Harbor 使用系统自带。

---

## 5. whisper-cli（语音识别程序）

### macOS Apple Silicon

1. 下载：  
   [whisper-cli-darwin-arm64.tar.gz](https://github.com/envyafish/Harbor/releases/download/ct2-sidecars-v1/whisper-cli-darwin-arm64.tar.gz)  
   SHA256：`44c2fcad873d9c86fa56b50b1cc211403d0d0266ec91d1ad8874c317ca59442b`
2. 解压后，将 `whisper-cli` 及同层依赖库放到：

```text
{app_data}/tools/whisper/
  whisper-cli
  （以及压缩包里同目录的其它文件）
```

3. 赋权：

```bash
chmod +x "{app_data}/tools/whisper/whisper-cli"
xattr -dr com.apple.quarantine "{app_data}/tools/whisper"
```

### Windows x64

按设置中的识别后端，解压到**对应目录**（不要混放）：

| 后端 | 下载 | 解压到 |
|------|------|--------|
| CPU | [whisper-bin-x64.zip](https://github.com/ggml-org/whisper.cpp/releases/download/v1.9.1/whisper-bin-x64.zip) | `{app_data}\tools\whisper-cpu\` |
| Vulkan | [Vulkan 包](https://github.com/envyafish/Harbor/releases/download/ct2-sidecars-v1/whisper-cli-x86_64-pc-windows-msvc-vulkan.zip) | `{app_data}\tools\whisper-vulkan\` |
| CUDA | [CUDA 包](https://github.com/envyafish/Harbor/releases/download/ct2-sidecars-v1/whisper-cli-x86_64-pc-windows-msvc-cuda.zip) | `{app_data}\tools\whisper-cuda\` |

解压后目录内应能直接看到 `whisper-cli.exe` 及 DLL。CUDA 需要本机 NVIDIA 驱动可用。

| 压缩包 | SHA256 |
|--------|--------|
| Windows CPU | `7d8be46ecd31828e1eb7a2ecdd0d6b314feafd82163038ab6092594b0a063539` |
| Windows Vulkan | `5f90f59ae77e49509c38cc19263b8ee8b04ac3c52ccad5c79ebb080efbebb829` |
| Windows CUDA | `6d4a882a6be05c287d93a10a765929a000c10feaeebf1e8e528e73d75ead406f` |

---

## 6. 翻译组件（ct2-mt）与翻译模型

「识别后再译成中文」时需要。

### 6.1 程序

| 平台 | 下载 | 放到（注意改名） |
|------|------|------------------|
| macOS Apple Silicon | [ct2-mt-aarch64-apple-darwin](https://github.com/envyafish/Harbor/releases/download/ct2-sidecars-v1/ct2-mt-aarch64-apple-darwin) | `{app_data}/tools/ct2-mt/ct2-mt` |
| Windows x64 | [ct2-mt-x86_64-pc-windows-msvc.exe](https://github.com/envyafish/Harbor/releases/download/ct2-sidecars-v1/ct2-mt-x86_64-pc-windows-msvc.exe) | `{app_data}\tools\ct2-mt\ct2-mt.exe` |

下载后的长文件名必须改成 `ct2-mt` / `ct2-mt.exe`。

```bash
# macOS 示例
mkdir -p "$HOME/Library/Application Support/com.tunan.harbor/tools/ct2-mt"
curl -L -o "$HOME/Library/Application Support/com.tunan.harbor/tools/ct2-mt/ct2-mt" \
  "https://github.com/envyafish/Harbor/releases/download/ct2-sidecars-v1/ct2-mt-aarch64-apple-darwin"
chmod +x "$HOME/Library/Application Support/com.tunan.harbor/tools/ct2-mt/ct2-mt"
```

| 平台 | SHA256 |
|------|--------|
| macOS Apple Silicon | `7437fe0f0506f8412c13638a71767ee9b8023e0f10fd4f37b126bd19f6efea68` |
| Windows x64 | `dcc78cd6c70d9031ca4cac8c7e5401d67e5bc26669b761cf0cb9e8d6a8d426c9` |

### 6.2 Opus 翻译模型（默认）

每个目录文件需**齐全**，且哈希与下表一致。

**英→中** → `{app_data}/models/opus-mt-en-zh-ct2/`  
下载前缀：`https://huggingface.co/gaudi/opus-mt-en-zh-ctranslate2/resolve/main/`

| 文件 | SHA256 |
|------|--------|
| `model.bin` | `f24c2bb82368f7de0196882de1d8b644d2aa54ae2439c3142f263de8a64ea2a9` |
| `source.spm` | `5775ddc9e3ff2fae91554da56468ad35ff56edaba870fea74447bc7234bfdaa8` |
| `target.spm` | `81dc94efa84e4025ef38d25d5d07429fe41e3eb29d44003f1db6fe98487b0052` |
| `config.json` | `ce02c0c0d02f285d2ff34c80b0867ccb5c4a3b250a275e6d1d2884f5499a6e46` |
| `shared_vocabulary.json` | `37314a6abb25ed8f8497498aeeb31fcea98de892bf00ff7c2e8c966b26fe0b82` |

**日→英**（日语音轨）→ `{app_data}/models/opus-mt-ja-en-ct2/`  
下载前缀：`https://huggingface.co/gaudi/opus-mt-ja-en-ctranslate2/resolve/main/`

| 文件 | SHA256 |
|------|--------|
| `model.bin` | `fcc505f9a24b43caf3514e5bc3fc1581bbe0b17cbf99d4eff136b7b5af4997e1` |
| `source.spm` | `d0b5c3b10b5959f056ff2c86e2f2356129242ff1fc72d3a4a34d6a8c0eee4e57` |
| `target.spm` | `35d89c704e270d441fade716a3931d49c43179400682edcca7f180694982a2f6` |
| `config.json` | `ce02c0c0d02f285d2ff34c80b0867ccb5c4a3b250a275e6d1d2884f5499a6e46` |
| `shared_vocabulary.json` | `c6e7f9988e5fe15c59ed331ce2d7c3dd551e70add8efc09f839f5a48168da4d6` |

### 6.3 NLLB（可选）

设置里选用 NLLB 时需要 → `{app_data}/models/nllb-200-distilled-600M-ct2/`  
下载前缀：`https://huggingface.co/JustFrederik/nllb-200-distilled-600M-ct2-int8/resolve/main/`  
许可：CC-BY-NC。

| 文件 | SHA256 |
|------|--------|
| `model.bin` | `ed1beaf75134de7505315a5223162f56acff397eff6b50638a500d3936fe707b` |
| `sentencepiece.bpe.model` | `14bb8dfb35c0ffdea7bc01e56cea38b9e3d5efcdcb9c251d6b40538e1aab555a` |
| `config.json` | `0c2f6fa2057c7264d052fb4a62ba3476eeae70487acddfa8e779a53a00cbf44c` |
| `shared_vocabulary.txt` | `a132a83330f45514c2476eb81d1d69b3c41762264d16ce0a7ea982e5d6c728e5` |

---

## 7. 日语直译（可选）

仅在设置中开启日语直译相关选项时需要。

### 7.1 程序

| 平台 | 下载 | 放到（注意改名） |
|------|------|------------------|
| macOS Apple Silicon | [ct2-whisper-ja-aarch64-apple-darwin](https://github.com/envyafish/Harbor/releases/download/ct2-sidecars-v1/ct2-whisper-ja-aarch64-apple-darwin) | `{app_data}/tools/ct2-whisper-ja-cpu/ct2-whisper-ja` |
| Windows CPU | [Windows CPU](https://github.com/envyafish/Harbor/releases/download/ct2-sidecars-v1/ct2-whisper-ja-x86_64-pc-windows-msvc.exe) | `{app_data}\tools\ct2-whisper-ja-cpu\ct2-whisper-ja.exe` |
| Windows CUDA | [Windows CUDA zip](https://github.com/envyafish/Harbor/releases/download/ct2-sidecars-v1/ct2-whisper-ja-x86_64-pc-windows-msvc-cuda.zip) | 解压到 `{app_data}\tools\ct2-whisper-ja-cuda\` |

单文件下载后需改名为 `ct2-whisper-ja` / `ct2-whisper-ja.exe`。CUDA 压缩包按包内结构解压即可。

| 文件 | SHA256 |
|------|--------|
| macOS | `ea41ea85a60a19b823e26fb16bdd191fa62d7ac3e61c1306367a49722f442e4d` |
| Windows CPU | `e6ff083967518f48485099ea98a3b90124f9746eea8702d5063d8c92e0fae889` |
| Windows CUDA zip | `f81baf9acfbf5ec34f37032fdc32993143a186e3a85c0b6587282887a71c7bee` |

### 7.2 模型（约 3GB）

目录：`{app_data}/models/whisper-ja-zh-chickenrice-ct2/`  
下载前缀：`https://huggingface.co/chickenrice0721/whisper-large-v2-translate-zh-v0.2-st-ct2/resolve/main/`

| 文件 | SHA256 |
|------|--------|
| `model.bin` | `d9ede0107bf5eef437db3625216e2395aebafd0a72967c5583c6234659d18273` |
| `config.json` | `d86b7a7664a12559d644aa210a32ce9a7e03913e794b7ea4fb7182de69e273a7` |
| `preprocessor_config.json` | `994838f1fa6462c8b9b3c90edada831f11f3dd8b4664634e18f4694d005c9dbf` |
| `tokenizer.json` | `27fc476bfe7f17299480be2273fc0608e4d5a99aba2ab5dec5374b4482d1a566` |
| `vocabulary.json` | `5ad28279db5e546349708b9a74736e2c018737ac5a600f1048f1f26c99b85b47` |

---

## 8. 最短路径（只跳过「下载 Whisper 模型」）

多数情况卡在大模型。最少步骤：

1. 退出 Harbor  
2. 创建 `{app_data}/models/whisper/`  
3. 放入设置里选中的那一个 `ggml-*.bin`  
4. 写入对应的 `ggml-*.sha256`（内容见第 3 节表格）  
5. 重新打开 Harbor，再生成字幕  

工具程序体积较小，一般可继续交给 Harbor 自动下载；优先手动放置 HuggingFace 上的大模型即可。

---

## 9. 校验与排错

1. **目录名、文件名必须与上文完全一致。**  
2. **程序要改名**：例如下载的是 `ct2-mt-aarch64-apple-darwin`，本地必须叫 `ct2-mt`。  
3. **SHA 不对会删掉重下**——用 `shasum -a 256`（macOS）或 `Get-FileHash`（Windows）先核对。  
4. macOS 提示无法打开：对目录执行 `xattr -dr com.apple.quarantine <路径>`。  
5. Windows GPU：确认已装显卡驱动与 VC++ 运行库。  
6. Harbor 升级后，若官方组件包有更新，旧文件可能不再匹配——请对照本文表格或 [ct2-sidecars-v1](https://github.com/envyafish/Harbor/releases/tag/ct2-sidecars-v1) 重新下载。

可在 Harbor **诊断日志**中查看生成字幕相关记录，确认是否已使用本地文件。

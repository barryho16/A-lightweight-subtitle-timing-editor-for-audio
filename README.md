# Subber — 音頻字幕編輯器 / Audio Subtitle Editor

[English](#english) | [繁體中文](#繁體中文)

A lightweight, audio-only subtitle timing editor with an Aegisub-style
S / D / F / G "timing" workflow, waveform scrubbing, and full tablet support.
Single-file HTML, zero frameworks, zero build steps.

一個輕量的「僅音頻」字幕時間軸編輯器，具備 Aegisub 風格的 S / D / F / G 打軸
工作流、波形可視化打點，並完整支援平板觸控操作。單一 HTML 檔，零框架、零建置步驟。

| 檔案 / File | 說明 / Description |
|---|---|
| `音頻字幕編輯器.html` | The entire application. Open this file. |
| `設計文件.txt` | Design specification v2.0 (Traditional Chinese). |

---

# English

## Quick start

No installation, no server, no build.

1. Open `音頻字幕編輯器.html` in Chrome, Edge, Firefox, or Safari.
2. Click **📂 音頻** and pick an audio file (`audio/*` — mp3, wav, m4a, ogg,
   and flac on browsers that can decode it).
3. Optionally click **📄 SRT** to load an existing subtitle file.
4. Click **📤 匯出** to save your work.

The editor boots with 4 demo subtitle lines so you can try the keyboard
workflow before loading anything.

## Keyboard shortcuts (desktop)

| Key | Action |
|---|---|
| `S` / `Space` | Play the selected line |
| `D` | Play the last 500 ms of the line (whole line if shorter) |
| `G` / `Ctrl+Enter` | Commit and jump to the next line |
| `A` / `F` | Pan the view left / right by 30% |
| `Z` / `Ctrl+Z` | Undo (up to 100 steps) |
| `Ctrl+I` | Insert a blank subtitle after the selection |
| `Delete` | Delete the selected subtitle |
| `↑` / `↓` | Previous / next line |

While the text box is focused, every single-key shortcut is disabled so typing
never triggers playback. Only `Ctrl+Enter` still commits.

## Mouse

| Action | Result |
|---|---|
| Left click on waveform | Set the start time of the selected line |
| Right click on waveform | Set the end time of the selected line |
| Drag within ±8 px of the red/blue line | Fine-tune that edge live |
| Left-drag elsewhere | Pan the view |
| Scroll wheel | Zoom horizontally, anchored at the cursor |
| `Ctrl` + scroll wheel | Vertical gain (0.5×–5×), synced to the right slider |

## Touch (tablet mode)

Tablet mode turns on automatically when `pointer: coarse` and the viewport is
narrower than 1024 px; toggle it manually with the **📱 平板** button.

| Gesture | Result |
|---|---|
| Single tap | Set the start time |
| Double tap (within 300 ms) | Set the end time |
| Single drag on empty space | Pan the view |
| Drag near a marker line | Fine-tune that edge |
| Pinch | Zoom around the midpoint of the two fingers |

Nine on-screen buttons cover the actions that would otherwise need a keyboard:
pan, zoom, insert, play, play-last-500 ms, commit, and undo.

## Features

- **Waveform** — `decodeAudioData` renders a min/max envelope on Canvas,
  with a live playhead driven by `requestAnimationFrame`.
- **Timeline** — 1 s to 300 s visible range, cursor-anchored wheel zoom,
  pinch zoom, and adaptive ruler ticks.
- **SRT import** — UTF-8, tolerant of CRLF, BOM, missing indices, multi-line
  text, and `.` as the millisecond separator. Lines are re-sorted by start time.
- **SRT export** — standard UTF-8 with LF line endings and renumbered indices.
- **Text editing** — a multi-line textarea wired to the list and CPS readout
  in real time.
- **Subtitle list** — `# / start / end / CPS / text` grid with zebra striping,
  selected-row highlight, event-delegated clicks, and auto-resort on time
  changes.
- **CPS warnings** — characters per second, excluding whitespace. Above 20 turns
  yellow, above 25 turns red.
- **Undo** — snapshot stack, depth 100, covering timing, text, insert, and
  delete operations.
- **Dark mode** — always on, by design.

## Export behaviour by platform

The export path degrades gracefully so that no platform is ever left with a
dead button:

- **Desktop / Android Chrome** — direct `Blob` download.
- **iOS (Safari and Chrome)** — the direct download path crashes the tab on
  some iOS versions, so an export modal opens instead with three options:
  copy all, share/save, and download. If `navigator.share({files})` is
  unavailable it falls back to `share({text})`, then to a new tab the user can
  save from manually.

Clipboard writes always go through `navigator.clipboard.writeText()` with a
raw string (LF-only, never read back from the DOM), with a temporary-textarea
fallback. This avoids the doubled blank lines that WebKit's `execCommand`
serialization causes when pasting into Notes, WeChat, or Word.

## Known limitations

- Audio is decoded entirely in memory, so files over an hour are heavy.
- The subtitle list is not virtualized and may stutter above ~500 rows.
- Waveform is mono; stereo detail is not shown.
- No FFT spectrum view.
- No drag-to-reorder or column sorting.
- No redo, and no recent-files list (both are browser-sandbox constrained).
- SRT only — ASS/SSA, styling, and word-level karaoke are out of scope, as are
  video, translation, and speech recognition.

## Browser support

Desktop Chrome, Edge, Firefox, and Safari; iPadOS 15+ Safari and Chrome;
Android Chrome; HarmonyOS browsers. See the compatibility matrix in
`設計文件.txt` for per-platform details.

---

# 繁體中文

## 快速開始

不需要安裝、不需要伺服器、不需要建置。

1. 以 Chrome、Edge、Firefox 或 Safari 開啟 `音頻字幕編輯器.html`。
2. 點擊 **📂 音頻** 選擇音頻檔（`audio/*`，即 mp3、wav、m4a、ogg，
   以及瀏覽器可解碼時的 flac）。
3. 可選擇性點擊 **📄 SRT** 載入既有字幕檔。
4. 點擊 **📤 匯出** 存檔。

編輯器啟動時會載入 4 行示範字幕，方便在載入素材前先熟悉打軸手感。

## 鍵盤快捷鍵（桌面模式）

| 按鍵 | 功能 |
|---|---|
| `S` / `Space` | 播放選中行 |
| `D` | 播放該行最後 500 毫秒（不足則播放整行） |
| `G` / `Ctrl+Enter` | 提交並跳到下一行 |
| `A` / `F` | 視圖左移 / 右移 30% |
| `Z` / `Ctrl+Z` | 撤銷（最多 100 步） |
| `Ctrl+I` | 在選中行之後插入空白字幕 |
| `Delete` | 刪除選中行 |
| `↑` / `↓` | 上一行 / 下一行 |

文字框獲得焦點時，所有單鍵快捷鍵一律失效，避免打字誤觸發播放；
此時仍可用 `Ctrl+Enter` 提交。

## 滑鼠操作

| 操作 | 結果 |
|---|---|
| 左鍵點擊波形 | 設定選中行的開始時間 |
| 右鍵點擊波形 | 設定選中行的結束時間 |
| 在紅／藍線 ±8px 內拖曳 | 即時微調該端點 |
| 在其他位置左鍵拖曳 | 平移視圖 |
| 滾輪 | 以游標為錨點水平縮放 |
| `Ctrl` + 滾輪 | 垂直增益（0.5×–5×），與右側滑桿同步 |

## 觸控（平板模式）

當裝置符合 `pointer: coarse` 且視窗寬度小於 1024px 時，平板模式會自動開啟；
也可透過 **📱 平板** 按鈕手動切換。

| 手勢 | 結果 |
|---|---|
| 單指輕觸 | 設定開始時間 |
| 雙擊（300 毫秒內） | 設定結束時間 |
| 空白處單指拖曳 | 平移視圖 |
| 標線附近拖曳 | 微調該端點 |
| 雙指捏合 | 以兩指中心為錨點縮放 |

九個螢幕按鈕涵蓋了原本需要鍵盤的操作：平移、縮放、插入、播放、
播放最後 500 毫秒、提交、撤銷。

## 核心功能

- **波形** — 以 `decodeAudioData` 解碼後在 Canvas 繪製 min/max 包絡，
  白色虛線播放頭由 `requestAnimationFrame` 驅動。
- **時間軸** — 可視範圍 1 秒至 300 秒，游標錨點滾輪縮放、雙指縮放，
  刻度間隔依視窗寬度自動調整。
- **SRT 匯入** — UTF-8，容錯 CRLF、BOM、缺序號、多行文本，以及以 `.`
  作為毫秒分隔符；解析後依開始時間重新排序。
- **SRT 匯出** — 標準 UTF-8、LF 換行、序號自動重排。
- **文字編輯** — 多行 textarea，即時同步字幕清單與 CPS 數值。
- **字幕清單** — `# / 開始 / 結束 / CPS / 文本` 網格，斑馬紋、選中高亮、
  事件委派點擊，時間變更後自動重排且選中行跟隨移動。
- **CPS 警告** — 去除空白後每秒字元數，超過 20 轉黃、超過 25 轉紅。
- **撤銷** — 快照堆疊，深度 100，涵蓋時間、文本、插入與刪除操作。
- **暗黑模式** — 全域強制開啟，設計上不提供開關。

## 跨平台匯出行為

匯出路徑會逐級降級，確保任何平台都不會出現「按了沒反應」：

- **桌面 / Android Chrome** — 直接以 `Blob` 下載。
- **iOS（Safari 與 Chrome）** — 部分 iOS 版本上直接下載會導致分頁崩潰，
  因此改為開啟匯出彈窗，提供「複製全部 / 分享儲存 / 下載檔案」三途徑。
  若 `navigator.share({files})` 不支援，則降級為 `share({text})`，
  再降級為開啟新分頁由使用者手動儲存。

剪貼簿一律以 `navigator.clipboard.writeText()` 寫入原始字串
（純 LF，不從 DOM 讀回），並備有臨時 textarea 降級方案。
這可避免 WebKit 的 `execCommand` 序列化導致貼到備忘錄、微信或 Word 時
每行之間多出空行的問題。

## 已知限制

- 音頻需整檔解碼至記憶體，超過一小時的檔案會有壓力。
- 字幕清單未做虛擬化，超過約 500 行可能卡頓。
- 波形為單聲道繪製，不顯示立體聲細節。
- 無 FFT 頻譜模式。
- 無拖放排序與欄位排序。
- 無重做（Redo）與最近檔案清單（受瀏覽器沙盒限制）。
- 僅支援 SRT；不含 ASS/SSA、樣式與逐字卡拉 OK，亦不處理影片、
  翻譯與語音辨識。

## 瀏覽器支援

桌面 Chrome、Edge、Firefox、Safari；iPadOS 15+ Safari 與 Chrome；
Android Chrome；HarmonyOS 瀏覽器。各平台細節請見 `設計文件.txt`
的相容性矩陣。

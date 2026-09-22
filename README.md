大部分代码与以下均为AI生成，本人负责构建流程和提供思路

留牌阶段的识牌与策略计算来自项目https://github.com/Oreki0504/hololive-dreams-helper

基於https://github.com/mwty-0415/Hololive-Dreams-Auto-High-Low開發和測試一些亂七八糟的功能
# Hololive Dreams Auto Bot

[简体中文](#-简体中文) | [繁體中文](#-繁體中文) | [English](#-english) | [日本語](#-日本語)

---

## 🇨🇳 简体中文

专为《Hololive Dreams》小游戏设计的全自动挂机与策略决策工具，集成智能留牌算法、高低牌动态算牌及多语言 UI[cite: 1, 2]。

### 三阶段翻倍策略

第一、第三阶段持续翻倍，直到游戏自动结算；第二阶段在本局开始时按起手奖金确定成功次数，随后只按确认成功的次数决定收手。例如 200 起手成功 5 次得到 6,400，700 起手成功 3 次得到 5,600。平手与重复画面不计数，失败重试同一阶段，成功入账才推进。原版仍为默认策略。[详细规则](THREE_STAGE.md#zh-cn)。

### ✨ 核心特性
- **最优留牌计算**：基于 Numba JIT 高性能加速，自动评估起手五张牌并计算期望收益最高的保留组合[cite: 2]。
- **动态算牌记牌**：内置 High-Low 记牌引擎，根据剩余牌堆实时计算当前最高胜率分支[cite: 2]。
- **风控止盈与极限冲刺**：
  - **垫刀期**：胜率偏低时主动收手提现，确保单日收益平稳累积[cite: 2]。
  - **冲刺期**：金币达 19,800 后自动解除风控，以追求单笔 10,000+ 巨额奖金为目标发起冲刺[cite: 2]。
- **收支监控**：自动记录失败轮次与门票扣除（50/局），实时核算净利润[cite: 1, 2]。
- **多语言界面**：原生支持简体中文、繁體中文、English 及 日本語[cite: 1]。
- **全局快捷键**：支持自定义全局停止热键（默认 `INSERT`），挂机时随时安全接管[cite: 1]。

### 🛠️ 源码运行
```bash
git clone [https://github.com/你的用户名/你的仓库名.git](https://github.com/你的用户名/你的仓库名.git)
cd 你的仓库名
pip install -r requirements.txt
python main_ui.py
```

### 🚀 打包为独立执行程序 (.exe)

```powershell
python -m pip install -r requirements.txt pyinstaller
python -m PyInstaller -y "Hololive Dreams-Auto.spec"
```

请在仓库根目录运行以上命令。仓库内的 `Hololive Dreams-Auto.spec` 会自动打包 `templates/`、背景、图标及所需模型，无需手动复制资源。输出位于 `dist/Hololive Dreams-Auto/`，请保留整个文件夹（包括 `_internal/`），不要单独移动 EXE。


### 📖 使用说明
1. 启动游戏并保持游戏窗口未完全最小化（支持后台遮挡，但不可最小化至任务栏）[cite: 2]。
2. 打开辅助工具，按需配置语言与快捷键[cite: 1]。
3. 点击 **「启动挂机」** 开始自动化运行[cite: 1]。
4. 任何时候按下设定的停止快捷键均可安全关停[cite: 1]。

> 兼容性说明：程序会精确匹配 `hololive-Dreams` 游戏窗口，支持 Windows 显示缩放、多显示器和其它窗口遮挡。执行鼠标点击时游戏会短暂置于前台，这是游戏接收输入所必需的。

### ⚠️ 免责声明
- 本工具仅供 Python 编程学习、图像识别技术研究交流使用。
- 请勿用于破坏游戏生态或任何商业盈利场景，因使用本工具造成的任何问题开发者概不负责。

---

## 🇭🇰/🇹🇼 繁體中文

專為《Hololive Dreams》小遊戲設計的全自動掛機與策略決策工具，整合智慧留牌演算法、高低牌動態算牌及多語言 UI[cite: 1, 2]。

### 三階段翻倍策略

第一、第三階段持續翻倍，直到遊戲自動結算；第二階段在本局開始時按起手獎金確定成功次數，之後只按確認成功的次數決定收手。例如 200 起手成功 5 次得到 6,400，700 起手成功 3 次得到 5,600。平手與重複畫面不計數，失敗重試同一階段，成功入帳才前進。原版仍為預設策略。[詳細規則](THREE_STAGE.md#zh-tw)。

### ✨ 核心特色
- **最佳留牌計算**：基於 Numba JIT 高效能加速，自動評估初始五張手牌並計算期望收益最高的保留組合[cite: 2]。
- **動態算牌記牌**：內建 High-Low 算牌引擎，根據剩餘牌堆即時計算當前最高勝率選項[cite: 2]。
- **風控止盈與極限衝刺**：
  - **墊刀期**：勝率偏低時主動收手提現，確保單日代幣在安全線內穩定累積[cite: 2]。
  - **衝刺期**：當代幣達到 19,800 後自動解除風控，鎖定單局 10,000+ 巨額獎金發起衝刺[cite: 2]。
- **收支與淨利監控**：自動記錄失敗次數與入場門票消耗（50/局），即時計算淨利潤[cite: 1, 2]。
- **多語言介面**：原生支援簡體中文、繁體中文、English 及 日本語[cite: 1]。
- **全域快捷鍵**：支援自訂全域停止快捷鍵（預設為 `INSERT`），掛機途中隨時安全接管[cite: 1]。

### 🛠️ 原始碼執行
```bash
git clone [https://github.com/你的用戶名/你的倉庫名.git](https://github.com/你的用戶名/你的倉庫名.git)
cd 你的倉庫名
pip install -r requirements.txt
python main_ui.py
```

### 🚀 打包為獨立執行檔 (.exe)

```powershell
python -m pip install -r requirements.txt pyinstaller
python -m PyInstaller -y "Hololive Dreams-Auto.spec"
```

請在儲存庫根目錄執行以上指令。儲存庫內的 `Hololive Dreams-Auto.spec` 會自動打包 `templates/`、背景、圖示及所需模型，無需手動複製資源。輸出位於 `dist/Hololive Dreams-Auto/`，請保留整個資料夾（包含 `_internal/`），不要單獨移動 EXE。


### 📖 使用說明
1. 開啟遊戲並維持遊戲視窗未被完全最小化（可被其他視窗遮擋，但不可縮小至工作列）[cite: 2]。
2. 開啟本輔助程式，依需求設定語言與停止快捷鍵[cite: 1]。
3. 點擊 **「啟動掛機」** 進入全自動流程[cite: 1]。
4. 任何時候按下設定的停止快捷鍵皆可安全停機[cite: 1]。

### ⚠️ 免責聲明
- 本工具僅供 Python 程式學習、電腦視覺技術研究交流使用。
- 請勿將本工具用於破壞遊戲平衡或任何商業營利用途，使用本程式產生的任何後果開發者概不負責。

---

## 🇺🇸 English

An automated assistant and decision-making bot for the mini-game in *Hololive Dreams*, featuring optimal poker-hand calculation, dynamic High-Low card counting, and a multilingual GUI[cite: 1, 2].

### Three-stage doubling strategy

Stages one and three keep doubling until the game settles automatically. Stage two sets a win-count target from the initial payout, then cashes out by confirmed wins rather than ongoing reward readings: five wins from 200 yields 6,400; three wins from 700 yields 5,600. Ties and repeated frames do not count. Losses retry the same stage; confirmed settlements advance it. Legacy remains the default. [Full rules](THREE_STAGE.md#en).

### ✨ Key Features
- **Optimal Hand Selection**: Powered by Numba JIT acceleration to evaluate initial poker hands and retain the mathematically optimal combination[cite: 2].
- **Dynamic Card Counting**: Tracks remaining cards in the deck during the High-Low game to determine real-time winning probabilities[cite: 2].
- **Smart Risk Control & Sprint Mode**:
  - **Staging Phase**: Automatically cashes out when odds are unfavorable to steadily build up bankroll[cite: 2].
  - **Sprint Phase**: Unlocks aggressive play once total coins reach 19,800, pushing for cashouts of 10,000+ coins in a single run[cite: 2].
- **Profit & Loss Tracking**: Automatically tracks failed runs and ticket fees (50 coins/entry), calculating net profit in real time[cite: 1, 2].
- **Multilingual UI**: Native support for Simplified Chinese, Traditional Chinese, English, and Japanese[cite: 1].
- **Global Stop Hotkey**: Supports customizable hotkeys (default `INSERT`) to safely halt the bot at any point[cite: 1].

### 🛠️ Running from Source
```bash
git clone [https://github.com/your-username/your-repo-name.git](https://github.com/your-username/your-repo-name.git)
cd your-repo-name
pip install -r requirements.txt
python main_ui.py
```

### 🚀 Build Executable (.exe)

```powershell
python -m pip install -r requirements.txt pyinstaller
python -m PyInstaller -y "Hololive Dreams-Auto.spec"
```

Run these commands from the repository root. The included `Hololive Dreams-Auto.spec` automatically bundles `templates/`, backgrounds, icons, and the required models; no manual resource copying is needed. Output is placed in `dist/Hololive Dreams-Auto/`. Keep the entire folder, including `_internal/`, together rather than moving the EXE alone.


### 📖 Instructions
1. Launch the game and ensure the game window is not fully minimized[cite: 2].
2. Open the bot UI and select your preferred language and stop hotkey[cite: 1].
3. Click **"Start Bot"** to begin automation[cite: 1].
4. Press your configured stop hotkey at any time to safely exit the loop[cite: 1].

### ⚠️ Disclaimer
- This project is developed solely for educational, computer vision, and automation research purposes.
- Do not use this tool for commercial purposes or in ways that compromise fair play. The developer assumes no liability for any issues arising from its use.

---

## 🇯🇵 日本語

『Hololive Dreams』のミニゲーム向けに設計された全自動周回・戦略決定支援ツールです[cite: 1, 2]。ポーカーの最適ホールド判定、ハイ＆ロー（High-Low）の動的カウンティング、多言語対応UIを搭載しています[cite: 1, 2]。

### 3段階のダブルアップ戦略

第1・第3段階はゲームが自動精算するまで挑戦します。第2段階は初期報酬から必要成功回数を決め、その後は成功回数だけで精算を判断します。200なら5回で6,400、700なら3回で5,600です。引き分けや重複画面は数えず、敗北時は同じ段階を再試行し、入金確認後に次へ進みます。既定は従来モードです。[詳細ルール（英語）](THREE_STAGE.md#en)。

### ✨ 主な機能
- **ポーカー最適手札計算**：Numba JITによる高速演算で、配られた5枚の手札から期待値が最大となるキープカードを自動選定します[cite: 2]。
- **動的カードカウンティング**：ハイ＆ロー中に残りの山札を追跡し、リアルタイムの勝率に基づき最適な選択（High / Low）を行います[cite: 2]。
- **リスク管理とスプリントモード**：
  - **安定期**：勝率が低い場合は無理をせず利益を確定（ドロップ）し、目標コインまで着実に貯蓄します[cite: 2]。
  - **スプリント期**：累計コインが19,800に達するとリスク制限を解除し、1撃10,000以上の大量獲得を目指して強気に挑戦します[cite: 2]。
- **収支・利益トラッキング**：失敗回数と入場料（1回あたり50コイン）の損失を自動集計し、当日の純利益をリアルタイムで表示します[cite: 1, 2]。
- **多言語対応**：簡体字中国語、繁体字中国語、英語、日本語に対応[cite: 1]。
- **グローバル停止ショートカット**：任意のキー（初期設定：`INSERT`）でいつでも安全に停止できます[cite: 1]。

### 🛠️ ソースコードからの実行
```bash
git clone [https://github.com/ユーザー名/リポジトリ名.git](https://github.com/ユーザー名/リポジトリ名.git)
cd リポジトリ名
pip install -r requirements.txt
python main_ui.py
```

### 🚀 単体実行ファイル (.exe) のビルド

```powershell
python -m pip install -r requirements.txt pyinstaller
python -m PyInstaller -y "Hololive Dreams-Auto.spec"
```

上記のコマンドはリポジトリのルートで実行してください。同梱の `Hololive Dreams-Auto.spec` が `templates/`、背景、アイコン、必要なモデルを自動的に組み込むため、手動コピーは不要です。出力先は `dist/Hololive Dreams-Auto/` です。EXE だけを移動せず、`_internal/` を含むフォルダ全体を保持してください。


### 📖 使用方法
1. ゲームを起動し、ウィンドウが完全に最小化されていない状態にします（他ウィンドウの背面に隠れていても動作可能）[cite: 2]。
2. ツールを起動し、言語や停止ショートカットキーを設定します[cite: 1]。
3. **「起動」** ボタンを押すと自動周回が開始されます[cite: 1]。
4. 途中で停止したい場合は、設定した停止キーを押すと安全に終了します[cite: 1]。

### ⚠️ 免責事項
- 本ツールはPythonプログラミング、画像認識、および自動化技術の研究・学習を目的として作成されています。
- 本ツールを不正目的や商用目的で使用することを禁止します。本ツールの利用によって生じたいかなる損害についても、開発者は責任を負いません。

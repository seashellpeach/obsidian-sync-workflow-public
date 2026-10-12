# Obsidian 同步流程

這份 Skill 可安裝在 Codex 或 Claude，協助你把選定的專案檔案同步到自己的 Obsidian Vault（筆記庫）。第一次使用時，它會用白話帶你確認要同步的資料夾、Vault、Vault 裡的存放位置、同步哪些檔案，以及何時同步。

每個人都使用自己的專案資料夾、Vault 和設定。下載的 Skill 安裝後，不必再手動搬到其他資料夾；要同步的專案資料也可以留在電腦原本的位置。

## 這個 Skill 會怎麼協助你

第一次設定時，它會：

1. 先確認要使用目前開啟的專案，還是你想選另一個資料夾。
2. 先幫你找找 Obsidian 筆記庫，再請你選要用哪一個，以及副本要放在筆記庫的哪個資料夾。
3. 查看少量專案概況與檔案清單，推薦同步內容，並主動建議每次完成並確認成果時同步；你也可以選擇里程碑同步或手動同步。
4. 列出完整方案，包含來源、目的地、檔案、排除內容、同步時機和版本方式。
5. 等你確認後，才建立設定或複製檔案。

你不必先懂技術名詞，也不用自己規劃檔案清單。你可以說「我不確定，請推薦」，或直接描述想保留哪些內容。若目前介面無法選擇資料夾或確認 Vault，Skill 會一步步告訴你怎麼找到；它不會為了找資料而掃描整台電腦。

## 安裝 Skill

### Codex

下載 [Codex 安裝檔](downloads/obsidian-sync-workflow.skill)，再把下載好的檔案拖曳到 Codex 視窗，依照畫面提示完成安裝。

安裝完成後，在 Codex 新對話輸入 `$obsidian-sync-workflow`，或直接描述你想做的 Obsidian 同步工作。若 Codex 還沒有顯示這份 Skill，重新啟動 Codex 再確認。[Codex Skills 說明](https://learn.chatgpt.com/docs/build-skills)

### Claude

下載 [Claude 安裝檔](downloads/obsidian-sync-workflow-claude.zip)，在 Claude 開啟 **自訂（Customize）→ Skills → ＋ → Create skill → Upload a skill**，選擇下載的 ZIP，再把這份 Skill 開啟。

如果 Claude 裡沒有 Skills 選項，先到 **Settings → Capabilities** 開啟 **Code execution and file creation**。學校或機構帳號若仍看不到上傳選項，請詢問帳號管理者。[Claude Skills 官方說明](https://support.claude.com/en/articles/12512180-use-skills-in-claude)

## 開始使用

在 Codex 或 Claude 開啟新對話，貼上這段：

> 我是第一次設定 Obsidian 同步，請用 Obsidian 同步流程 Skill 帶我一步一步完成。先問我想同步哪個專案或資料夾；如果我不熟悉路徑，請優先用資料夾選擇功能帶我選，不要一開始就叫我輸入路徑。若目前介面沒有選擇功能，再一步步教我怎麼找到資料夾。接著確認要使用的 Obsidian Vault（筆記庫）和裡面的存放位置。如果我不確定要同步哪些檔案或何時同步，請先看少量專案概況，再用白話推薦一個簡單方案。請主動建議「每次完成並確認一項專案成果時同步」，也讓我選擇在里程碑同步或只在我提出要求時同步；說明日常問答、未完成草稿和整段對話不會自動同步。請列出來源、Obsidian 存放位置、要同步和排除的內容、同步時機，以及舊版本怎麼處理；等我確認完整方案後再建立設定或寫入。之後符合這個專案的同步規則時直接沿用，不要每次再問我。

Codex 也可以直接輸入 `$obsidian-sync-workflow` 開始。Claude 會依照你的描述，在這份 Skill 已開啟時自動使用它。

你也可以用自己的話補充，例如：

- 「只同步完成的成果，草稿先不要。」
- 「專案資料夾在別處，請帶我找到它。」
- 「我不知道要放在 Vault 哪裡，請依專案名稱推薦。」
- 「完成一份正式成果時再同步；先保留舊版本。」
- 「這個專案每次完成並確認成果時同步，日常問答和草稿不要同步。」

後續可以說「請依這個專案已確認的 Obsidian 規則，同步這次完成的成果」。Skill 會沿用你已確認的設定；路徑、檔案或權限有問題時會先停下來說明。

## 同步方式與限制

- **單向複製：**從你選定的來源資料夾複製到 Vault。來源是原始檔，Obsidian 存放閱讀用副本；不會雙向合併變更。
- **只複製你確認的檔案：**不會把整個資料夾的內容全部搬進 Obsidian。
- **衝突時停止：**若來源不見、權限不足，或 Obsidian 裡的副本被另外修改，工具會停止並回報，不會自行覆寫或刪除檔案。
- **依專案規則同步：**首次設定後，完成符合條件的專案成果時會沿用已確認規則，不必每次再確認。單純結束對話不會觸發同步；日常問答、草稿和整段對話也不會自動同步。
- **會維護索引頁：**同步工具會在 Vault 內建立並更新一頁索引，設定前會把位置和名稱列給你確認。
- **安裝後不用找資料夾放 Skill：**下載後直接依上面的方式安裝即可。完成同步設定時，Skill 會把同步設定保存在你選的專案資料夾旁，不用另外搬動設定檔。
- **如果目前無法讀寫資料夾：**Skill 會先告訴你狀況，不會假裝已完成同步。同步工具需要 Python 3.9 或更新版本，不需另外安裝套件。

## 授權

本 Skill 採用自訂的[限制性非商業使用授權](LICENSE.md)：允許非商業的個人、教學與研究用途，可閱讀、下載、安裝、執行，也可保留安裝和使用所需的副本；不允許商業使用、修改或散布 Skill 檔案。要分享時，請分享原始 GitHub repository 網址。

**公開 GitHub 的限制：**GitHub 規定公開 repository 的使用者可以在 GitHub 站內檢視及 fork。這份自訂授權不會移除 GitHub 服務條款已授予的站內檢視與 fork 權利，也不代表授權在 GitHub 以外修改或散布檔案。若你不能接受任何站內 fork，就不適合把 repository 設為公開。

這是自訂授權，不是 MIT 等標準授權；GitHub 不一定會將它辨識為標準授權類別。更多說明見 [GitHub：為 repository 選擇授權](https://docs.github.com/en/repositories/managing-your-repositorys-settings-and-features/customizing-your-repository/licensing-a-repository) 與 [GitHub 服務條款](https://docs.github.com/en/site-policy/github-terms/github-terms-of-service)。

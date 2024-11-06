# Introduce of Git
---
# 1. 版本控制基礎概念
---
## 1.1 什麼是版本控制？

版本控制是一種記錄檔案修改歷史的系統，可以讓你追蹤文件的變化、回到之前的版本，並且與團隊協作。

想像一下：
- 📝 就像 Word 的修訂功能
- 📸 或者是你幫重要文件定期做的"備份"
- 🎮 類似遊戲的存檔點

### 版本控制系統的基本功能：

1. 記錄修改歷史
2. 支援多人協作
3. 可以回溯先前版本
4. 追蹤每個改動的作者和時間
5. 支援並行開發（分支功能）

## 1.2 為什麼需要版本控制？

### 1.2.1 沒有版本控制時的常見問題：

``` plaintext
project/
  ├── final.py
  ├── final_v2.py
  ├── final_v3.py
  ├── final_FINAL.py
  ├── final_REAL_FINAL.py
  └── final_REAL_FINAL_v2.py
```

![圖片描述](./images/Pasted%20image%2020241104162738.png)
這麼多的final版 到底哪一版才是final?

![圖片描述2](./images/Pasted%20image%2020241104162830.png)
### 1.2.2 版本控制能解決的問題：

1. **追蹤程式碼變更**
    - 誰改了什麼？
    - 什麼時候改的？
    - 為什麼要改？
2. **團隊協作**
    - 多人同時開發不衝突
    - 程式碼整合更容易
    - 減少溝通成本
3. **程式碼品質**
    - 回溯問題版本
    - 進行 Code Review
    - 維護程式碼穩定性
4. **備份與復原**
    - 隨時可以回到先前版本
    - 不怕誤刪重要程式碼
    - 方便進行測試和實驗

## 1.3 Why Git?

### 1.3.1 分散式版本控制系統（如 Git）

**優點：**

1. **離線工作**
    - 本地有完整的版本歷史
    - 不需要持續連網
2. **更好的分支管理**
    - 建立分支速度快
    - 合併操作更靈活
3. **備份優勢**
    - 每個開發者都有完整備份
    - 降低資料遺失風險
4. **速度更快**
    - 大部分操作在本地完成
    - 不需要網路延遲

**缺點：**

- 學習曲線較陡
- 概念較複雜
- 初期設置較繁瑣

### 1.3.2 為什麼選擇 Git？

1. **業界標準**
    - GitHub/GitLab 的普及
    - 大多數開源項目都使用 Git
2. **強大的分支功能**
    - 適合特性開發
    - 方便實驗新功能
3. **完整的生態系統**
    - 豐富的工具支援
    - 大量的學習資源
4. **高效能**
    - 優秀的壓縮算法
    - 快速的分支操作

### 1.3.3 簡單的展示一下Git實際操作

假設我有一個SAP自動登入程式的專案 我寫了一段程式碼 並且已經commit過一次 目前正在主分支"main" 且位於C1的節點上

![圖片描述](./images/Pasted%20image%2020241105113904.png)

我初步完成了這支自動化程式給User做使用後 我要做一個保存紀錄這個完成的版本 所以我又commit了一次

`git commit`

![圖片描述](./images/Pasted%20image%2020241105114110.png)

此時C2節點位置的程式已經給User做使用了 User提出希望還能再新增幾個功能 所以我保持原有的程式繼續給User使用 我另建一個分支做新功能開發

`git checkout -b feature`

![圖片描述](./images/Pasted%20image%2020241105114738.png)

我在今天下班前 完成了其中一個功能 我要做一個儲存且記錄 所以我commit一次

`git commit -m "feat: 添加用戶不需維護帳號密碼的功能"`

![圖片描述](./images/Pasted%20image%2020241105115241.png)

結果隔天突然收到User 說程式有Bug 需要修復 所以我得退回主分支的main 再弄一個分支去修復bug

`git switch main`

`git checkout -b bugfix`

![圖片描述](./images/Pasted%20image%2020241105132121.png)

我修復好bug後 做commit 並切回到主分支 把修復的版本的分支合併到主分支

`git commit -m "fix: 緊急修復bug"`

![圖片描述](./images/Pasted%20image%2020241105132512.png)

`git switch main`

`git merge bugfix --no-ff`

![圖片描述](./images/Pasted%20image%2020241105132613.png)

然後我切回feature分支繼續開發剩下的功能 並完成程式後做commit

`git switch feature`

`git commit -m "feat: 添加自動更新密碼的功能"`

![圖片描述](./images/Pasted%20image%2020241105132819.png)

最後我切回主分支去更新User要求的功能到程式上

`git swtich main`

`git merge feature`

![圖片描述](./images/Pasted%20image%2020241105132946.png)

最後刪除bugfix與feature分支

`git branch -d feature bugfix`

# 2. Git 基礎設置
---
## 2.1 Git 的安裝方式

[Download Git](https://git-scm.com/)

## 2.2 初始設置

### 2.2.1 基本配置
``` bash
# 設置用戶名稱
git config --global user.name "name"

# 設置信箱
git config --global user.email "email"

# 設置預設分支名稱（建議設為 main）
git config --global init.defaultBranch main

# 檢查設置
git config --list
```

### 2.2.2 換行符設置
``` bash
# Windows
git config --global core.autocrlf true

# macOS/Linux
git config --global core.autocrlf input
```

## 2.3 Git 基本工作環境介紹

### 2.3.1 重要的工作區域
``` plaintext
【工作目錄】 -----> 【暫存區】 -----> 【本地倉庫】 -----> 【遠端倉庫】
 Working Dir    Staging Area    Local Repo     Remote Repo
```
![[Pasted image 20241105111143.png]]
### 2.3.2 常用命令列工具

1. **Git Bash** (Windows)
    - 提供類 Unix 環境
    - 支援 Git 命令
    - 包含基本的 Unix 命令
2. **Terminal** (macOS/Linux)
    - 系統內建終端機
    - 直接支援 Git 命令

### 2.3.3 GUI 工具推薦

1. **Git GUI 客戶端**
    - GitHub Desktop
    - GitLab
    - GitKraken
2. **整合式開發環境（IDE）的 Git 支援**
    - VSCode Git 整合
    - IntelliJ IDEA Git 整合

### 2.3.4 建議的工作環境設置

1. **配置 .gitignore**
``` bash
# 創建全局 .gitignore 
git config --global core.excludesfile ~/.gitignore_global
```
	1. 為什麼需要全域 .gitignore？
	.gitignore_global` 是一個全域的忽略檔案清單，讓你可以設定在所有 Git 專案中都要忽略的檔案類型。這非常有用，因為有些檔案是你永遠不想加入版本控制的。
	常見的需要忽略的檔案：
``` plaintext
1. 作業系統產生的檔案
   - Windows: Thumbs.db, Desktop.ini
   - macOS: .DS_Store

2. IDE/編輯器的設定檔
   - .vscode/
   - .idea/
   - *.swp (vim)

3. 編譯產生的檔案
   - *.class (Java)
   - *.pyc (Python)
   - node_modules/ (Node.js)

4. 個人設定檔
   - .env
   - config.local.json
```
	2. 設置步驟
		1. 建立全域 .gitignore
``` bash
# Windows (在 Git Bash 中)
touch ~/.gitignore_global

# 或用 Windows 命令提示字元
echo. > %USERPROFILE%\.gitignore_global
```
		2. 設定 Git 使用這個檔案
``` bash
git config --global core.excludesfile ~/.gitignore_global
```
		3. 編輯檔案內容
``` plaintext
# OS generated files
.DS_Store
.DS_Store?
._*
.Spotlight-V100
.Trashes
ehthumbs.db
Thumbs.db

# IDE files
.idea/
.vscode/
*.swp
*.swo

# Compiled files
*.class
*.pyc
*.pyo
*.pyd
__pycache__/

# Dependencies
node_modules/
vendor/

# Environment files
.env
.env.local
*.local.json

# Log files
*.log
npm-debug.log*
yarn-debug.log*
yarn-error.log*

# Build output
/dist
/build
/out
```
	3. 與專案的 .gitignore 的區別
``` plaintext
.gitignore_global （全域）
    └── 適用於所有專案
    └── 通常是個人開發環境相關
    └── 作業系統/IDE/編輯器產生的檔案

.gitignore （專案）
    └── 只適用於特定專案
    └── 專案相關的忽略規則
    └── 依賴項目/建置產出/暫存檔案
```
	4. 實際案例
	假設我是一個Full Stack，使用多種工具：
``` plaintext
# ~/.gitignore_global

# 編輯器
.vscode/
.idea/
*.sublime-project
*.sublime-workspace

# macOS
.DS_Store
.AppleDouble
.LSOverride

# Windows
Thumbs.db
Desktop.ini

# Node.js
node_modules/
npm-debug.log
yarn-error.log

# Python
__pycache__/
*.py[cod]
venv/
.env

# Java
*.class
target/
.settings/
.classpath
.project
```
	5. 檢查設置是否生效
``` bash
# 查看全域 gitignore 設置
git config --global core.excludesfile

# 測試特定檔案是否會被忽略
git check-ignore -v filename.ext
```
**優點：**
	1. 不用在每個專案重複設定相同的忽略規則
	2. 保持專案的 .gitignore 檔案簡潔
	3. 避免意外提交個人環境檔案
	4. 團隊成員可以有各自的忽略規則

2. **設置 SSH 金鑰**（用於 GitHub）
``` bash
# 生成 SSH 金鑰
ssh-keygen -t ed25519 -C "your_email@example.com"

# 查看公鑰內容
cat ~/.ssh/id_ed25519.pub
```

# 3. Git 核心概念
---
## 3.1 Git 的三個區域

讓我用一個簡單的圖來說明三個主要區域：
``` plaintext
【工作區】         【暫存區】         【版本庫】
  (1)               (2)               (3)
你的項目目錄  ->  git add 後  ->  git commit 後
實際檔案      ->  暫存的變更  ->  永久的記錄
```
### 3.1.1 工作區（Working Directory）

- 你實際編輯檔案的地方
- 就是你在檔案系統看到的目錄
- 例如：
``` plaintext
project/
├── src/
│   └── main.js
├── docs/
│   └── readme.md
└── package.json
```
### 3.1.2 暫存區（Staging Area）

- 又稱為「索引」（Index）
- 存放 "準備提交" 的變更
- 是一個中間狀態
- 允許你選擇性地提交變更

### 3.1.3 版本庫（Repository）

- 存放所有提交的歷史記錄
- 位於 `.git` 目錄下
- 包含完整的版本歷史
- 可以被推送到遠端

## 3.2 Git 的檔案狀態

### 3.2.1 Untracked（未追蹤）

- Git 不知道這個檔案的存在
- 新建的檔案預設是這個狀態
- 例如：
``` bash
# 新建一個檔案
touch newfile.txt

# Git 狀態會顯示
$ git status
Untracked files:
  newfile.txt
```

### 3.2.2 Tracked（已追蹤）

檔案有三種狀態：

1. **Modified（已修改）**
    - 檔案已經被修改但還未暫存
``` bash
# 修改一個檔案
echo "new content" > file.txt

# Git 狀態
$ git status
Changes not staged for commit:
  modified: file.txt
```
2. **Staged（已暫存）**
	- 修改已經被標記為下次提交的一部分
``` bash
# 將修改加入暫存區
git add file.txt

# Git 狀態
$ git status
Changes to be committed:
  modified: file.txt
```
3. **Committed（已提交）**
	- 檔案已經安全地存放在本地資料庫中
``` bash
# 提交修改
git commit -m "Update file.txt"

# Git 狀態
$ git status
nothing to commit, working tree clean
```

## 3.3 檔案狀態的轉換
``` plaintext
Untracked ──git add──→ Staged
     ↑                    │
     │                    │
     │                git commit
     │                    │
     │                    ↓
Modified ←──修改──── Committed
```

## 3.4 常用命令與狀態查看
``` bash
# 查看當前狀態
git status

# 簡短格式顯示狀態
git status -s

# 查看未暫存的變更
git diff

# 查看已暫存的變更
git diff --staged

# 提交變更
git commit -m "提交說明"
```

## 3.5 實際案例
``` bash
# 1. 建立新檔案（Untracked）
touch example.txt

# 2. 加入追蹤（Staged）
git add example.txt

# 3. 修改檔案（Modified）
echo "Hello" > example.txt

# 4. 再次暫存（Staged）
git add example.txt

# 5. 提交（Committed）
git commit -m "Add example.txt with content"
```

# 4. Git 基本操作命令

## 4.1 創建版本庫：`git init`
``` bash
# 在當前目錄初始化 Git 倉庫
git init

# 初始化並創建新目錄
git init my-project

# 初始化後會產生:
my-project/
└── .git/          # Git 倉庫資料
    ├── HEAD       # 指向當前分支
    ├── config     # 倉庫配置
    ├── objects/   # Git 物件
    └── refs/      # 分支和標籤
```

## 4.2 查看狀態：`git status`
``` bash
# 完整狀態
git status

# 簡潔模式
git status -s  # 或 --short

# 輸出示例：
 M README.md      # 已修改未暫存
MM main.js        # 已修改且部分已暫存
A  new-file.txt   # 新增到暫存區
?? untracked.txt  # 未追蹤
```

## 4.3 添加文件：`git add`
``` bash
# 添加特定檔案
git add filename.txt

# 添加特定類型檔案
git add *.js

# 添加目錄
git add src/

# 添加所有變更
git add .

# 互動式添加
git add -i

# 部分添加
git add -p filename.txt  # 可以選擇性地暫存檔案的部分內容
```

## 4.4 提交更改：`git commit`
``` bash
# 基本提交
git commit -m "提交說明"

# 詳細提交訊息
git commit
# 會開啟編輯器，輸入多行訊息

# 添加並提交
git commit -am "直接提交已追蹤的檔案"

# 修改最後一次提交
git commit --amend

# 空提交
git commit --allow-empty -m "Empty commit"
```

## 4.5 查看歷史：`git log`
``` bash
# 基本日誌
git log

# 單行顯示
git log --oneline

# 圖形化顯示
git log --graph

# 顯示差異
git log -p

# 最近 N 個提交
git log -n 5

# 漂亮的格式化輸出
git log --pretty=format:"%h - %an, %ar : %s"
```

## 4.6 基本工作流程示例

### 情境一：新建專案
``` bash
# 1. 創建專案目錄
mkdir my-project
cd my-project

# 2. 初始化 Git
git init

# 3. 創建初始檔案
echo "# My Project" > README.md

# 4. 添加到暫存區
git add README.md

# 5. 初始提交
git commit -m "Initial commit"
```

### 情境二：修改現有檔案
``` bash
# 1. 修改檔案
echo "新內容" >> README.md

# 2. 查看變更
git status
git diff README.md

# 3. 暫存變更
git add README.md

# 4. 提交變更
git commit -m "Update README.md"
```

### 情境三：多檔案作業
``` bash
# 1. 創建多個檔案
touch file1.txt file2.txt

# 2. 修改檔案
echo "內容1" > file1.txt
echo "內容2" > file2.txt

# 3. 查看狀態
git status

# 4. 選擇性添加
git add file1.txt
git commit -m "Add file1"

git add file2.txt
git commit -m "Add file2"
```

## 4.7 常見問題與解決
``` bash
# 取消暫存
git restore --staged <file>

# 放棄修改
git restore <file>

# 查看特定提交
git show <commit-hash>

# 查看檔案歷史
git log --follow <file>
```

## 4.8 良好的提交習慣

1. **提交訊息格式**
``` bash
# 好的提交訊息格式
git commit -m "feat: add user authentication"
git commit -m "fix: resolve login bug"
git commit -m "docs: update README"
```
2. **適當的提交大小**
	- 每個提交應該是一個邏輯單位
	- 相關的改動放在同一個提交
	- 不相關的改動分開提交

# 5. Git 分支管理
---
## 5.1 分支的概念與用途

分支就像是開發時的平行宇宙，可以讓多個功能同時開發而不互相影響。
``` plaintext
master/main
    ├── feature-1
    ├── feature-2
    └── hotfix
```
**主要用途：**
1. 功能開發（Feature）
2. 問題修復（Hotfix）
3. 版本發布（Release）
4. 實驗性功能（Experimental）

## 5.2 基本分支操作

### 5.2.1 創建分支
``` bash
# 查看所有分支
git branch

# 創建新分支
git branch feature-login

# 創建並切換到新分支
git checkout -b feature-login
# 或
git switch -c feature-login

# 從特定提交創建分支
git branch feature-login <commit-hash>
```

### 5.2.2 切換分支
``` bash
# 使用 checkout
git checkout feature-login

# 使用 switch（更新的命令）
git switch feature-login

# 切換回上一個分支
git checkout -
```

### 5.2.3 合併分支
``` bash
# 1. 切換到目標分支（通常是 main/master）
git checkout main

# 2. 合併其他分支
git merge feature-login

# 快轉合併（Fast-forward）
git merge --ff feature-login

# 創建合併提交
git merge --no-ff feature-login

# 取消合併
git merge --abort
```

## 5.3 分支管理策略

### 5.3.1 Feature Branch Workflow
``` plaintext
main
 ├── feature-1
 │    └── 開發新功能
 └── feature-2
      └── 開發另一功能
```
步驟：
``` bash
# 1. 創建功能分支
git checkout -b feature-login

# 2. 開發功能
git add .
git commit -m "Add login form"

# 3. 更新主分支
git checkout main
git pull

# 4. 合併功能
git merge feature-login
```

### 5.3.2 Gitflow Workflow
``` plaintext
master
 ├── develop
 │   ├── feature-1
 │   └── feature-2
 ├── release-1.0
 └── hotfix-1.0.1
```

**主要分支：**
- `master`：穩定版本
- `develop`：開發版本
- `feature/*`：新功能
- `release/*`：版本準備
- `hotfix/*`：緊急修復
``` bash
# 創建開發分支
git checkout -b develop master

# 創建功能分支
git checkout -b feature/login develop

# 完成功能
git checkout develop
git merge --no-ff feature/login

# 準備發布
git checkout -b release/1.0 develop

# 發布到主分支
git checkout master
git merge --no-ff release/1.0
```

## 5.4 解決衝突

當兩個分支修改了同一個檔案的同一部分時，會產生衝突。

### 5.4.1 衝突標記
``` plaintext
<<<<<<< HEAD
我的修改
=======
其他人的修改
>>>>>>> feature-branch
```

### 5.4.2 解決步驟
``` bash
# 1. 合併時遇到衝突
git merge feature-branch
Auto-merging file.txt
CONFLICT (content): Merge conflict in file.txt

# 2. 查看衝突檔案
git status

# 3. 編輯解決衝突
# 手動編輯檔案，選擇要保留的內容

# 4. 標記為已解決
git add file.txt

# 5. 完成合併
git commit -m "Resolve merge conflict"
```

### 5.4.3 衝突解決工具
``` bash
# 使用工具解決衝突
git mergetool

# 配置 VS Code 為合併工具
git config --global merge.tool vscode
```

## 5.5 分支管理最佳實踐

1. **命名規範**
``` bash
feature/login     # 功能分支
hotfix/bug-123    # 修復分支
release/v1.0.0    # 發布分支
```
2. 分支清理
``` bash
# 刪除已合併分支
git branch -d feature-login

# 強制刪除分支
git branch -D feature-login

# 查看已合併分支
git branch --merged

# 查看未合併分支
git branch --no-merged
```
3. 遠端分支操作
``` bash
# 推送分支
git push origin feature-login

# 刪除遠端分支
git push origin --delete feature-login

# 追蹤遠端分支
git checkout -b feature-login origin/feature-login
```

# 6. Git 遠端操作
---
## 6.1 什麼是 GitHub？
GitHub 是最大的 Git 代碼託管平台，提供：

1. **代碼託管**：儲存和管理代碼
2. **協作功能**：Pull Request, Issues
3. **CI/CD**：自動化測試和部署
4. **專案管理**：Project Boards, Milestones
5. **社交功能**：Follow, Star, Fork

## 6.2 創建 GitHub 帳號

1. **註冊步驟**
    - 訪問 github.com
    - 填寫用戶名、郵箱、密碼
    - 驗證郵箱
    - 選擇計劃（免費/付費）
2. **設置個人資料**
    - 添加頭像
    - 填寫個人簡介
    - 設置公開資訊

## 6.3 添加 SSH Key
``` bash
# 1. 生成 SSH 密鑰
ssh-keygen -t ed25519 -C "your_email@example.com"

# 2. 啟動 ssh-agent
eval "$(ssh-agent -s)"

# 3. 添加私鑰
ssh-add ~/.ssh/id_ed25519

# 4. 複製公鑰
cat ~/.ssh/id_ed25519.pub
# 或在 Windows
clip < ~/.ssh/id_ed25519.pub

# 5. 添加到 GitHub
# GitHub -> Settings -> SSH and GPG keys -> New SSH key
```

## 6.4 遠端操作基礎

### 6.4.1 git remote
``` bash
# 查看遠端倉庫
git remote -v

# 添加遠端倉庫
git remote add origin git@github.com:username/repo.git

# 修改遠端倉庫
git remote set-url origin new-url

# 移除遠端倉庫
git remote remove origin

# 重命名遠端倉庫
git remote rename origin upstream
```

### 6.4.2 git push
``` bash
# 推送到遠端
git push origin main

# 首次推送並設置上游分支
git push -u origin main

# 強制推送（謹慎使用！）
git push --force origin main

# 推送標籤
git push origin --tags

# 刪除遠端分支
git push origin --delete feature-branch
```

### 6.4.3 git pull
``` bash
# 拉取並合併變更
git pull origin main

# 指定合併策略
git pull --rebase origin main

# 只拉取特定分支
git pull origin feature-branch

# 拉取所有分支
git pull --all
```

### 6.4.4 git fetch
``` bash
# 獲取遠端更新
git fetch origin

# 獲取所有分支
git fetch --all

# 獲取並清理已刪除的遠端分支
git fetch --prune

# 獲取特定分支
git fetch origin feature-branch
```

## 6.5 遠端分支管理

### 6.5.1 基本操作
``` bash
# 查看遠端分支
git branch -r

# 查看所有分支
git branch -a

# 切換到遠端分支
git checkout -b feature origin/feature

# 追蹤遠端分支
git branch --track feature origin/feature
```

### 6.5.2 同步策略
``` bash
# 1. 更新本地分支
git checkout main
git fetch origin
git merge origin/main

# 2. 推送本地變更
git add .
git commit -m "Update"
git push origin main
```

### 6.5.3 常見工作流程

1. **克隆專案**
``` bash
# 克隆倉庫
git clone git@github.com:username/repo.git

# 進入專案目錄
cd repo
```
2. 創建功能分支
``` bash
# 創建並切換到新分支
git checkout -b feature-login

# 推送到遠端
git push -u origin feature-login
```
3. 同步遠端變更
``` bash
# 獲取遠端更新
git fetch origin

# 合併主分支更新
git checkout feature-login
git merge origin/main
```
4. 提交變更
``` bash
# 添加和提交變更
git add .
git commit -m "Add login feature"

# 推送到遠端
git push origin feature-login
```
### 6.5.4 常見問題處理

1. **推送被拒絕**
``` bash
# 先拉取更新
git pull origin main

# 解決衝突後再推送
git push origin main
```
2. 分支落後遠端
``` bash
# 使用 rebase
git pull --rebase origin main

# 或使用合併
git pull origin main
```
3. 清理本地分支
``` bash
# 清理已合併的本地分支
git branch --merged | grep -v "\*" | xargs -n 1 git branch -d

# 清理已刪除的遠端分支
git remote prune origin
```

# 7. Git & GitHub 協作流程
---
## 7.1 Pull Request (PR) 工作流程

### 7.1.1 基本 PR 流程
``` plaintext
Fork -> Clone -> Branch -> Modify -> Push -> PR -> Review -> Merge
```
1. **Fork 專案**
	- 點擊 GitHub 專案頁面的 "Fork" 按鈕
	- 在自己的帳號下創建副本
2. 設置本地環境
``` bash
# 克隆你的 fork
git clone git@github.com:YOUR_USERNAME/project.git

# 添加上游倉庫
git remote add upstream git@github.com:ORIGINAL_OWNER/project.git

# 創建功能分支
git checkout -b feature-name
```
3. 提交 PR
``` bash
# 提交更改
git add .
git commit -m "Add feature"
git push origin feature-name

# 到 GitHub 創建 PR
# 填寫 PR 描述
# 選擇目標分支
```

### 7.1.2 PR 模板範例
``` markdown
## 描述
簡短描述這個 PR 的目的

## 變更內容
- 添加了登入功能
- 修復了註冊頁面的 bug
- 更新了使用者文檔

## 測試
- [ ] 單元測試已通過
- [ ] 手動測試已完成
- [ ] 文檔已更新

## 截圖
如果適用，請添加截圖

## 相關議題
Fixes #123
```

## 7.2 Code Review 最佳實踐

### 7.2.1 提交者準則

1. **PR 準備**
    - 保持變更小且聚焦
    - 提供清晰的描述
    - 包含測試案例
    - 自我檢查代碼
2. **回應 Review**
``` markdown
// 回應評論範例
> 建議使用 async/await
已更新，改用 async/await 實作。

// 請求澄清
@reviewer 能否提供使用範例？
```
### 7.2.2 審查者準則

1. **Review 重點**
    - 代碼邏輯
    - 程式碼風格
    - 測試覆蓋
    - 文檔完整性
2. 評論範例
``` markdown
// 建議性評論
建議考慮使用 Map 代替 Object，可以提升查詢效能。

// 必要性修改
這裡需要添加錯誤處理，避免 undefined 異常。

// 提問
為什麼選擇這種實作方式？是否考慮過其他替代方案？
```

## 7.3 Issue 追蹤

### 7.3.1 Issue 類型

1. Bug Report
2. Feature Request
3. Documentation
4. Question
### 7.3.2 Issue 模板範例
``` markdown
## Bug Report

### 描述問題
簡短清楚地描述 bug

### 重現步驟
1. 前往 '...'
2. 點擊 '....'
3. 滾動到 '....'
4. 發現錯誤

### 預期行為
描述應該發生什麼

### 實際行為
描述實際發生什麼

### 環境
- OS: [例如 Windows]
- Browser: [例如 chrome]
- Version: [例如 22]
```
### 7.3.3 Issue 管理
1. **標籤系統**
    - `bug`: 程式錯誤
    - `feature`: 新功能請求
    - `documentation`: 文檔相關
    - `help wanted`: 需要協助
    - `good first issue`: 適合新手
2. **優先級管理**
    - Critical: 緊急修復
    - High: 重要功能
    - Medium: 一般改進
    - Low: 次要更新

## 7.4 專案管理功能

### 7.4.1 Projects Board
``` plaintext
To Do -> In Progress -> Review -> Done
```
1. **設置專案面板**
    - 自動化工作流程
    - 整合 Issues 和 PRs
    - 追蹤進度
2. **常用欄位**
    - Backlog
    - Sprint Planning
    - In Progress
    - Review
    - Done

### 7.4.2 Milestones

- 設置發布目標
- 追蹤完成進度
- 管理版本發布

### 7.4.3 Actions 自動化
``` yaml
# 範例：自動化測試
name: Tests
on: [push, pull_request]
jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
      - name: Run tests
        run: |
          npm install
          npm test
```
### 7.4.4 團隊協作最佳實踐

1. **分支命名規範**
``` plaintext
feature/login
bugfix/issue-123
hotfix/security-patch
docs/api-update
```
2. 提交訊息規範
``` plaintext
feat: add login functionality
fix: resolve memory leak
docs: update API documentation
test: add unit tests for user service
```
3. **代碼審查清單**
	- [ ]  符合程式碼風格
	- [ ]  包含適當的測試
	- [ ]  文檔已更新
	- [ ]  無安全漏洞
	- [ ]  效能考量

# 8. Git 進階技巧
---
## 8.1 git rebase 使用方法

### 8.1.1 基本 rebase
``` bash
# 基本語法
git rebase <base-branch>

# 例如：將 feature 分支 rebase 到 main
git checkout feature
git rebase main
```

### 8.1.2 互動式 rebase
``` bash
# 互動式 rebase 最近的 N 個提交
git rebase -i HEAD~3

# 常用操作選項：
# pick   = 使用提交
# reword = 修改提交信息
# edit   = 修改提交
# squash = 合併到前一個提交
# drop   = 刪除提交
```
### 8.1.3 rebase 實例
``` bash
# 合併多個提交
git rebase -i HEAD~3

# 範例輸出：
pick abc1234 first commit
squash def5678 second commit
squash ghi9012 third commit

# 解決衝突
git rebase --continue  # 繼續 rebase
git rebase --abort    # 取消 rebase
```
## 8.2 git cherry-pick 選擇性合併

### 8.2.1 基本用法
``` bash
# 選擇單一提交
git cherry-pick <commit-hash>

# 選擇多個提交
git cherry-pick <commit-hash-1> <commit-hash-2>

# 不自動提交
git cherry-pick -n <commit-hash>
```
### 8.2.2 常見使用場景
``` bash
# 將 hotfix 應用到多個分支
git checkout release
git cherry-pick <hotfix-commit>

# 選擇性合併功能
git cherry-pick feature-branch~2..feature-branch
```
## 8.3 git stash 暫存修改

### 8.3.1 基本操作
``` bash
# 暫存修改
git stash

# 帶說明的暫存
git stash save "WIP: working on login feature"

# 查看暫存列表
git stash list

# 應用暫存
git stash apply    # 保留 stash
git stash pop      # 應用並刪除 stash

# 刪除暫存
git stash drop stash@{0}
git stash clear    # 清除所有暫存
```
### 8.3.2 進階 stash
``` bash
# 暫存未追蹤的文件
git stash -u

# 互動式暫存
git stash -p

# 從 stash 創建分支
git stash branch new-branch stash@{0}
```
## 8.4 標籤管理

### 8.4.1 創建標籤
``` bash
# 輕量標籤
git tag v1.0.0

# 附註標籤
git tag -a v1.0.0 -m "Release version 1.0.0"

# 給特定提交打標籤
git tag -a v1.0.0 <commit-hash>
```

### 8.4.2 管理標籤
``` bash
# 列出標籤
git tag
git tag -l "v1.0.*"  # 使用模式匹配

# 查看標籤信息
git show v1.0.0

# 刪除標籤
git tag -d v1.0.0

# 推送標籤
git push origin v1.0.0      # 推送特定標籤
git push origin --tags      # 推送所有標籤
```

## 8.5 Git 鉤子（Hooks）

### 8.5.1 常用鉤子
``` bash
# 位置：.git/hooks/
pre-commit          # 提交前執行
pre-push            # 推送前執行
commit-msg          # 提交訊息檢查
pre-receive         # 服務器端接收前
post-receive        # 服務器端接收後
```

### 8.5.2 pre-commit 範例
``` bash
#!/bin/sh
# .git/hooks/pre-commit

# 運行測試
npm test
if [ $? -ne 0 ]; then
    echo "測試失敗，提交被拒絕"
    exit 1
fi

# 檢查代碼風格
eslint .
if [ $? -ne 0 ]; then
    echo "代碼風格檢查失敗，提交被拒絕"
    exit 1
fi
```

### 8.5.3 commit-msg 範例
``` bash
#!/bin/sh
# .git/hooks/commit-msg

commit_msg=$(cat "$1")
pattern="^(feat|fix|docs|style|refactor|test|chore): .+"

if ! echo "$commit_msg" | grep -qE "$pattern"; then
    echo "提交訊息格式錯誤"
    echo "正確格式：<type>: <description>"
    echo "允許的類型：feat, fix, docs, style, refactor, test, chore"
    exit 1
fi
```

## 8.6 進階技巧最佳實踐

1. **Rebase 使用原則**
    - 不要在公共分支上使用 rebase
    - 用於整理本地提交歷史
    - 保持提交歷史清晰
2. **Cherry-pick 應用場景**
    - 將 hotfix 應用到多個版本
    - 選擇性地合併特定功能
    - 避免大範圍使用
3. **Stash 使用建議**
    - 臨時保存工作進度
    - 切換分支前暫存修改
    - 定期清理不需要的 stash
4. **標籤管理策略**
    - 為每個發布版本打標籤
    - 使用語義化版本號
    - 添加詳細的標籤說明
5. **Hooks 開發指南**
    - 保持鉤子腳本簡單
    - 確保執行效率
    - 添加適當的錯誤處理

# 9. Git 最佳實踐
---
## 9.1 Commit Message 規範

### 9.1.1 基本格式
``` plaintext
<type>(<scope>): <subject>

<body>

<footer>
```
### 9.1.2 Type 類型
``` plaintext
feat:     新功能
fix:      錯誤修復
docs:     文檔更新
style:    代碼格式（不影響代碼運行）
refactor: 重構
test:     測試相關
chore:    構建過程或輔助工具變動
```
### 9.1.3 範例
``` plaintext
# 簡單提交
feat: 添加用戶登入功能

# 完整格式
feat(auth): 添加用戶登入功能

實作了以下功能：
- 密碼加密
- JWT 認證
- 記住我功能

Closes #123
```

## 9.2 .gitignore 文件設置

### 9.2.1 基本規則
``` gitignore
# 忽略特定文件
config.json
secret.key

# 忽略特定類型文件
*.log
*.tmp

# 忽略特定目錄
node_modules/
dist/
.vscode/

# 忽略但保留特定文件
!important.log

# 忽略特定路徑下的文件
logs/*.log
build/temp/*
```
### 9.2.2 常用模板
``` gitignore
# Node.js
node_modules/
npm-debug.log
yarn-error.log

# IDE
.idea/
.vscode/
*.sublime-workspace

# 編譯輸出
dist/
build/
*.class

# 環境文件
.env
.env.local
*.local.json

# 系統文件
.DS_Store
Thumbs.db
```

## 9.3 分支命名規範

### 9.3.1 分支類型
``` plaintext
main/master    # 主分支
develop        # 開發分支
feature/       # 功能分支
hotfix/        # 緊急修復
release/       # 發布分支
bugfix/        # 問題修復
```
### 9.3.2 命名規則
``` plaintext
feature/user-login
feature/JIRA-123-user-profile
hotfix/security-issue
release/v1.2.0
bugfix/login-validation
```

## 9.4 團隊工作流程建議

### 9.4.1 Git Flow
``` plaintext
master
  └── develop
      ├── feature/login
      ├── feature/signup
      └── release/v1.0.0
          └── hotfix/v1.0.1
```

### 9.4.2 工作流程步驟

1. **功能開發**
``` bash
# 創建功能分支
git checkout develop
git checkout -b feature/new-feature

# 完成後合併回 develop
git checkout develop
git merge --no-ff feature/new-feature
```
2. 發布流程
``` bash
# 創建發布分支
git checkout -b release/v1.0.0 develop

# 修復發布問題
git commit -m "fix: last minute fixes"

# 合併到主分支和開發分支
git checkout main
git merge --no-ff release/v1.0.0
git tag -a v1.0.0 -m "Release 1.0.0"
```

## 9.5 常見問題解決方案

### 9.5.1 撤銷操作
``` bash
# 撤銷暫存
git reset HEAD <file>

# 撤銷提交
git reset --soft HEAD^   # 保留修改
git reset --hard HEAD^   # 丟棄修改

# 撤銷發布
git push --delete origin v1.0.0  # 刪除遠端標籤
git tag -d v1.0.0               # 刪除本地標籤
```
### 9.5.2 分支管理問題
``` bash
# 清理已合併分支
git branch --merged | grep -v "\*" | xargs -n 1 git branch -d

# 找回已刪除分支
git reflog
git checkout -b recover-branch <commit-hash>
```
### 9.5.3 合併衝突
``` bash
# 使用工具解決衝突
git mergetool

# 放棄合併
git merge --abort

# 使用特定策略
git merge -X theirs feature-branch
git merge -X ours feature-branch
```
### 9.5.4 效能優化
``` bash
# 倉庫優化
git gc
git prune

# 大文件處理
git lfs track "*.psd"
git lfs migrate import --include="*.psd"
```

### 9.5.5 安全性建議

1. **敏感資料處理**
``` bash
# 移除敏感資料
git filter-branch --force --index-filter \
'git rm --cached --ignore-unmatch config.json' HEAD

# 使用 git-secret 或 git-crypt 加密敏感文件
```
2. 權限控制
``` bash
# 配置 .gitconfig
[core]
    fileMode = true
    sharedRepository = group
```

### 9.5.6 持續整合建議
``` yaml
# GitHub Actions 範例
name: CI
on: [push, pull_request]
jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
      - name: Run tests
        run: |
          npm install
          npm test
      - name: Lint
        run: npm run lint
```


# 10. 統整
---
## 10.1 Git 指令大全
| 操作方法 |                 Git 命令                 |         效果          |           使用情境舉例           |
| :--: | :------------------------------------: | :-----------------: | :------------------------: |
| 初始化  |               `git init`               |    建立新的 Git 儲存庫     |        當你開始一個新專案時使用        |
| 複製專案 |           `git clone <url>`            |     複製遠端儲存庫到本地      |      想要參與開源專案或取得團隊專案時      |
|  新增  |            `git add <file>`            |      將檔案加入暫存區       |         新增了一個功能檔案時         |
|      |              `git add .`               |     將所有變更加入暫存區      |     完成一個功能後要提交所有相關檔案時      |
|  提交  |       `git commit -m "message"`        |     提交變更到本地儲存庫      |      完成一個功能或修復後要記錄變更時      |
|      |       `git commit -am "message"`       |   將add和commit合為一步   | # 只添加修改的檔案 如果是添加的檔案還是要用add |
| 檢視狀態 |              `git status`              |       查看工作區狀態       |      想知道哪些檔案被修改或尚未提交時      |
|  分支  |              `git branch`              |      列出所有本地分支       |       需要確認目前有哪些開發分支時       |
|      |          `git branch <name>`           |        建立新分支        |      要開發新功能或修復 bug 時       |
|      |        `git checkout <branch>`         |       切換到指定分支       |       要開始處理其他功能或修復時        |
|      |            `git branch -a`             |    顯示所有本地和遠端的分支     |                            |
|      |            `git branch -r`             |       顯示遠端分支        |                            |
|      |            `git branch -v`             |    顯示每個分支最後一次提交     |                            |
|      |         `git branch --merged`          |   列出已經合併到當前分支的分支    |       準備清理已完成的功能分支時        |
|      |        `git branch --no-merged`        |   列出尚未合併到當前分支的分支    |        檢查哪些功能還在開發中         |
|      |         `git branch -d <name>`         |      刪除已合併的分支       |         清理已完成的功能分支         |
|      |         `git branch -D <name>`         |    強制刪除分支（即使未合併）    |         放棄某個功能開發時          |
|      |       `git branch -m <newname>`        |       重命名當前分支       |          修正分支名稱時           |
|      |  `git branch -m <oldname> <newname>`   |       重命名指定分支       |         修正其他分支名稱時          |
|      |    `git branch --edit-description`     |      為分支添加描述說明      |          說明分支用途時           |
| 合併分支 |          `git merge <branch>`          |    將指定分支合併到當前分支     |       功能開發完成要合併回主分支時       |
|      |      `git merge --no-ff <branch>`      |      強制創建合併提交       |      合併重要功能分支，保留歷史記錄       |
|      |     `git merge --squash <branch>`      |   將分支的所有變更壓縮成一個提交   |        想要保持主分支歷史整潔時        |
|      |       `git merge <commit-hash>`        |      只合併特定的提交       |          只需要部分功能時          |
|      |          `git merge --abort`           |  取消當前的合併，恢復到合併前狀態   |        解決衝突太複雜想重來時         |
|      |       `git merge -s <strategy>`        |      使用指定的合併策略      |          特殊合併需求時           |
|      |      `git merge -X ours <branch>`      |  合併時衝突優先採用當前分支的更改   |        確定自己的更改更正確時         |
|      |     `git merge -X theirs <branch>`     |  合併時衝突優先採用被合併分支的更改  |        確定對方的更改更正確時         |
|      |    `git merge --no-commit <branch>`    |     進行合併但不自動提交      |          想預覽合併結果時          |
| 刪除檔案 |            `git rm <file>`             | 從 Git 版控和工作目錄中刪除檔案  |       確定要移除不再需要的檔案時        |
|      |        `git rm --cached <file>`        | 只從 Git 版控中刪除，保留實體檔案 |     想保留檔案但不再追蹤時（如設定檔）      |
|      |           `git rm -f <file>`           |  強制刪除已修改或已加入索引的檔案   |       確定要捨棄修改並移除檔案時        |
|      |        `git rm -r <directory>`         |    遞迴刪除整個目錄及其內容     |         要移除整個資料夾時          |
|      |         `git rm *.<extension>`         |    刪除特定副檔名的所有檔案     |        要移除所有特定類型檔案時        |
|      |            `git rm "*.txt"`            |   使用萬用字元刪除符合規則的檔案   |       要移除符合特定模式的檔案時        |
|  查詢  |               `git log`                |       顯示提交歷史        |         查看專案的開發歷史          |
|      |          `git log --oneline`           |      每個提交顯示一行       |          快速瀏覽提交歷史          |
|      |           `git log --graph`            |    顯示分支和合併的圖形化歷史    |          了解分支合併狀況          |
|      |              `git log -p`              |     顯示每次提交的差異內容     |         檢視具體程式碼變更          |
|      |            `git log <file>`            |     顯示特定檔案的修改歷史     |          追蹤檔案的變更           |
|      |       `git log --author="name"`        |      顯示特定作者的提交      |          檢視團隊成員貢獻          |
|      |     `git log --since="2024-01-01"`     |     顯示特定時間後的提交      |          查看近期開發進度          |
|      |            `git log --stat`            |    顯示每次提交的檔案修改統計    |           了解修改範圍           |
|  查看  |               `git show`               |    顯示最近一次提交的詳細內容    |         檢視剛才提交的內容          |
|      |          `git show <commit>`           |     顯示指定提交的詳細內容     |         檢視特定版本的變更          |
|      |       `git show <commit>:<file>`       |     顯示特定版本的檔案內容     |         查看舊版本的檔案內容         |
|      |            `git show <tag>`            |      顯示標籤的詳細資訊      |         查看發布版本的內容          |
|      |           `git show --stat`            |      顯示變更的統計資訊      |          快速了解修改範圍          |
|  標籤  |               `git tag`                |       列出所有標籤        |          檢視所有版本標記          |
|      |          `git tag -l "v1.*"`           |    使用pattern查找標籤    |          查找特定版本系列          |
|      |            `git tag v1.0.0`            |       創建輕量標籤        |          標記小版本更新           |
|      |    `git tag -a v1.0.0 -m "message"`    |      創建帶註解的標籤       |          標記重要版本發布          |
|      |      `git tag -a v1.0.0 <commit>`      |      為特定提交添加標籤      |         補充遺漏的版本標記          |
|      |          `git tag -d v1.0.0`           |       刪除本地標籤        |          移除錯誤的標籤           |
|      |        `git push origin v1.0.0`        |      推送特定標籤到遠端      |           發布新版本            |
|      |           `git push --tags`            |      推送所有標籤到遠端      |          同步所有版本標記          |
|  差異  |               `git diff`               |    查看工作區與暫存區的差異     |        檢視未加入暫存區的修改         |
|      |          `git diff --staged`           |    查看暫存區與最新提交的差異    |         檢視準備提交的修改          |
|      |     `git diff <commit1> <commit2>`     |     比較兩個提交之間的差異     |         比較不同版本的變化          |
|      |      `git diff branch1..branch2`       |     比較兩個分支之間的差異     |       查看功能分支與主分支的差異        |
|      |          `git diff -- <file>`          |      查看特定檔案的修改      |         檢視單一檔案的變更          |
|      |          `git diff ...branch`          |      顯示分支的合併差異      |           預覽合併結果           |
|  遠端  |              `git remote`              |     列出所有遠端倉庫名稱      |        檢視目前有哪些遠端倉庫         |
|      |            `git remote -v`             |     顯示遠端倉庫的 URL     |        查看遠端倉庫的詳細資訊         |
|      |     `git remote add <name> <url>`      |       新增遠端倉庫        |          添加新的協作來源          |
|      |       `git remote remove <name>`       |       移除遠端倉庫        |        移除不再使用的遠端倉庫         |
|      |    `git remote rename <old> <new>`     |       重命名遠端倉庫       |          調整遠端倉庫名稱          |
|      |   `git remote set-url <name> <url>`    |     修改遠端倉庫的 URL     |          更新遠端倉庫位置          |
|      |        `git remote show <name>`        |     顯示遠端倉庫詳細資訊      |        查看遠端分支和追蹤狀態         |
|  挑選  |       `git cherry-pick <commit>`       |    將特定提交套用到目前分支     |      將 bug 修復套用到其他分支       |
|      | `git cherry-pick <commit1> <commit2>`  |    將多個提交套用到目前分支     |      將一系列相關修改合併到發布分支       |
|      | `git cherry-pick <commit1>..<commit2>` |   將一段範圍的提交套用到目前分支   |       將一個完整功能的提交序列合併       |
|      |     `git cherry-pick -e <commit>`      |     在套用時修改提交訊息      |      調整提交說明以符合目前分支情況       |
|      |     `git cherry-pick -n <commit>`      |     只套用修改但不自動提交     |        想要在提交前進行額外修改        |
|      |      `git cherry-pick --continue`      | 解決衝突後繼續 cherry-pick |   處理 cherry-pick 過程中的衝突    |
|      |       `git cherry-pick --abort`        | 取消整個 cherry-pick 過程 |   放棄有問題的 cherry-pick 操作    |
|  推送  |               `git push`               |   推送當前分支到對應的遠端分支    |          日常程式碼提交           |
|      |      `git push <remote> <branch>`      |     推送指定分支到特定遠端     |          推送到特定位置           |
|      |            `git push --all`            |      推送所有本地分支       |          同步所有開發進度          |
|      |           `git push --tags`            |       推送所有標籤        |           發布新版本時           |
|      |             `git push -f`              |      強制覆蓋遠端歷史       |          修改已推送的提交          |
|      |       `git push origin :branch`        |       刪除遠端分支        |          清理不需要的分支          |
|  拉取  |              `git fetch`               |    從遠端獲取所有分支的更新     |          更新本地倉庫資訊          |
|      |          `git fetch <remote>`          |      從特定遠端獲取更新      |          從特定來源更新           |
|      |     `git fetch <remote> <branch>`      |     只獲取特定分支的更新      |          更新特定功能分支          |
|      |           `git fetch --all`            |      從所有遠端獲取更新      |          同步多個遠端源           |
|      |             `git fetch -p`             |    清理已刪除的遠端分支參考     |           維護分支清潔           |
|      |           `git fetch --tags`           |       更新所有標籤        |           同步版本標記           |
| 拉取合併 |               `git pull`               |   拉取並合併當前分支的遠端更新    |           更新本地代碼           |
|      |      `git pull <remote> <branch>`      |    從特定遠端分支拉取並合併     |          合併特定分支更新          |
|      |          `git pull --rebase`           |   使用rebase方式合併更新    |          保持提交歷史整潔          |
|      |            `git pull --all`            |      更新所有追蹤的分支      |           同步所有分支           |
|      |    `git pull --strategy=<strategy>`    |      使用特定合併策略       |          處理特殊合併情況          |
|      |             `git pull -q`              |     安靜模式執行pull      |          自動化腳本中使用          |
|      | `git pull --allow-unrelated-histories` |      合併不相關的歷史       |         合併獨立開發的專案          |
| 重定基底 |         `git rebase <branch>`          |  將當前分支變更重新應用到目標分支   |        更新功能分支到最新主分支        |
|      |        `git rebase -i <commit>`        |      互動式修改提交歷史      |         整理、合併、修改提交         |
|      |        `git rebase --continue`         |   解決衝突後繼續 rebase    |      處理 rebase 過程中的衝突      |
|      |          `git rebase --abort`          |   取消整個 rebase 操作    |       放棄有問題的 rebase        |
|      |     `git rebase --preserve-merges`     |     保留原有的合併提交記錄     |        重整歷史但保留分支結構         |
|      |         `git rebase -i HEAD~3`         |      修改最近的三個提交      |         整理最近的提交歷史          |
|  還原  |         `git revert <commit>`          |   建立一個新提交來還原指定提交    |          撤銷錯誤的提交           |
|      |    `git revert <commit1> <commit2>`    |       還原多個提交        |          批次撤銷多個更改          |
|      |   `git revert <commit1>..<commit2>`    |      還原一段範圍的提交      |          撤銷一系列更改           |
|      |        `git revert -n <commit>`        |     還原但不自動建立提交      |          一次還原多個提交          |
|      |        `git revert --continue`         |      解決衝突後繼續還原      |           處理還原衝突           |
|      |          `git revert --abort`          |      取消整個還原操作       |          放棄有問題的還原          |
|  暫存  |              `git stash`               |      暫存工作目錄的修改      |          需要臨時切換分支          |
|      |       `git stash save "message"`       |      帶描述訊息的暫存       |         記錄暫存的具體內容          |
|      |            `git stash list`            |      顯示所有暫存的列表      |         查看暫存的修改記錄          |
|      |           `git stash apply`            |     套用最近的暫存但不刪除     |        在多個分支使用同樣修改         |
|      |            `git stash pop`             |     套用最近的暫存並刪除      |         恢復之前的工作狀態          |
|      |            `git stash drop`            |       刪除最近的暫存       |          清理不需要的暫存          |
|      |           `git stash clear`            |       刪除所有暫存        |          清理所有暫存記錄          |
|      |          `git mv <old> <new>`          |      重命名檔案或目錄       |           修改檔案名稱           |
|      |         `git mv <file> <dir>`          |      移動檔案到其他目錄      |           重組專案結構           |
|      |          `git mv -k * <dir>`           |      批次移動多個檔案       |          大規模重構專案           |
|      |                                        |                     |                            |

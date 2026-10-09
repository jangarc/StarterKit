# 建立方案流程

## 預計資料夾結構

```bash
StarterKit方案
  src
    Application專案
	Domain專案
	Infrastructure專案
	WebApi專案
  Project.slnx
```

## 建立方案

在建立Visual Studio建立新方案，初始化版本庫

```bash
# 初始化專案
git init
git submodule init
# 建立.NET方案專用 .gitignore
dotnet new gitignore
# 提交所有內容
git add .
git commit -m "初始化專案"
# 建立分支
git branch -M main
# 建立遠端
git remote add origin git@github.com:jangarc/StarterKit.git
# 推送到分支
git push -u origin main
```

## 綁定子方案

先至github開立新儲存庫StarterKit-Domain.git

```bash
cd src
# 綁定子儲存庫預設會有main分支)
git submodule add git@github.com:jangarc/StarterKit-Domain.git Domain
# 將檔案Copy回Domain資料夾
cd Domain
dotnet new gitignore
git add .
git commit -m "初始化Domain專案"
git push -u origin main
```

先至github開立新儲存庫StarterKit-Application.git

```bash
cd ../Application
# 綁定子儲存庫(預設會有main分支)
git submodule add git@github.com:jangarc/StarterKit-Application.git Application
# 將檔案Copy回 Application 資料夾
cd Application
dotnet new gitignore
git add .
git commit -m "初始化Application專案"
git push -u origin main
```

先至github開立新儲存庫StarterKit-Infrastructure.git

```bash
cd ../Infrastructure
# 綁定子儲存庫(預設會有main分支)
git submodule add git@github.com:jangarc/StarterKit-Infrastructure.git Infrastructure
# 將檔案Copy回 Infrastructure 資料夾
cd Infrastructure
dotnet new gitignore
git add .
git commit -m "初始化Infrastructure專案"
git push -u origin main
```

先至github開立新儲存庫StarterKit-WebApi.git

```bash
cd ../WebApi
# 綁定子儲存庫(預設會有main分支)
git submodule add git@github.com:jangarc/StarterKit-WebApi.git WebApi
# 將檔案Copy回 WebApi 資料夾
cd WebApi
dotnet new gitignore
git add .
git commit -m "初始化WebApi專案"
git push -u origin main
```

[注意] 增加任一子專案後，會產生根專案會產生.gitmodules檔，所以最終應該要回到根專案進行add & commit

```
# 回到 /StarterKit(執行前確認所有子專案都己)
git add .
git commit -m "增加子模組..."
git push origin main
```

## git submodule 使用

拉取最新代碼

```bash
# 使用
git submodule update --remote --merge

# 或進入子專案版本庫資料夾
cd src/Domain
git pull origin main
```

推送代碼

```bash
# 進入子模組目錄
cd src/Domain

# 提交並推送 Domain 的修改
git add .
git commit -m "提交說明"
git push origin main

# 回到主方案根目錄
cd ../..

# 檢查狀態，你會看到 src/Domain 顯示為新修改
git status

# 提交主方案的改動（包含 slnx 的調整與子模組的新指針）
git add .
git commit -m "chore: 更新主方案與 Domain 子模組版本"
git push origin main
```

XXX

## git submodule 常見問題處理

### git submodule update --init --recursive 時顯示授權不足
```bash
# 使用以下指令檢查使用SSH, 如果都沒顯示時，代表Git使用內建OpenSSH
git config --global core.sshCommand
# 指定Windows內建SSH
git config --global core.sshCommand "C:/Windows/System32/OpenSSH/ssh.exe"
```

### 在 clone submodule 專案時同時初始化所有子專案

```bash
git clone --recursive git@github.com:jangarc/StarterKit.git
```

### 備份至本地儲存庫

```bash
# 假設儲存庫資料夾在D:\store 在該資料夾裡建立可供備份的版本庫 
git init --bare project1.git # => 會產生 D:\store\project1.git 資料夾

# 使用本地儲存庫 => 在專案中增加遠端
git remote localRepo D:\store\project1.git
# 將專案備份至本地儲存庫
git push localRepo main
```

### 拉取主專案時同時拉取子專案更新

```bash
git pull origin --recurse-submodules
git pull origin main --recurse-submodules
```

### 在推送主專案時怎麼避免《忘記推送到子模組遠端，就直接提交主專案》導致其他人壞掉的致命陷阱

```bash
# 使用以下指令: 有子分支未推送時，就推送主分支時會卡下來
git push --recurse-submodules=check 
# 或使用以下指令: 有子分支未推送時，先幫你把所有子專案推送完，再將主專案推送出去
git push --recurse-submodules=on-demand
# 或使用設定方式解決
git config --global push.recurseSubmodules on-demand
```

---

## 常用git指令

```bash
# 刪除分支
git branch -d [分支名稱]
```

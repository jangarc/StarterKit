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
cd src
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
cd src
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
cd src
# 綁定子儲存庫(預設會有main分支)
git submodule add git@github.com:jangarc/StarterKit-WebApi.git WebApi
# 將檔案Copy回 WebApi 資料夾
cd WebApi
dotnet new gitignore
git add .
git commit -m "初始化WebApi專案"
git push -u origin main
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
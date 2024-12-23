# VS Code 和 Anaconda 設定檔

這個倉庫包含我的 VS Code 和 Anaconda 環境設定，用於在不同電腦間同步設定。

## 檔案結構
- `.vscode/`: VS Code 設定檔
  - `settings.json`: VS Code 基本設定
  - `keybindings.json`: 快捷鍵設定
- `conda_env/`: Anaconda 環境設定
  - `aia_env.yml`: AIA_ENV 環境配置文件

## 初始設定流程

### 主要電腦（首次設定）
1. 創建並設定 VS Code 環境：
   - 安裝 VS Code
   - 安裝所需擴展（如：Python, Vim 等）
   - 配置 settings.json 和 keybindings.json

2. 設定 Anaconda 環境：
   - 安裝 Anaconda
   - 創建新環境：`conda create -n AIA_ENV python=3.10`
   - 安裝所需套件：`conda install pytorch torchvision torchaudio -c pytorch`

3. 導出環境設定：
   ```bash
   # 導出 Anaconda 環境
   conda activate AIA_ENV
   conda env export --no-builds > conda_env/aia_env.yml
   ```

4. 上傳到 Git：
   ```bash
   git init
   git add .
   git commit -m "Initial commit: VS Code and Anaconda settings"
   git remote add origin <您的GitHub倉庫URL>
   git push -u origin main
   ```

### 其他電腦（同步設定）
1. 克隆設定倉庫：
   ```bash
   git clone <您的GitHub倉庫URL>
   ```

2. 設定 VS Code：
   - 安裝 VS Code 和必要擴展
   - 將 `.vscode` 資料夾複製到您的專案目錄中
   - 修改 `settings.json` 中的路徑（如果 Anaconda 安裝路徑不同）

3. 設定 Anaconda 環境：
   ```bash
   # 創建環境
   conda env create -f conda_env/aia_env.yml
   ```

## 更新設定流程

### 當您更改了設定
1. 更新 VS Code 設定：
   - 如果修改了 VS Code 設定，更新 `.vscode` 資料夾中的文件

2. 更新 Anaconda 環境：
   ```bash
   # 如果安裝了新的套件，更新環境文件
   conda activate AIA_ENV
   conda env export --no-builds > conda_env/aia_env.yml
   ```

3. 提交更改：
   ```bash
   git add .
   git commit -m "更新設定: <描述更改內容>"
   git push
   ```

### 在其他電腦上同步更改
1. 拉取最新更改：
   ```bash
   git pull
   ```

2. 更新 VS Code 設定：
   - 複製更新後的 `.vscode` 資料夾到專案目錄

3. 更新 Anaconda 環境：
   ```bash
   # 更新環境
   conda activate AIA_ENV
   conda env update -f conda_env/aia_env.yml
   ```

## 常見問題處理
1. VS Code 設定不生效：
   - 確認 `.vscode` 資料夾在正確的專案目錄中
   - 重新啟動 VS Code

2. Anaconda 環境問題：
   - 如果環境損壞，可以重新創建：
     ```bash
     conda deactivate
     conda env remove -n AIA_ENV
     conda env create -f conda_env/aia_env.yml
     ```

3. 路徑問題：
   - 確認 `settings.json` 中的 Anaconda 路徑符合當前電腦的安裝路徑
   - 根據需要調整路徑設定

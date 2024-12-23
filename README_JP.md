# VS Code と Anaconda 設定 | VS Code and Anaconda Settings | VS Code 和 Anaconda 設定檔

<div align="center">

[中文](README.md) | [English](README_EN.md) | [日本語](README_JP.md)

</div>

このリポジトリには、異なるコンピュータ間で同期するための VS Code と Anaconda 環境設定が含まれています。

<!-- CASCADE-SETTINGS-SYNC-MARKER -->
<!-- バージョン: 1.0 -->
<!-- 最終更新: 2024-12-23 -->
<!-- 設定タイプ: VS Code, Anaconda, GPU -->

## クイックプレビュー
![VS Code 設定プレビュー](images/vscode-preview.png)
![Anaconda 環境プレビュー](images/anaconda-preview.png)

## 自動同期手順
VS Code と Codeium 拡張機能を使用している場合：
1. この README.md ファイルを開く
2. Codeium に「このプロジェクトの設定を同期してください」と伝える
3. Codeium が自動的に設定マーカーを検出し、すべての設定を完了します

手動設定を希望する場合は、以下の手順に従ってください。

## ディレクトリ構造
```
vscode-settings-sync/
├── .vscode/                 # VS Code 設定
│   ├── settings.json       # 基本設定
│   └── keybindings.json    # キーボードショートカット
├── conda_env/              # Anaconda 環境設定
│   └── aia_env.yml        # AIA_ENV 環境構成
└── images/                 # ドキュメント画像
    ├── vscode-preview.png
    └── anaconda-preview.png
```

## 初期設定プロセス

### メインコンピュータ（初回設定）
1. VS Code 環境の作成と設定：
   - VS Code をインストール
   - 必要な拡張機能をインストール（Python, Vim など）
   - settings.json と keybindings.json を設定

2. Anaconda 環境の設定：
   - Anaconda をインストール
   - 新しい環境を作成：`conda create -n AIA_ENV python=3.10`
   - 必要なパッケージをインストール：`conda install pytorch torchvision torchaudio -c pytorch`

3. 環境設定のエクスポート：
   ```bash
   # Anaconda 環境をエクスポート
   conda activate AIA_ENV
   conda env export --no-builds > conda_env/aia_env.yml
   ```

4. Git にアップロード：
   ```bash
   git init
   git add .
   git commit -m "Initial commit: VS Code and Anaconda settings"
   git remote add origin <GitHub リポジトリ URL>
   git push -u origin main
   ```

### 他のコンピュータ（同期設定）
1. 設定リポジトリのクローン：
   ```bash
   git clone <GitHub リポジトリ URL>
   ```

2. VS Code の設定：
   - VS Code と必要な拡張機能をインストール
   - `.vscode` フォルダをプロジェクトディレクトリにコピー
   - `settings.json` のパスを修正（Anaconda のインストールパスが異なる場合）

3. Anaconda 環境の設定：
   ```bash
   # 環境を作成
   conda env create -f conda_env/aia_env.yml
   ```

## 更新プロセス

### 設定を変更した場合
1. VS Code 設定の更新：
   - VS Code 設定を変更した場合、`.vscode` フォルダ内のファイルを更新

2. Anaconda 環境の更新：
   ```bash
   # 新しいパッケージをインストールした場合、環境ファイルを更新
   conda activate AIA_ENV
   conda env export --no-builds > conda_env/aia_env.yml
   ```

3. 変更をコミット：
   ```bash
   git add .
   git commit -m "設定を更新：<変更内容の説明>"
   git push
   ```

### 他のコンピュータでの同期
1. 最新の変更を取得：
   ```bash
   git pull
   ```

2. VS Code 設定の更新：
   - 更新された `.vscode` フォルダをプロジェクトディレクトリにコピー

3. Anaconda 環境の更新：
   ```bash
   # 環境を更新
   conda activate AIA_ENV
   conda env update -f conda_env/aia_env.yml
   ```

## トラブルシューティング
1. VS Code 設定が反映されない：
   - `.vscode` フォルダが正しいプロジェクトディレクトリにあることを確認
   - VS Code を再起動

2. Anaconda 環境の問題：
   - 環境が破損した場合、再作成：
     ```bash
     conda deactivate
     conda env remove -n AIA_ENV
     conda env create -f conda_env/aia_env.yml
     ```

3. パスの問題：
   - `settings.json` の Anaconda パスがコンピュータのインストールパスと一致することを確認
   - 必要に応じてパスを調整

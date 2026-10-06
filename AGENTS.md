# AGENTS.md

- 所有回應一律使用繁體中文。

## 範圍
- `C:\Users\user\Desktop\呱呱` 本身不是 git repo。真正的 repo 是底下兩個同 remote（`https://github.com/c115143135-max/-prgraming-.git`）的重複 clone：`-prgraming-\`、`-prgraming--1\`
- 根目錄的 `11.ipynb` 是未追蹤的散落複本，不要改；只改其中一個 clone 內。
- 每次任務只選一個 clone，勿兩邊套用同一編輯，否則會無聲分歧。
- 有意義的檔案只有 `11.ipynb`、`README.md`（僅一行標題）、`.gitignore`（標準 Python 範本）。無相依清單、測試、lint、CI、`opencode.json`。

## 指令（Python + conda，勿猜）
- 本專案語言為 Python，唯一套件管理方式是 conda，環境名稱 `iem_python`（已驗證：Python 3.12.13，與 `11.ipynb` 的 kernelspec `display_name: iem_python` 一致）。
- 一律用 `conda run -n iem_python ...` 執行，例如 `conda run -n iem_python python -m jupyter nbconvert --to notebook --execute 11.ipynb`。禁止 `pip`、`venv`、`py`、系統 `python`（此機器的 `python` 是壞掉的 Store 捷徑，`py` 是 3.13.6，與 notebook 無關）。
- `conda` 不在 PATH，需用完整路徑 `C:\Users\user\anaconda3\Scripts\conda.exe`（`env list` 已確認 `iem_python` 位於 `C:\Users\user\anaconda3\envs\iem_python`）。
- `iem_python` 內已有 `jupyter_client` / `jupyter_server` / `ipykernel`，可用 nbconvert 執行 notebook 驗證；不要另裝 Jupyter。
- 原本指定的 `C:\Users\user\Desktop\556` 不存在，指令一律帶明確路徑（如 `git -C "<clone>" status`），或把 workdir 設為該 clone。

## 地雷
- `git status` 可能顯示 `M 11.ipynb` 但 diff 是空的（僅 LF vs CRLF 警告），不要提交這種噪音。
- `.ipynb` 內嵌執行 `outputs`，提交前保持精簡，避免大型輸出。
- 預設分支 `main` 對應 `origin/main`，只從一個 clone 提交，避免兩個重複 clone 互搶 push。

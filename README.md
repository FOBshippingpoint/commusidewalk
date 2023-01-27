# commu-sidewalk

以R做平安走路許願帳戶的資料處理

[補充文件](https://docs.google.com/document/d/1bOuwkF_0abTdAyhnxUxhxrwExjNR9BnhfFtT7l5Vzc4/edit?usp=sharing)
[Google試算表  v20230127](https://docs.google.com/spreadsheets/d/17eUoIsEBugXniR0klzlvmXeewM029A7fDpOw2HI6MSY/edit#gid=558584087)

## Develop

檔案架構：
```text
│  .gitignore
│  commu-sidewalk.Rproj # RStudio project file
├─data                  # 儲存資料
├─output                # 輸出資料
└─src                   # R scripts
        1_download.R
        2_cleaning.R
        3_output.R
```

### 自動化

`main.R`會自動執行所有步驟，最終你會在`/data`裡面看到`今日日期.csv`，就是資料處理後的結果。

Linux
```sh
# cd to project directory (same floor with .gitignore)
> Rscript main.R
```

Windows
```powershell
> Rscript.exe main.R
```

### Library Used

- jsonlite
- tidyverse (沒用多少)
- ggplot2

### 1\_download.R

從commutag下載標註圖片`df_img`及資料集資訊`lst_info`（in `/data/raw.RData`）。

改變`is_limit`可改為下載有限的(8筆)或整組圖片資料。

### 2\_cleaning.R

1. rename formReply id (ugly) to chinese question name
2. use `|` as deliminator for list (we cannot save list in csv)
3. formReply$value -> formReply
4. 加入哈爸資料有的我這邊沒有的欄位，設成NA
5. 重新命名欄位
6. 重新排序成可以餵給App script的順序
7. 儲存成csv（Excel會亂碼，但LibreOffice可以正常開）

### 3\_output.R

試玩ggplot2，產生照片數量的時間序列圖。
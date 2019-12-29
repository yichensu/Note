# SQL syntax

## 如何匯入csv檔

採用路徑：
1. 在Schema區域中（MySQL左邊區域）按右鍵
2. 選擇 `create schema`
3. 建立schema之後，先create table，可以認真設primary key，但也可以先不設定
4. 建立table後，可以選擇用`Table Data Import Wizard`輸入csv檔或json，若存入現存的失敗，可採用「建立新的table」
5. 若前面沒有認真社primary key，會是唯獨檔，要`alter table`，新增primary key才能繼續寫入
6. 要測試資料數量的話，可以給予下列指令
```
select count(*) from dcard.`2019`; --記得要用``去包住數字
```

## 如何進行MySQL中，兩個table的整合

### 常見問題：
1. 原本資料量太大，被分為多個CSV黨儲存，但需要匯入MySQL來分析
2. 可能有重複的id，而一直出現 `Duplicate entry`
```
INSERT IGNORE INTO dcard.myTable (   -- ignore:MySQL即使有重複，也不會出現error
    id, 
    title, 
    school,
    created_at,
    content
)
SELECT 
    id, 
    title, 
    school,
    created_at,
    content
FROM 
    dcard.newTable

```
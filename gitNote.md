# 我的筆記

## 如何使用github?

> 一開始出建立的時候會使用
- git init: 在目標資料夾下面初始化git
> 以下步驟每次都會進行
- git add . : 把所有檔案都加入版本管理的狀態中
- git add file: 把叫做file的檔案名加入版本管理中
- git commit -m "message":儲存一個版本 -m 後面的東西是對於這個版本的描述
- git push:把儲存好的版本推上github
> 非必要使用
- git status: 可以看到被版本管理的檔案(非必要)

> 嘗試如何將檔案連結加到目錄頁
- 形式：[檔案名稱](路徑)
- 取得路徑方式：按md檔案的右鍵 >> `copy relative path` >> 貼到()內

[c++ note](c++Note/c++.md)
[SQL note](SQL/syntax.md)

## 如何使用command line 

- `cd ..`: 退到上一層目錄
- `mkdir file`:新增一個資料夾（叫file)
- `touch file`:創造一個檔案（file)
- `open .`:打開當前麽目錄
- `cd  file` ：進入某個資料夾（叫file)
- `ls`:看目錄下面的所有檔案

## 如何使用branch

- `git branch newBranch`： 新增一個branch，叫做newBranch
- `git checkout newBranch`：跳到另一個叫做newBranch的branch
- 就可以繼續git add推上去
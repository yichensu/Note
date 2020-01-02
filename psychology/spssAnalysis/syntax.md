# SPSS syntax

## HLM

### 為何使用HLM
當資料有分層關係的時候，例如：
1. 國家裡面有城市，城市裡面又有學校，學校裡面有班級，班級裡面有學生，都是層層關係。
2. 一個人被測量多個時點的正負向情緒，而我們想知道受試者本身因素
3. 假設問：動物體重愈重，壽命愈長或愈短。是在問物種內還是物種間？
![MLM1](⁩)


一般回歸式 vs. 多層次分析：
1. 一般回歸式： 
2. 多層次分析：


若想了解不同群體間效果，多層次分析的模型較為合理


### 如何進行資料轉換

- `/MAKE newName FROM otherData`: 將原本橫向的資料都轉換成一欄
```
/MAKE new variable ["label"] [FROM] varlist [/MAKE ...] --可以給標籤
```
- `/INDEX`: 以哪些欄位當作標籤，會有幾個標籤，放()內
```
{new variable ["label"]                                  }]
          {new variable ["label"] (make variable name)             }
          {new variable ["label"] (n) new variable ["label"](n) ...}
```

```
[/ID = new variable ["label"]] --是否有新的ID

[/NULL = {DROP**}] --這個還不懂，待研究
         {KEEP  }

[/COUNT=new variable ["label"]]

[/KEEP={ALL**  }] [/DROP=varlist] 
       {varlist}
```
碩論的程式碼
```
VARSTOCASES
  /MAKE PA FROM meanpa1 meanpa2 meanpa3 meanpa4
  /MAKE NA FROM meanna1 meanna2 meanna3 meanna4
  /MAKE PA_ed FROM EMODIVERSITY_Positive1 EMODIVERSITY_Positive2 EMODIVERSITY_Positive3 EMODIVERSITY_Positive4
  /MAKE NA_ed FROM EMODIVERSITY_Negative1 EMODIVERSITY_Negative2 EMODIVERSITY_Negative3 EMODIVERSITY_Negative4
  /MAKE global_ed FROM EMODIVERSITY_Global1 EMODIVERSITY_Global2 EMODIVERSITY_Global3 EMODIVERSITY_Global4
  /INDEX=time(4) 
  /KEEP=subjectID gender age maas
  /NULL=KEEP.
--下列是MLM分析
mixed PA with gender age maas
/fixed = gender age maas
/random = intercept maas | subject(subjectID) cov(un)
/print=solution testcov.

mixed NA with gender age maas
/fixed = gender age maas
/random = intercept maas | subject(subjectID) cov(un)
/print=solution testcov.

```
### 結果判讀
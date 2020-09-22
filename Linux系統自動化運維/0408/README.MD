# Linux Shell Script

使用 .sh 副檔名來命名 Shell Script 檔案。然後將該檔案設定為可執行
```
chmod +x demo.sh
```
- 變數宣告 \
variable1=value
若是值內有空白則需要使用 '' 或 "" 包裹起來
 
使用變數方式為 ${變數名稱} ex:echo ${value} \
刪除變數使用unset

- 運算式 \
expr命令可以用來做數值運算、數值或字串比較、字串匹配、字串提取、字串長度計算等功能。 它還具有幾個特殊功能,判斷變數或參數是否為整數、是否為空、是否為0等。
```
$expr 10 + 10
20
$expr 1500 + 900
2500
$expr 30 / 3
10
$expr 30 / 3 / 2
5
```
- if .. else \
    在shell script中使用fi做結尾 \
    使用 -gt （greater than 縮寫）和 -lt （less than 縮寫）代表大於和小於，而 -ge （greater equal 縮寫）和 -le（less equal 縮寫）則是大於等於和小於等於的運算子符號。
```
if [ $x -gt $y ]; then
   echo "value x is greater than value y"
else
   echo "value x is not greater than value y"
fi
```
- case \
    用以處理多種條件判斷 結尾為esac
```
language='Java'

case $language in
    Java*) echo "是 Java！"
            ;;
    Python*) echo "是 Python！"
            ;;
    C*)     echo "是 C！"
            ;;
    *)      echo "沒 match 到！"
esac
```
- while, break
```
while [ 1 ]; do
  HOUR=`date +'%H'`
  if [ $HOUR -eq 10 ]; then
     echo "OH OH, it's already 10:00, i got to go"
     break
  fi
  sleep 5
done
```
上面的範例說明, 持續每五秒檢查一次, 是否已經是 10 點鐘了, 若已經 10 點, 則 break 跳出 while 迴圈.

- Function \
函式名稱（function 關鍵字為選擇性）
是否有傳入參數
函式內操作
是否有回傳值
```
function function_name () {
     做一些事情
    [ 回傳值 ]
}
```

###  參考資料
[簡明 Linux Shell Script 入門教學](https://blog.techbridge.cc/2019/11/15/linux-shell-script-tutorial/) \
[鳥哥的 Linux 私房菜](http://linux.vbird.org/linux_basic/0340bashshell-scripts.php#function)

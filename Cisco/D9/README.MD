## 11/18上課

![0](eigrp.png)
- Successor可理解為best path，圖中C節點為successor
- Feasible successor AD必須小於FD
- 不等價負載均衡:可讓大部分走最好路徑，小部分走其他路徑 **variance*FD要大於其他路徑的FD** 

|Network|Neighbor|FD|AD
|-----|:--------:|-----|-----|
|172.16.0.0 |B | 30 | 10 |
|   |C | 20 | 10 |
|   |D | 45 | 25 |


- ACL(Access Control List)
    - 簡易防火牆
    - 資料分類  

**所有規則都無符合，封包會drop，黑名單模式下，最後一筆要加上permit any**

設定規則
規則要在何接口，指定方向

**ACL實驗**
![1](1.PNG)

- R2設定
```
access-list 1 deny host 1.1.1.1
access-list 1 permit any
int e0/0
ip access-group 1 in
```
設定完成後能夠阻擋來自1.1.1.1封包
![2](2.PNG)

[ACL介紹]("http://www.tsnien.idv.tw/Manager_WebBook/chap9/9-5%20%E5%B0%81%E5%8C%85%E9%81%8E%E6%BF%BE%E8%A1%A8%20%E2%80%93%20ACL.html")
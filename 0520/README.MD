# 0520上課

## ZABBIX監控
Configutation > Hosts > item > create
建立新item
![za2](za2.PNG)
New Application > http stats

httpd port號要記得改
![httpd](httpd.PNG)
到Monitoring
![moni](data.PNG)

建立新的trigger
![tri](trigger.PNG)

接著到VM2關閉httpd
![problem](problem.PNG)
就會看到最上方有紅色警示。
- Line Notify
![line](line.PNG)
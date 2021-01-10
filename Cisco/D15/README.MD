## 第十五周上課

**spanning tree**

loop will cause broadcast storm  
loop roburstness

- Find the loop bridge
    - priority + MAC address(與其他節點通訊，最小值成為根橋)
        - priority = 32768 + VLAN ID(default = 1)
- Find the root port
- Find the designated port (D port)
    - 對每個區域網路到根橋的最少成本，若相同則比較ID

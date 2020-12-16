## 第十二週上課

**scale**
彈性伸縮
`kubectl scale deployment myweb --replicas 3`

`kubectl set image deployment myweb2 httpd=httpd:2.4.46`更新
`kubectl rollout undo deployment myweb2` 取消更新


進去pod裡的容器
`kubetl exec myweb-4655fdf -it -- bash`
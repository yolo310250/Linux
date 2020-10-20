## 第五周上課

**容器互連**

`docker run -it --name c1 busybox sh`  
`docker run -it --name c2 --link c1:c1 busybox sh`  
- 後面所建立之容器可連接前面的，前面則無法
![1](1.PNG)

`docker network create --driver bridge mynet`  
`docker run -it --name c3 --network mynet busybox sh`  
`docker run -it --name c3 --network mynet busybox sh`  
![2](2.PNG)
## 第三周上課
容器只要沒有持續執行的程式，容器便會結束

`docker info`:docker相關資訊
`docker attach`:重新連回容器

- `docker pull gcc`

```
mkdir -p /data
cd /data
vim hello.c
    檔案寫入:
    #include <stdlib.h>
    #include <stdio.h>

    int main(){
        printf("hello world\n");
        return 0;
    }
```
`docker run -it -v /data:/data gcc:latesst bash`:(本地資料夾映射到docker內)  
`-v` 資料持久化  
`gcc -o /data/hello /data/hello.c`  
`./hello`
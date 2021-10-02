1、构建docker-compose 方法如下：

```
1、新建一个文件夹

2、文件夹下touch一个文件 docker-compose.yml

3、输入内容

4、docker-compose up -d
```

2、docker-compose常见命令

```
1. docker-compose up -d 启动；
2. docker-compose logs 打印日志；
3. docker-compose pull 更新镜像；
4. docker-compose stop 停止容器；
5. docker-compose restart 重启容器；
6. docker-compose down 停止并删除容器；
```

安装 centos

```
yum install docker
yum install docker-compose
```



routeros docker ，构建如下：

```
version: "3.3"

services:

  mkt01:
    image: cnsoluciones/mikrotik:latest
    container_name: mkt01
    restart: always
    ports:
      - "121:21"
      - "122:22"
      - "123:23"
      - "150:50"
      - "151:51"
      - "180:80"
      - "1443:443"
      - "1500:500"
      - "11194:1194"
      - "11701:1701"
      - "11723:1723"
      - "14500:4500"
      - "15900:5900"
      - "18080:8080"
      - "18291:8291"
      - "18728:8728"
      - "18729:8729"
    environment:
      - "VNCPASSWORD=false"
    network_mode: bridge
    privileged: true


  winbox:
    image: cnsoluciones/novnc-winbox:latest
    container_name: winbox
    hostname: winbox
    restart: always
    #volumes:
    #  - ./user-data/.wine:/home/alpine/.wine
    links:
      - "mkt01"
    ports:
      - "5901:5900"
      - "18081:8080"
    network_mode: bridge
```


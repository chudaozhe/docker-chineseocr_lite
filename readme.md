# 目录结构
```
│  .gitignore
│  docker-compose.yml
│  readme.md
├─.docker
│      docker-compose.yaml
├─chineseorc
│      init.sh
```
其中`.docker`目录不是必须的，是配合docker-desktop一起用的，一个python的开发环境

其中`docker-compose.yml`文件中`networks`的定义，为了与其他`docker-compose.yml`网络互通，使用了外部网络。如果不需要多个docker-compose互通，可以修改一下
```
version: '3'
networks:
  web-network:

services:
  docker-chineseorc:
    ...
    networks:
      - web-network
```
# 获取项目代码
```
cd chineseorc
#默认分支，即 onnx
git clone git@github.com:DayBreak-u/chineseocr_lite.git
```
# 一些修改
```
cd chineseocr_lite
mv 仿宋_GB2312.ttf fangsong_GB2312.ttf

vi backend/webInterface/tr_run.py
   myfont = ImageFont.truetype("fangsong_GB2312.ttf", size=size)
   
# 关于Dockerfile
官方提供的`Dockerfile`没有问题，编译`docker build -t my/chineseocr .`一下就能用
但是，后来我发现用python的官方镜像+init.sh也是可以运行这个项目的，详见docker-compose.yml
```

# 使用
```
# 启动
docker-compose up -d
# 浏览器访问
http://127.0.0.1:8089/
```

# 文章
http://www.cuiwei.net/p/1052444754
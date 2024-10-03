


## 🤔 这是什么？
它是一个工作流。可快速构建指定架构/平台的docker镜像

## 使用说明
https://wkdaily.cpolar.cn/archives/gc

下载好的.tar文件上传到docker目录下（示例将文件上传至mnt/nvme0n1-4/xxx.tar）xxx表示为文件名

打开ssh：
```
cd /mnt/nvme0n1-4/
```
```  
ls
```
```
docker load -i xxx.tar
```

此时镜像文就导入到docker中了

## 在哪里可以搜索或查询docker镜像的详细信息
### [查询镜像的详细信息 点击这里直达](https://docker.fxxk.dedyn.io/)

## 解压工具
> Windows 上推荐使用7zip<br>
> macOS 推荐使用MacZip<br>
> Linux上推荐直接用tar 命令

## 相关项目
https://github.com/wukongdaily/OrangePiShell


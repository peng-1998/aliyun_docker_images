# Pytorch Docker 容器
用于构建pytorch机器学习环境的docker项目，使用阿里云的自动构建服务
镜像仓库的地址为registry.cn-hangzhou.aliyuncs.com/pengdeeplearning/pytorch_cuda:[镜像版本号]
使用以下命令拉取镜像:
```
docker pull registry.cn-hangzhou.aliyuncs.com/pengdeeplearning/pytorch_cuda:[镜像版本号]
```
可以使用的镜像版本有：
|tag|python|pytorch|torchvision|编译cuda|环境cuda|大小(GB)|
|---|---|---|---|---|---|---|
|torch111_vision012_cu113_cuda117_devel_manjaro|3.10.5|1.11|0.12|11.3|11.7|7.072|
|torch111_vision012_cu113_cuda113_devel_ubuntu2004|3.8.10|1.11|0.12|11.3|11.3|6.056|
|torch111_vision012_cu113_cuda113_runtime_ubuntu2004|3.8.10|1.11|0.12|11.3|11.3|5.037|
|torch112_vision013_cu116_cuda117_devel_manjaro|3.10.5|1.12|0.13|11.6|11.7|7.198|
|torch112_vision013_cu116_cuda116_devel_ubuntu2004|3.8.10|1.12|0.13|11.6|11.6|6.543|
|torch112_vision013_cu116_cuda116_runtime_ubuntu2004|3.8.10|1.12|0.13|11.6|11.6|5.298|

## StaMutAble
### About

StaMutAble is a computational framework for predicting mutation-induced protein stability changes, with a focus on improving the identification of stabilizing mutations. It integrates predictions from ten existing tools—PremPS, ThermoMPNN, MultiMutate, RaSP, FoldX, ACDC-NN, MAESTRO, ThermoNet, SimBa-SYM, and DDGun3D—as input features and trains ensemble random forest models on datasets balanced between destabilizing and stabilizing mutations. The framework provides two models: RF-Ensemble-BalAvg for regression and RF-Ensemble-BalVote for classification, enabling more accurate, robust, and balanced predictions, particularly for stabilizing mutations.


### StaMutAble Installation and Usage Instructions


#### 1.Pull Docker Image

For the easiest setup, pull the public Docker image. Make sure Docker is installed: https://docs.docker.com/get-started/get-docker/

```
docker pull minghuilab/StaMutAble:v1
```


•  Image size: 57.3 GB  
•  Estimated download time (approximate):

> 100 Mbps: ~76 min    
> 1 Gbps: ~8 min  
> (actual time depends on your network speed)


#### 2.Run the Docker Container and Activate Environment

```
docker run -it minghuilab/StaMutAble:v1 /bin/bash
conda activate py38
cd stamutable
```


##### 3.Preparing Input and Output Dictionaries

程序默认的输入文件路径是/stamutable/stamutable_input，默认的输出路径是/stamutable/stamutable_output

可以根据具体的情况来设定和创建输入输出路径
































## StaMutAble
### About

StaMutAble is a computational framework for predicting mutation-induced protein stability changes, with a focus on improving the identification of stabilizing mutations. It integrates predictions from ten existing tools—PremPS, ThermoMPNN, MultiMutate, RaSP, FoldX, ACDC-NN, MAESTRO, ThermoNet, SimBa-SYM, and DDGun3D—as input features and trains ensemble random forest models on datasets balanced between destabilizing and stabilizing mutations. The framework provides two models: RF-Ensemble-BalAvg for regression and RF-Ensemble-BalVote for classification, enabling more accurate, robust, and balanced predictions, particularly for stabilizing mutations.

### StaMutAble Installation and Usage Instructions

#### 1.Pull Docker Image

For the easiest setup, pull the public Docker image. Make sure Docker is installed: https://docs.docker.com/get-started/get-docker/(https://docs.docker.com/get-started/get-docker/)

```
docker pull minghuilab/StaMutAble:v1
```







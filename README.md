# StaMutAble
## About

StaMutAble is a computational framework for predicting mutation-induced protein stability changes, with a focus on improving the identification of stabilizing mutations. It integrates predictions from ten existing tools—PremPS, ThermoMPNN, MultiMutate, RaSP, FoldX, ACDC-NN, MAESTRO, ThermoNet, SimBa-SYM, and DDGun3D—as input features and trains ensemble random forest models on datasets balanced between destabilizing and stabilizing mutations. The framework provides two models: RF-Ensemble-BalAvg for regression and RF-Ensemble-BalVote for classification, enabling more accurate, robust, and balanced predictions, particularly for stabilizing mutations.


## StaMutAble Installation and Usage Instructions


### 1. Pull Docker Image

For the easiest setup, pull the public Docker image. Make sure Docker is installed: https://docs.docker.com/get-started/get-docker/

```
docker pull minghuilab/stamutable:v1
```


•  Image size: 99.7 GB  
•  Estimated download time (approximate):

> 100 Mbps: ~132 min    
> 1 Gbps: ~14 min  
> (actual time depends on your network speed)


### 2. Run the Docker Container and Activate Environment

```
docker run -it minghuilab/stamutable:v1 /bin/bash
conda activate pyG
cd stamutable
```


### 3. Preparing Input and Output Dictionaries

The program's default input file path is **/stamutable/example_pdb3**, and the default output path is **/stamutable/example_pdb3_output**. 

The input and output paths can be customized and created according to specific needs.

The reference format for the input file is shown below: [example_100muts.txt](stamutable_input/example_100muts.txt):

```
pdb_chain       mutation
5B83_A  M229W,F232W
```

**Note：**

(1) The **pdb_mut** column represents the mutation along with the PDB ID and chain where the mutation occurs. The **mutation** column indicates all single-point mutations occurring on this protein.

(2) Different columns in the table are separated by tabs.


### 4. Running StaMutAble

For regression model RF-Ensemble-BalAvg:

```
python StaMutAble_regression.py --workdir /stamutable/ --input /stamutable/example_100muts.txt --output /stamutable/stamutable_output/
```

For classification model RF-Ensemble-BalVote:

```
python StaMutAble_classification.py --workdir /stamutable/ --input /stamutable/example_100muts.txt --output /stamutable/stamutable_output/
```


### 5. Recommended System Requirements

•	**RAM:** ≥120 GB recommended (≥110 GB minimal requirement)

•	**Disk Space:** ≥340 GB (Docker image: ~340 GB + additional space for data and output)















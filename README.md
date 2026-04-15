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
docker run -it minghuilab/StaMutAble:v1 /bin/bash
conda activate pyG
cd stamutable
```


### 3. Preparing Input and Output Dictionaries

The program's default input file path is **/stamutable/stamutable_input**, and the default output path is **/stamutable/stamutable_output**. 

The input and output paths can be customized and created according to specific needs.

The reference format for the input file is shown below: [example_100muts.txt](stamutable_input/example_100muts.txt):

```
pdb_mut	PremPS	ThermoMPNN	ThermoNet	ACDC-NN	DDGun3D	MAESTRO	MultiMutate	SimBa-SYM	FoldX	RaSP
1SAK_A_F338A	0.66	0.5463	4.572	2.1404076	2.1	1.07524647487	-2.0934	0.9	0.567048	0.8238141898148867
5PTI_A_N24A	2.12	1.2373	0.1041	0.6778762	0.7	0.382988748	0.115158	-0.5	0.766338	0.892086238
1RG8_A_C16S	2.01	0.3742	0.1334	1.281904	1.4	3.01222517238	2.90558	1.9	1.0886	1.758955752651941
3OJM_A_K127D	0.62	-0.1659	0.239	0.07103062	-0.4	0.676603256	-6.13512	0.8	-0.734569	0.464097051
1LZ1_A_V110N	-0.06	0.2837	0.2856	0.26195014	0.8	0.64712527087	-0.073332	0.2	-0.526365	0.4073131118005857
```

**Note：**

(1) The **pdb_mut** column represents the mutation along with the PDB ID and chain where the mutation occurs. 

(2) Different columns in the table are separated by tabs.

(3) Column names (the names of the 10 tools) should adopt the most canonical nomenclature. Please follow the format shown in this example.


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

•	**Disk Space:** ≥120 GB (Docker image: ~99.7 GB + additional space for data and output)















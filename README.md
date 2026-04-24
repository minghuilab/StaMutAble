# StaMutAble
## About

StaMutAble is a computational framework for predicting mutation-induced protein stability changes, with a focus on improving the identification of stabilizing mutations. It integrates predictions from ten existing tools—PremPS, ThermoMPNN, MultiMutate, RaSP, FoldX, ACDC-NN, MAESTRO, ThermoNet, SimBa-SYM, and DDGun3D—as input features and trains ensemble random forest models on datasets balanced between destabilizing and stabilizing mutations. The framework provides two models: RF-Ensemble-BalAvg for regression and RF-Ensemble-BalVote for classification, enabling more accurate, robust, and balanced predictions, particularly for stabilizing mutations.


## StaMutAble Installation and Usage Instructions


### 1. Pull Docker Image

For the easiest setup, pull the public Docker image. Make sure Docker is installed: https://docs.docker.com/get-started/get-docker/

```
wget https://huggingface.co/liuyang9529/StaMutAble/blob/main/stamutable_flat.tar.gz
gunzip -c stamutable_flat.tar.gz | docker import - minghuilab/stamutable:v1
```


•  After decompression, the image is about 113 GB.  
•  Estimated download time depends on your network speed.


### 2. Run the Docker Container and Activate Environment

```
docker run -it minghuilab/stamutable:v1 /bin/bash
cd stamutable
```

### 3. Download RF models, Required Dependencies and Databases

Due to size limitations on Docker image uploads, the remaining files are provided through alternative distribution methods.

We have released all five regression models and five classification models on Hugging Face. You can download them using the following commands and place them in the specified directory.

**(1) Download RF models**

```
wget -O /stamutable/models/cls_1/mega1_3000_2_model.pkl https://huggingface.co/liuyang9529/StaMutAble/resolve/main/cls_mega1_3000_2_model.pkl
wget -O /stamutable/models/cls_2/mega2_7500_2_model.pkl https://huggingface.co/liuyang9529/StaMutAble/resolve/main/cls_mega2_7500_2_model.pkl
wget -O /stamutable/models/cls_3/mega3_6000_2_model.pkl https://huggingface.co/liuyang9529/StaMutAble/resolve/main/cls_mega3_6000_2_model.pkl
wget -O /stamutable/models/cls_4/mega4_8000_1_model.pkl https://huggingface.co/liuyang9529/StaMutAble/resolve/main/cls_mega4_8000_1_model.pkl
wget -O /stamutable/models/cls_5/mega5_5000_1_model.pkl https://huggingface.co/liuyang9529/StaMutAble/resolve/main/cls_mega5_5000_1_model.pkl

wget -O /stamutable/models/reg_1/mega1_3000_2_model.pkl https://huggingface.co/liuyang9529/StaMutAble/resolve/main/reg_mega1_3000_2_model.pkl
wget -O /stamutable/models/reg_2/mega2_5500_2_model.pkl https://huggingface.co/liuyang9529/StaMutAble/resolve/main/reg_mega2_5500_2_model.pkl
wget -O /stamutable/models/reg_3/mega3_4000_2_model.pkl https://huggingface.co/liuyang9529/StaMutAble/resolve/main/reg_mega3_4000_2_model.pkl
wget -O /stamutable/models/reg_4/mega4_3500_2_model.pkl https://huggingface.co/liuyang9529/StaMutAble/resolve/main/reg_mega4_3500_2_model.pkl
wget -O /stamutable/models/reg_5/mega5_3500_2_model.pkl https://huggingface.co/liuyang9529/StaMutAble/resolve/main/reg_mega5_3500_2_model.pkl
```

**(2) Download Rosetta to run ThermoNet**

Install Rosetta 3.10

Obtain an academic license for Rosetta from: https://els2.comotion.uw.edu/product/rosetta

Download Rosetta 3.10 (including both source code and Linux binaries) from: https://www.rosettacommons.org/software/license-and-download

Extract the downloaded tarball to a local directory. Ensure that the Rosetta executables can be accessed by specifying their full path (or by adding the directory to your PATH environment variable).

```
cd /stamutable/methods10/ThermoNet
wget https://downloads.rosettacommons.org/downloads/academic/3.10/rosetta_bin_linux_3.10_bundle.tgz
tar -xzvf rosetta_bin_linux_3.10_bundle.tgz -C /stamutable/methods10/ThermoNet
```





**(3) Download uniclust30 to run DDGun3D**

```
cd /stamutable/methods10/DDGun3D/ddgun-master/data/
wget -c http://wwwuser.gwdg.de/~compbiol/uniclust/2018_08/uniclust30_2018_08_hhsuite.tar.gz
tar -xzvf uniclust30_2018_08_hhsuite.tar.gz
```




### 4. Preparing Input files and Dictionaries

**Please prepare an input directory, and name the input file as <folder_name>_input.txt.**

Example: The program requires an input directory named **/stamutable/example_5B83_1mut/**, which should contain the mutation file [**example_5B83_1mut_input.txt**](/example_5B83_1mut/example_5B83_1mut_input.txt).

The reference format for the input file is shown below:

```
PDB ID  MutChain        mutation
5B83    A       Y135K
5B83    A       G205R
5B83    A       V222P
```

**Note：**

(1) The **PDB ID** column lists the corresponding PDB identifiers.
The **MutChain** column indicates the chain in which the mutation occurs.
The **mutation** column lists the single-point mutations for the given protein.

(2) Different columns in the table are separated by tabs.

(3) Please ensure that PDB structure filenames do not contain underscores (_) and are consistent with the PDB IDs listed in the PDB ID column of the input mutation file.


### 5. Running StaMutAble

(1) You can run the program by editing the run_prediction.sh script .

You only need to fill in the first line, **job_name**, with the name of the directory you have defined.

For examples, you can set **job_name** to **example_5B83_1mut** or **example_1L8W_1mut**, as shown in /stamutable/run_prediction_example_5B83_1mut.sh and /stamutable/run_prediction_example_1L8W_1mut.sh.


```
job_name=""     # e.g. : example_5B83_1mut or example_1L8W_1mut
base_dir="/stamutable/${job_name}/"

input_muts="${base_dir}/${job_name}_input.txt"
input_pdbs="${base_dir}/input_pdbs"
output_pdbs="${base_dir}/pdbs"

methods10_input="${base_dir}/${job_name}.txt"
methods10_output="/stamutable/methods10_output/"

predicting_output="/stamutable/${job_name}_output/"
predicting_muts="/stamutable/${job_name}_predictions10.txt"
output_pdbs="${base_dir}/pdbs/"
mkdir -p "$output_pdbs"
```










(2) Running prediction
```
sh run_prediction.sh
```

Run two examples: **example_5B83_1mut** and **example_1L8W_1mut**.
```
sh run_prediction_example_5B83_1mut.sh
sh run_prediction_example_1L8W_1mut.sh
```


### 6. Recommended System Requirements

•	**RAM:** ≥120 GB recommended (≥110 GB minimal requirement)

•	**Disk Space:** ≥340 GB (Docker image: including ~113 GB for the Docker image, ~87 GB for the UniClust30_2018_08 protein database, ~33 GB for Rosetta, plus additional space for data and outputs)















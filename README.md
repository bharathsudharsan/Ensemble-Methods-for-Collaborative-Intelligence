# Combining Ubiquitous ML Models in IoT

The concept of ***ML model aggregation rather than data aggregation*** has gained much attention as it boosts prediction performance while maintaining stability and preserving privacy. In a non-ideal scenario, there are chances for a base model trained on a single device to make independent but complementary errors. To handle such cases, in this repo, we implement 8 robust ML model combining methods that achieves reliable prediction results by combining numerous base models (trained on many devices) to form a central model that effectively limits errors, built-in randomness and uncertainties.

The contributions of this work can be summarized as follows:

- The studies from centralized learning, split learning, distributed ensemble learning have extensively investigated combining models trained on devices like smartphones, Raspberry Pis, Jetson Nanos, etc. Such devices have sufficient resources to train base models (or ensembles) using standard training algorithms from Python Scikit-learn or light version ML frameworks like TensorFlow Lite. In contrast, we aim to achieve collective intelligence using MCUs, since billions of deployed IoT devices like HVAC controllers, smart meters, video doorbells have resource-constrained MCU-based hardware with only a few MB of memory. 

- From the available multitudinous number of studies, we choose, implement, and provide 8 robust ML model combining methods that are compatible with a wide range of datasets (varying feature dimensions and classes) and IoT devices (heterogeneous hardware specifications). We open-source the implementation, utilizing which researchers and engineers can start practicing distributed ensemble learning by combining ML base models trained on ubiquitous IoT devices.

## Table of Contents

- [Medical Data Usecase](#medical-data-usecase)
- [Algorithms for Combining ML Models](#algorithms-for-combining-ml-models)
  * [Dependencies](#dependencies)	
- [Devices and Datasets for Experiments](#devices-and-datasets-for-experiments)
- [Experiments: Distributed Train then Combine](#experiments--distributed-train-then-combine)
  * [Procedure](#procedure)
  * [Results Analysis](#results-analysis)
  * [Observations](#observations)
- [Useful Books, Toolboxes and Datasets](#useful-books--toolboxes-and-datasets)
  * [Books](#books)
  * [Toolboxes](#toolboxes)
  * [Datasets](#datasets)
- [Classic Papers](#classic-papers)
  * [Overview & Survey](#overview---survey)
  * [Boosting](#boosting)
  * [Clustering Ensemble](#clustering-ensemble)
  * [Outlier Ensemble](#outlier-ensemble)
  * [Ensemble Learning for Data Stream](#ensemble-learning-for-data-stream)
  * [Key Algorithms](#key-algorithms)
- [Source and Ranking Portals](#source-and-ranking-portals)
- [Reputed Data Mining Conferences/Workshops/Journals](#reputed-data-mining-conferences-workshops-journals)
  * [Conferences and Workshops](#conferences-and-workshops)
  * [Journals](#journals)
- [Doing Good Research and Get it Published](#doing-good-research-and-get-it-published)


## Medical Data Usecase

The **Providing sensitive medical data for research** use case can be a potential application where **Combining ML Models** can be utilized.

![alt text](https://github.com/bharathsudharsan/ML-Model-Combining/blob/master/Medical_data_usecase.png)

The data required for most research are sensitive in nature, as it revolves around a private individual. So, GDPR restricts sending such sensitive yet valuable medical data (from hospitals, imaging centers) to research institutes. As shown in above Fig, when the resource-constrained medical devices like insulin-delivery devices, BP apparatus are equipped with IoT hardware-friendly training algorithms like [ML-MCU](https://github.com/bharathsudharsan/ML-MCU), or [Train++](https://github.com/bharathsudharsan/Train_plus_plus), they can perform onboard training of base models, even without depending on the hospital’s local servers. After training, the base models from similar devices can be extracted, combined, and sent to research labs with improved data privacy preservation. For example, the 2 base models *M7<sub>1</sub>*, *M7<sub>2</sub>* (see above Fig) trained on ECG monitors using vital data of patients can be combined centrally, then shared for research. 

## Algorithms for Combining ML Models

To enable ***combining ML models rather than combining distributed data***, we select, implement and provide 8 robust methods that apply to a variety of IoT use-case data while also suitable for combining models trained on heterogeneous IoT devices.

| **Algorithm**                                                                       | **Source**                                                                                                                                               | **Implementation Code**                                                                                                                                 |
| :---------------------------------------------------------------------------------- | :------------------------------------------------------------------------------------------------------------------------------------------------------- | :------------------------------------------------------------------------------------------------------------------------------------------------------ |
| Simple Average                                                                      | [Ensemble Methods: Foundations and Algorithms](https://dl.acm.org/doi/10\.5555/2381019)                                                                  | [Average\_Maximization\_Voting\_Median.py](https://github.com/bharathsudharsan/ML-Model-Combining/blob/master/Average\_Maximization\_Voting\_Median.py) |
| Weighted Average: Average across all scores/prediction results                      | [Ensemble Methods: Foundations and Algorithms](https://dl.acm.org/doi/10\.5555/2381019)                                                                  | [Average\_Maximization\_Voting\_Median.py](https://github.com/bharathsudharsan/ML-Model-Combining/blob/master/Average\_Maximization\_Voting\_Median.py) |
| Maximization: Simple combination by taking the maximum scores                       | [Ensemble Methods: Foundations and Algorithms](https://dl.acm.org/doi/10\.5555/2381019)                                                                  | [Average\_Maximization\_Voting\_Median.py](https://github.com/bharathsudharsan/ML-Model-Combining/blob/master/Average\_Maximization\_Voting\_Median.py) |
| Weighted Majority Vote                                                              | [Ensemble Methods: Foundations and Algorithms](https://dl.acm.org/doi/10\.5555/2381019)                                                                  | [Average\_Maximization\_Voting\_Median.py](https://github.com/bharathsudharsan/ML-Model-Combining/blob/master/Average\_Maximization\_Voting\_Median.py) |
| Median: Take the median value across all scores/prediction results                  | [Ensemble Methods: Foundations and Algorithms](https://dl.acm.org/doi/10\.5555/2381019)                                                                  | [Average\_Maximization\_Voting\_Median.py](https://github.com/bharathsudharsan/ML-Model-Combining/blob/master/Average\_Maximization\_Voting\_Median.py) |
| Dynamic Classifier Selection (DCS)                                                  | [Combination of multiple classifiers using local accuracy estimates](https://ieeexplore.ieee.org/document/588027)                                        | [DCS-LA.py](https://github.com/bharathsudharsan/ML-Model-Combining/blob/master/DCS-LA.py)                                                               |
| Dynamic Ensemble Selection (DES)                                                    | [From dynamic classifier selection to dynamic ensemble selection](https://citeseerx.ist.psu.edu/viewdoc/download?doi=10\.1.1.139.4165&rep=rep1&type=pdf) | [DES-LA.py](https://github.com/bharathsudharsan/ML-Model-Combining/blob/master/DES-LA.py)                                                               |
| Stacking (meta ensembling): Use a meta learner to learn the base classifier results | [A Kaggler’s Guide to Model Stacking in Practice](https://datasciblog.github.io/2016/12/27/a-kagglers-guide-to-model-stacking-in-practice/)              | [Stacking.py](https://github.com/bharathsudharsan/ML-Model-Combining/blob/master/Stacking.py)                                                           |

### Dependencies

- Python 3.5, 3.6, or 3.7
- joblib
- matplotlib (optional for running examples)
- numpy>=1.13
- numba>=0.35
- pyod
- scipy>=0.19.1
- scikit_learn>=0.20

## Devices and Datasets for Experiments 

**Devices:** Distributed, ubiquitous IoT Devices in the real world have heterogeneous hardware specifications. To replicate this scenario, the devices chosen to carry out the distributed training, given in below Table, contains 10 resource-constrained MCU boards (B1-B10) and 5 CPU devices (C1-C5). 

|                                                                       | Board\#: **Name**      | **Specs: Processor flash, SRAM, clock (MHz)**  |
| :-------------------------------------------------------------------- | :--------------------- | :--------------------------------------------- |
|                                                                       | B1: nRF52840 Feather   | Cortex-M4, 1MB, 256KB, 64                      |
|                                                                       | B2: STM32f10 Blue Pill | Cortex-M0, 128kB, 20KB, 72                     |
|                                                                       | B3: Adafruit HUZZAH32  | Xtensa LX6, 4MB, 520KB, 240                    |
|                                                                       | B4: Raspberry Pi Pico  | Cortex-M0+, 16MB, 264KB, 133                   |
| ********************************MCUs********************************  | B5: ATSAMD21 Metro     | Cortex-M0+, 256kB, 32KB, 48                    |
|                                                                       | B6: Arduino Nano 33    | Cortex-M4, 1MB, 256KB, 64                      |
|                                                                       | B7: Teensy 4\.0        | Cortex-M7, 2MB, 1MB, 600                       |
|                                                                       | B8: STM32 Nucleo H7    | Cortex-M7, 2MB, 1MB, 480                       |
|                                                                       | B9: Feather M4 Express | Cortex-M4, 2MB, 192KB, 120                     |
|                                                                       | B10: Arduino Portenta  | Cortex-M7+M4, 2MB, 1MB, 480                    |
|                                                                       | **CPU\#: Name**        | **Basic specs**                                |
|                                                                       | C1: W10 Laptop         | Intel Core i7 @1\.9GHz                         |
|                                                                       | C2: NVIDIA Jetson Nano | 128-core GPU @1\.4GHz                          |
| **CPUs**                                                              | C3: W10 Laptop         | Intel Core i5 @1\.6GHz                         |
|                                                                       | C4: Ubuntu Laptop      | Intel Core i7 @2\.4GHz                         |
|                                                                       | C5: Raspberry Pi 4     | Cortex-A72 @1\.5GHz                            |

**Datasets:** Below datasets are used for training on the above MCUs and CPUs.

1. [Banknote Authentication](https://archive.ics.uci.edu/ml/datasets/banknote+authentication) (5 features, 2 classes, 1372 samples) <br/>
2. [Haberman's Survival](https://archive.ics.uci.edu/ml/datasets/Haberman's+Survival) (3 features, 2 classes, 306 samples) <br/>
3. [Titanic](https://www.kaggle.com/c/titanic/data) (11 features, 2 classes,  1300 samples) <br/>

## Experiments: Distributed Train then Combine

### Procedure

The training process on all 15 devices is carried out using the resource-friendly classifier training algorithm from [ML-MCU](https://ieeexplore.ieee.org/document/9490288).

Initially, for the Banknote dataset, upon all devices completing the training, 15 base models are obtained (first set). Then, each of the 8 ML model combining methods are one by one applied on this first set of models, producing 8 central models (one central model as an output of each combining method). A similar procedure was followed for the remaining datasets, producing the second and third set of models, followed by model combining. At this stage, there are 8 central models for each dataset, whose performance was evaluated in terms of Accuracy, ROC, and F1 score (F1) metrics and reported in below Fig. 

### Results Analysis

Here, using the below Fig, performance of combined central models are analyzed.

![alt text](https://github.com/bharathsudharsan/ML-Model-Combining/blob/master/Performance_of_combined_models.png)

**Banknote Authentication dataset:** The highest performance is shown by the Dynamic Classifier Selection (DCS-LA) method. Followed by Maximization, then the Median combination method, where both show the same accuracy and slightly different ROC and F1. The Simple Averaging, Weighted Averaging, and the Weighted Majority Vote (WMV) methods achieve similar performance. The combine by Stacking is the least performing, followed by Dynamic Ensemble Selection (DES) method. 

**Haberman's Survival dataset:** Again, DCS-LA showed the top performance. The DES and Stacking methods that produced a low performance for the previous dataset are the second and third best-performing methods. The other algebraic, averaging, and voting methods perform almost the same, achieving good accuracy and F1 but low ROC. 

**Titanic dataset:** Stacking shows the highest accuracy, but DES achieved slightly higher ROC and F1 so, DES is the overall top-performing method. Unlike in previous datasets, here, the algebraic (combine by Maximization and Median), Averaging, and Voting methods show varying performance. From the algebraic methods, the combine by Median performed better. From averaging methods, Simple Averaging performed better.

### Observations

The following observation were made during experimentation:
1. The computational cost for creating an ensemble is not much higher than training a single base model. It is because multiple versions of the base model need to be generated during parameter tuning. Also, the computational cost for combining multiple IoT devices trained base models was small due to the simplicity of the presented combination strategies.
2. To construct a good ensemble, it is recommended to create base models ***as accurate and as diverse as possible***. 
3. Creating a learning algorithm that is consistently better than others is a hopeless daydream. i.e., from above Fig, Stacking shows top performance for the Titanic dataset and least in the Banknote dataset.

## Useful Books, Toolboxes and Datasets

### Books

1. [Ensemble Methods: Foundations and Algorithms](https://www.crcpress.com/Ensemble-Methods-Foundations-and-Algorithms/Zhou/p/book/9781439830031): Classical text book covering most of the ensemble learning techniques.
A **must-read** for people in the field

2. [Ensemble Machine Learning: Methods and Applications](https://link.springer.com/book/10.1007%2F978-1-4419-9326-7): Responding to a shortage of literature dedicated to the topic, this volume offers comprehensive coverage of state-of-the-art ensemble learning techniques,
including various contributions from researchers in leading industrial research labs.

3. [Applications of Supervised and Unsupervised Ensemble Methods](https://www.springer.com/gp/book/9783642039980): This book contains the extended papers presented at the 2nd Workshop on Supervised and Unsupervised Ensemble Methods and their Applications (SUEMA), in conjunction with ECAI.

4. [Data Mining and Knowledge Discovery Handbook](https://link.springer.com/chapter/10.1007/0-387-25465-X_45) Chapter 45 (Ensemble Methods for Classifiers): This chapter provides an overview of ensemble methods in classification tasks. We present all important types of ensemble method including boosting and bagging.
Combining methods and modeling issues such as ensemble diversity and ensemble size are discussed.

5. [Outlier Ensembles: An Introduction](https://www.springer.com/gp/book/9783319547640): Great intro book for ensemble learning in outlier analysis.

### Toolboxes

1. [combo](https://github.com/yzhao062/combo): combo is a comprehensive Python toolbox for combining machine learning (ML) models and scores for various tasks, including classification, clustering, and anomaly detection. It supports the combination of ML models from core libraries such as scikit-learn and xgboost.

2. [pycobra](https://github.com/bhargavvader/pycobra):  python library implementing ensemble methods for regression, classification and visualisation tools including Voronoi tesselations.

3. [DESlib](https://github.com/scikit-learn-contrib/DESlib):  A Python library for dynamic classifier and ensemble selection.

4. [imbalanced-learn](https://github.com/scikit-learn-contrib/imbalanced-learn):  A Python Package to Tackle the Curse of Imbalanced Datasets in Machine Learning.


### Datasets

As a subfield of machine learning, ensemble learning is usually tested against
general machine learning benchmark datasets. Some helpful links can be found below:

1. [List of datasets for machine-learning research - Wikipedia](https://en.wikipedia.org/wiki/List_of_datasets_for_machine-learning_research)
2. [UCI Machine Learning Repository](http://archive.ics.uci.edu/ml/index.php)
3. [PMLB: a large benchmark suite for machine learning evaluation and comparison](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC5725843/): [Dataset Repository](https://github.com/EpistasisLab/penn-ml-benchmarks)

## Classic Papers

### Overview & Survey

1. Ensemble methods in machine learning @MCS. [PDF](http://citeseerx.ist.psu.edu/viewdoc/download?doi=10.1.1.34.4718&rep=rep1&type=pdf)
2. Popular ensemble methods: An empirical study @JAIR. [PDF](https://www.d.umn.edu/~rmaclin/publications/opitz-jair99.pdfP)
3. Ensemble learning: A survey @ Wiley Interdisciplinary Reviews. [PDF](https://onlinelibrary.wiley.com/doi/pdf/10.1002/widm.1249)

### Boosting

1. Xgboost: A scalable tree boosting system @ KDD. [PDF](https://dl.acm.org/ft_gateway.cfm?ftid=1775849&id=2939785)
2. Lightgbm: A highly efficient gradient boosting decision tree @ NIPS. [PDF](https://papers.nips.cc/paper/6907-lightgbm-a-highly-efficient-gradient-boosting-decision-tree.pdf)
3. CatBoost: unbiased boosting with categorical features @ NIPS. [PDF](https://papers.nips.cc/paper/7898-catboost-unbiased-boosting-with-categorical-features.pdf)

### Clustering Ensemble

1. Cluster Ensembles – A Knowledge Reuse Framework for Combining Multiple Partitions @ JMLR. [PDF](http://strehl.com/download/strehl-jmlr02.pdf)
2. Clusterer Ensemble @ KBS. [PDF](https://cs.nju.edu.cn/zhouzh/zhouzh.files/publication/kbs06.pdf)
3. A survey of clustering ensemble algorithms @ IJPRAI. [PDF](https://pdfs.semanticscholar.org/0d1b/7d01fb2634b6160a96bbdd73f918ed3859cb.pdf)
4. Clustering ensemble method @ Cybernetics. [PDF](https://www.researchgate.net/publication/322520921_Clustering_ensemble_method)

### Outlier Ensemble

1. Outlier ensembles: position paper @ SIGKDD Explorations. [PDF](https://pdfs.semanticscholar.org/841e/ce7c3812bbf799c99c84c064bbcf77916ba9.pdf)
2. Ensembles for unsupervised outlier detection: challenges and research questions a position paper @ SIGKDD Explorations. [PDF](http://www.kdd.org/exploration_files/V15-01-02-Zimek.pdf)
3. Isolation forest @ ICDM. [PDF](https://cs.nju.edu.cn/zhouzh/zhouzh.files/publication/icdm08b.pdf)
4. Outlier detection with autoencoder ensembles @ SDM. [PDF](http://saketsathe.net/downloads/autoencode.pdf)
5. An Unsupervised Boosting Strategy for Outlier Detection Ensembles @ PAKDD. [PDF](https://link.springer.com/chapter/10.1007/978-3-319-93034-3_45)
6. LSCP: Locally selective combination in parallel outlier ensembles @ SDM. [PDF](https://epubs.siam.org/doi/pdf/10.1137/1.9781611975673.66)

### Ensemble Learning for Data Stream

1. A survey on ensemble learning for data stream classification @ ACM Computing Surveys. [PDF](https://www.researchgate.net/publication/315698712_A_Survey_on_Ensemble_Learning_for_Data_Stream_Classification)
2. Ensemble learning for data stream analysis: A survey @Information Fusion. [PDF](http://www.math.chalmers.se/Stat/Grundutb/GU/MSA220/S18/DataStream-Classification.pdf)

### Key Algorithms

1. Bagging predictors @Machine Learning. [PDF](https://link.springer.com/content/pdf/10.1007/BF00058655.pdf)
2. A decision-theoretic generalization of on-line learning and an application to boosting @JCSS. [PDF](https://pdfs.semanticscholar.org/5fb5/f7b545a5320f2a50b30af599a9d9a92a8216.pdf)
3. Bagging, Boosting @AAAI/IAAI. [PDF](http://www.cs.ecu.edu/~dingq/CSCI6905/readings/BaggingBoosting.pdf)
4. Stacked generalization @Neural Networks. [PDF](https://citeseerx.ist.psu.edu/viewdoc/download?doi=10.1.1.133.8090&rep=rep1&type=pdf)
5. Stacked regressions @Machine Learning. [PDF](https://link.springer.com/content/pdf/10.1007/BF00117832.pdf)

## Source and Ranking Portals

1. [CORE](http://portal.core.edu.au/conf-ranks/)
2. [ERA](http://www.conferenceranks.com/#)
3. [SJR](https://www.scimagojr.com/)

## Reputed Data Mining Conferences/Workshops/Journals

### Conferences and Workshops

1. [ACM International Conference on Knowledge Discovery and Data Mining (SIGKDD)](http://www.kdd.org/conferences)

2. [ACM International Conference on Management of Data (SIGMOD)](https://sigmod.org/)

3. [The Web Conference (WWW) ](https://www2018.thewebconf.org/)

4. [IEEE International Conference on Data Mining (ICDM)](http://icdm2018.org/)

5. [SIAM International Conference on Data Mining (SDM)](https://www.siam.org/Conferences/CM/Main/sdm19)

6. [IEEE International Conference on Data Engineering (ICDE)](https://icde2018.org/)

7. [ACM InternationalConference on Information and Knowledge Management (CIKM)](http://www.cikmconference.org/)

8. [ACM International Conference on Web Search and Data Mining (WSDM)](http://www.wsdm-conference.org/2018/)

9. [The European Conference on Machine Learning and Principles and Practice of Knowledge Discovery in Databases (ECML-PKDD)](http://www.ecmlpkdd2018.org/)

10. [The Pacific-Asia Conference on Knowledge Discovery and Data Mining (PAKDD)](http://pakdd2019.medmeeting.org)

### Journals

1. [ACM Transactions on Knowledge Discovery from Data (TKDD)](https://tkdd.acm.org/)

2. [IEEE Transactions on Knowledge and Data Engineering (TKDE)](https://www.computer.org/web/tkde)

3. [ACM SIGKDD Explorations Newsletter](http://www.kdd.org/explorations)

4. [Data Mining and Knowledge Discovery](https://link.springer.com/journal/10618)

5. [Knowledge and Information Systems (KAIS)](https://link.springer.com/journal/10115)


## Doing Good Research and Get it Published

[How to do good research, Get it published in SIGKDD and get it cited](http://www.cs.ucr.edu/~eamonn/Keogh_SIGKDD09_tutorial.pdf): A fantastic tutorial on by Prof. Eamonn Keogh (UC Riverside)

[Checklist for Revising a SIGKDD Data Mining Paper](https://web.cs.dal.ca/~eem/gradResources/KDD/Checklist%20for%20Revising%20a%20SIGKDD%20Data%20Mining%20Paper.pdf): A concise checklist by Prof. Eamonn Keogh (UC Riverside)

[How to Write and Publish Research Papers for the Premier Forums in Knowledge & Data Engineering](http://acsic.org/files/Writing16-Web.pdf): A tutorial on how to structure data mining papers by Prof. Xindong Wu (University of Louisiana at Lafayette)

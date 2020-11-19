# Fake news detection based on the induction of fuzzy sets
This git repository shows the work of Giovanni Laganà's final thesis of his master's degree at Università degli Studi di Milano, about the extension of the algorithm described in [1], observing how the choice of input formatting techniques [2] will affect the learning results, focusing on the problem of detecting the reliability score of news published on online newspapers.

# Architecture
![architecture](architecture.png)

# Repository structure
This repository is structured as follows:
- modules:
    * ```main_kaggle.py```: the module which downloads the dataset from Kaggle
    * ```main_preprocessing.py```: the module that runs a preprocessing pipeline
    * ```main_model_selection.py```: the module that select the best model through a grid search
    * ```main_experiment.py```: the module that launches the experiments and stores them in a .csv file
    * ```main_results_viewer.py```: the module that reads the experiments from the .csv file generated by the previous module

- classes:
    * ```experiment.py```: the class responsible for creating, fitting and using a predicitive model through the [mulearn](https://github.com/dariomalchiodi/mulearn) package
    * ```model.py```: the class for the models that we want to build and use
    * ```ppsteps.py```: the class that implements fit and transform functions, according to scikit-learn's [convention](https://scikit-learn.org/stable/developers/develop.html)
    * ```preprocessing.py```: the class to configure the preprocessing pipeline with the operations that we want 
    
    Note: these files are grouped in ```classes``` folder.
- test:
    * ```test_ppsteps.py```: the file where unitary tests are executed
    
- generated files (not shown in this repository):
    * ```datasets/fakeandreal/Fake.csv, True.csv```: the two files from the dataset loaded from Kaggle
    * ```preprocessed_datasets/test/, train/```: the folder containing the preprocessed datasets divided into train and test sets
    * ```images/```: the folder containing all scatterplots generated by the experiments
    * ```results/experiments.csv```: the dataframe containing the configuration of experiments and their results

# Datasets (updated on 29/06/2020)
Currently, two main interesting datasets about web news have been found.
1. [Fake and real news dataset](https://www.kaggle.com/clmentbisaillon/fake-and-real-news-dataset?select=Fake.csv), 111 MB
2. [All the News 2.0](https://components.one/datasets/all-the-news-2-news-articles-dataset/), 9.2 GB 

# Datasets loading
The two datasets presented in the section above are not included in this repository to avoid inefficiency.
The module ```main_kaggle.py``` automatically downloads data from Kaggle (currently this is done for dataset 1). 
Before executing the code, please configure the Kaggle's API by the following steps:

* make sure to have Python 3 installed and correctly configured
* install the Kaggle's API by typing in console ```pip3 install kaggle```
* register to the Kaggle website
* go to ```https://www.kaggle.com/<username>/account``` and click the button "Create New API Token"
* the file downloaded in the previous step (```kaggle.json```) contains the credentials to login to the kaggle website: do not share with anyone
* Move this file to ```~/.kaggle/``` folder in Mac and Linux (if not present just create it) or to ```C:\Users\.kaggle\``` on windows.
Alternatively, you can populate KAGGLE_USERNAME and KAGGLE_KEY environment variables with values from kaggle.json to get the api to authenticate.

For any doubts, i recommend to read this very good [guide](https://technowhisp.com/kaggle-api-python-documentation/).

When all steps above are done, you can safely run ```main_kaggle.py```.
This script has the effect of creating a folder ```datasets/fakeandreal``` in your repository. 
This folder contains two .csv files, respectively about fake and real news.

# Dataset Preprocessing
Once your data is loaded into ```datasets``` folder, you can run ```main_preprocessing.py```.
This module has the effect of generating the preprocessed datasets in ```preprocessed_datasets``` folder.

# Learning
Assuming you have a preprocessed dataset in ```preprocessed_datasets``` folder, you can run ```main_experiment.py``` in order to launch an experiment with a specific configuration.
This experiment is directly stored in ```results/experiments.csv``` file.
Whenever the plot flag is enabled, scatterplots are saved in ```images``` folder.

# Display of Results
When you want to display final results, you can run ```main_results_viewer.py``` to show the experiments outcome. 

# Bibliography
* [1] Learning Membership Functions for Fuzzy Sets through Modified Support Vector Clustering,
in F. Masulli, G. Pasi e R. Yager (Eds.), Fuzzy Logic and Applications. 10th International Workshop,
WILF 2013, Genoa, Italy, November 19–22, 2013. Proceedings., Vol. 8256, Springer International
Publishing, Switzerland, Lecture Notes on Artificial Intelligence (ISBN 978-3-319-03199-6), 52–59, 2013.  

* [2] Schütze, H., Manning, C. D., & Raghavan, P. (2008). Introduction to information retrieval 
Vol. 39, pp. 1041-4347). Cambridge: Cambridge University Press.  

* [3] Mikolov, T., Chen, K., Corrado, G., and Dean, J. (2013). Efficient estimation of word representations in vector space. arXiv preprint arXiv:1301.3781.
 Pham, T. T. (2018). A study on deep learning for fake news detection.  

* [4] Wardle, C. (2017). Fake news. it’s complicated. First Draft News.  

* [5] Andreas Vlachos and Sebastian Riedel. Fact checking: Task definition and dataset construction. ACL’14.  

* [6] Naeemul Hassan, Chengkai Li, and Mark Tremayne. Detecting check-worthy factual claims in presidential debates. In CIKM’15.  

* [7] Michele Banko, Michael J Cafarella, Stephen Soder- land, Matthew Broadhead, and Oren Etzioni. Open information extraction from the web. In IJCAI’07.  

* [8] Amr Magdy and Nayer Wanas. Web-based statistical fact checking of textual documents. In Proceedings of the 2nd international workshop on Search and mining user-generated contents, pages 103–110. ACM, 2010.  

* [9] You Wu, Pankaj K Agarwal, Chengkai Li, Jun Yang, and Cong Yu. Toward computational fact-checking. Proceedings of the VLDB Endowment, 7(7):589–600, 2014.  

* [10] Baoxu Shi and Tim Weninger. Fact checking in het- erogeneous information networks. In WWW’16.    

* [11] Giovanni Luca Ciampaglia, Prashant Shiralkar, Luis M Rocha, Johan Bollen, Filippo Menczer, and Alessandro Flammini. Computational fact checking from knowledge networks. PloS one, 10(6):e0128193, 2015.  

* [12] V.L. Rubin, Y. Chen, N.J. Conroy, Deception detection for news: three types of fakes 52 (1) (2015) 1–4.  

* [13] N.J. Conroy, V.L. Rubin, Y. Chen, Automatic deception detection: methods for finding fake news 52 (1) (2015) 1–4.  

* [14] Ray Oshikawa, Jing Qian, William Yang Wang, A Survey on Natural Language Processing for Fake News Detection, Proceedings of the 12th Language Resources and Evaluation Conference (LREC 2020) pp. 6086-6093.  

* [15] Kai Shu, Amy Sliva, Suhang  Wang, Jiliang  Tang, Huan Liu, Fake News Detection on Social Media: A Data Mining Perspective, ACM SIGKDD Explorations Newsletter September 2017.  

* [16] Alessandro Bondielli, Francesco Marcelloni, A survey on fake news and rumour detection techniques, Information Sciences
 Volume 497, September 2019, Pages 38-55   

* [17] Xinyi Zhou, Reza Zafarani, A Survey of Fake News: Fundamental Theories, Detection Methods, and Opportunities   

* [18] Jose Camacho-Collados, Mohammad Taher Pilehvar, On the Role of Text Preprocessing in Neural Network Architectures: An Evaluation Study on Text Categorization and Sentiment Analysis

* [19] Ruqing Zhang et al. “Aggregating neural word embeddings for document repre-sentation”. In:European Conference on Information Retrieval. Springer. 2018,pp. 303–315.

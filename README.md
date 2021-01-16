# RACF

> RACF (**R**ecency **A**ware **C**ollaborative **F**iltering) is an implementation of the "_[Recency Aware Collaborative Filtering for Next Basket Recommendation]_"(https://dl.acm.org/doi/abs/10.1145/3340631.3394850) original paper.

> RACF is a set of collaborative filtering approaches for solving the problem of predicting the Next Basket Recommendation.



## Quick Start : 
You can start playing with this implementation either by downloading the provided Jupyter Notebook "__*RecencyAwareCF.ipynb*__" or by __*CLI*__ by cloning this repository.  

### Directory structure 
After cloning this git repository it would be strutured following this schema :
* NextBasketRecomSys
  * |-- src 
  * |--|-- main.py
  * |--|-- NextBasketRecFramework.py
  * |--|-- util.py
  * |-- data
  * |--|-- instacart
  * |--|-- dunnhumby

### Requirements:
* **Python 3.8+** (older version has not been tested)
* **Numpy 1.19+** (older version has not been tested)
* **Sklearn 0.23+** (older version has not been tested)
* **Pandas 1.0+**  (older version has not been tested)  
* **Similaripy** (Install it using the package installer Pip)
* **Scipy 1.5** (older version has not been tested)   
> A requirement file is available.

### Quick start with a subset of Instacart : 
> Please first download the complete [instacart dataset](https://www.instacart.com/datasets/grocery-shopping-2017) and release the CSV files under __*NextBasketRecomSys/data/instacart*__ path

Next, now you ready to run **main.py** by specifying some argument (in the following order):
* __Dataset path__:
  * --data_path : Path to the dataset folder (Default: ../data/instacart)
* __Data preprocessing args__:
  * --item_threshold : to Remove all items the appears with less than this number of baskets. (default:10)
  * --basket_threshold : to Remove all users with less than this number of baskets. (default:2)  
  * --subdata : to select a small subset of the current dataset to test the algorithms instantly. (default: 0.1) 
  * --verbose : to show data preprocessing progress Take True or False value (default:true)
* __Methods args__:
  * --method_name : the chose which method to use from the framework implementation :
    * __UWPop__ : **U**ser-**W**ise **Pop**ularity method
    * __UPCF__ : **U**ser **Pop**ularity **C**ollaborative **F**iltering method 
    * __IPCF__: **I**tem **Pop**ularity **C**ollaborative **F**iltering method
  * __Method's parameters__:
    * --recency : Default=0, in the paper they used the following values {1,5,25,100,inf)  
    * --asymmetry :  Default=0, in the paper they used the following values {0,0.25,0.5,0.75,1}  
    * --locality : Default=1, in the paper they used the following values {1,5,10,50,100,1000}
    * --top_k : rank-aware parameter, to select the number of items to recommend 
## Example of use: 
```
Python3 main.py --methode_name IPCF --recency 5 --asymmetry 1 --locality 5 --top_k 10
```
First, This will randomly sample transactions associated with __*10%*__ users and filter out products with __*<10 transactions*__ and users with less than __*2 baskets*__. 
Once the preprocessing is done, it will use the Item-popularity-CF(**IPCF@r**) method to predict the next __top 10 items__ to recommend using the following parameter (r=5, alpha=1, q=5).

And finally, it will show some the evaluation of the model in both test and train set.

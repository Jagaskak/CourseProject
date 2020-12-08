# Overview
This project attempts to reproduce the paper [Mining causal topics in text data: iterative topic modeling with time series feedback](https://dl.acm.org/doi/10.1145/2505515.2505612).

# GitHub structure
Each folder contains a README file that will explain more about the contents of the directory. 
The Data folder provides an overview/methodology of how to access the data and structure it to run our code.
The Results folder contains images of our results and a short analysis of what it means as well as interactive visualization.

# Run the code
We strongly suggest using Google Colab as it reduced the overhead of installing packages. 
The other option is to download the Jupyter Notebook and set it up on your local machine.
Make sure the data is stored locally. 

## To run on GoogleColab (will save a copy in your Google Drive)
1. Open the Jupyter notebook titled "ITMTF_GoogleColab.ibynb"
2. At the top of the notebook there is a link that says "Open in Colab"
3. Click the link and follow the instructions to give permissions to GoogleColab
4. The notebook should be located in My Drive. Edit the paths in the first cell to point to your data on your Google Drive
5. Run the cells

## To run locally
1. Clone this reproduce
2. Open the Juptyer notebook titled "ITMTF.ipynb"
3. Run the cells

## Code Examples
There is documentation for the main function (```ITMTF()```) which implements the topic modeling. An example of how to call it is below as well as in the notebook.

### ITMTF Function
Parameters:
```
paramCtrl  -- str (either 'k' or 'decay'), tells function to test various k or decay values
params     -- list of integers, each val in list is either a k or decay values to test.
              For k values, the last k value will be used to test a variable number of topics starting at k topics.
              In every iteration of ITMTF, k will increase by the number of causal topics found + some constant
decay      -- (0.5, 1] decay parameter to use when running lda (effective only when paramCtrl='k')
k          -- Interger representing number of topics to use when running lda (effective only when paramCtrl='decay')
iterations       -- Integer number of iterations to run ITMTF
const_k_increase -- Integer number of topics to increase (in addition to number of causal topics found) 
                    each iteration when running varying number of topics (effective only when paramCtrl='k')
                    Default is 0
verbose          -- True/False Print out purity and confidence every iteration
```
Returns:
```
k_lda_model    -- The final lda_model  
k_avg_purities -- Average purity of all causal topics in each iteration
k_avg_conf     -- Average confidence of all causal topics in each iteration
```

Example Calls: 
```
k_lda_model, k_avg_purities, k_avg_conf = ITMTF("k", params=[10, 20, 30, 40, 10])
mu_lda_model, mu_avg_purities, mu_avg_conf = ITMTF("decay", params=[0.51, 0.6, 0.7, 0.8, 0.9, 1])
```


### Standard Graph Visualizations
These visualizations are built using matplotlib.plotly. The function ```show_plot()``` is a wrapper for the plotly function ```plot()```.
```
k_labels = ["10", "20", "30", "40", "Varying Number of Topics"]
show_plot(range(1, 6), k_avg_purities, 
          "Iteration", "Average Purity",     
          k_labels, 
          xticks=range(1, 6), yaxisrange=[0, 120], 
          title="Average Purity for Different Number of Topics",
          legend_title="Number of Topics",
          saveAs="purity_k.png")
show_plot(range(1, 6), k_avg_conf,     
          "Iteration", "Average Confidence", 
          k_labels, 
          xticks=range(1, 6), yaxisrange=[95.5, 100], 
          title="Average Confidence for Different Number of Topics",
          legend_title="Number of Topics",
          saveAs="confidence_k.png")

mu_labels = ["0.51", "0.6", "0.7", "0.8", "0.9", "1"]
show_plot(range(1, 6), mu_avg_purities, 
          "Iteration", "Average Purity", 
          mu_labels, 
          xticks=range(1, 6), yaxisrange=[0, 120], 
          title="Average Purity for Different Decay Values", 
          legend_title="Decay Values", 
          saveAs="purity_mu.png")
show_plot(range(1, 6), mu_avg_conf, 
          "Iteration", "Average Confidence", 
          mu_labels, 
          xticks=range(1, 6), yaxisrange=[95.5, 100], 
          title="Average Confidence for Different Decay Values", 
          legend_title="Decay Values", 
          saveAs="confidence_mu.png")
```

### Interactive Visualizations
These visualizations are built using pyLDAvis. The below example also includes an example of how to save the visualization.
```
pyLDAvis.enable_notebook()
vis = pyLDAvis.gensim.prepare(k_lda_model, corpus, id2word)
pyLDAvis.save_html(vis, 'LDAvis_k.html')

pyLDAvis.enable_notebook()
vis = pyLDAvis.gensim.prepare(mu_lda_model, corpus, id2word)
pyLDAvis.save_html(vis, 'LDAvis_mu.html')
```
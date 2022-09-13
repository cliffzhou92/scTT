# scTT

## Introduction
We present a single-cell transition tensor (scTT) method based on multi-stable attractor theory to integrate the multiple time-scale dynamics of gene expression, mRNA splicing and cell state-transitions, and rank the genes that characterizes the multi-stability. Overall, scTT provides a consistent dynamical description of single-cell transcriptome data across multiple scales. 

<img src="https://github.com/cliffzhou92/scTT/blob/main/img/figure_scheme.png" width="700">

## Basic Usage
```python
import sctt as st
adata.obs['attractor'] =  # initialize the attractor, can use leiden or original annotation
adata_aggr = st.dynamical_iteration(adata,n_states =K, n_iter = 20, weight_connectivities = 0.5, n_neighbors = 100, n_components = 20,thresh_ms_gene = 0,thresh_entropy = 0.1)
# n_states: number of attractors
# n_iter: maximum of iteration
# thresh_entropy: the threshold of maximum entropy difference between iterations to halt iteration, default is 0.1
# weight_connectivities: the weight of diffusion kernel as opposed to velocity kernel, default is 0.5
# n_neighbors: number of neghbors used to constrcut cellular random walk, default is 100
# n_component: number of eigen components to use in GPCCA decomposion, default is 20
# thresh_ms_gene: the threshold of minimum multi-stability score of genes to include when constructing random walk, default is 0
st.infer_lineage(adata,si=4,sf=3) # infer and plot the transition path
st.plot_tensor(adata, adata_aggr,  basis = 'trans_coord',list_attractor = [0,1,2,3]) # plot the transition tensor components
st.plot_top_genes(adata, top_genes = 10) # plot the U-S diagram of top genes with highest multi-stability score

```

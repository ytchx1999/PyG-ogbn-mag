# GraphSAINT + metapath2vec + FLAG
This is an improvement of the  [(GraphSAINT (R-GCN aggr))](https://github.com/snap-stanford/ogb/blob/master/examples/nodeproppred/mag/graph_saint.py)  model, using metapath2vec embedding. 

### ogbn-mag

+ Check out the model： [(GraphSAINT (R-GCN aggr))](https://github.com/snap-stanford/ogb/blob/master/examples/nodeproppred/mag/graph_saint.py)
+ Check out metapath2vec model：[metapath2vec](https://ericdongyx.github.io/papers/KDD17-dong-chawla-swami-metapath2vec.pdf)

#### Improvement Strategy：

+ adjust hidden_dim
+ add metapath2vec embedding
+ add FLAG method

#### Environmental Requirements

+ pytorch == 1.8.1
+ pytorch_geometric == 1.6.3
+ ogb == 1.3.0

#### Experiment Setup：

1. Generate metapath2vec embeddings, which save in `mag_embedding.pt`

   ```bash
   python metapath2vec.py
   ```

2. Run the real model

   ```bash
   python rgcn_saint.py
   ```


#### Detailed Hyperparameter:

GrapgSAINT:

```bash
num_layers = 2
hidden_dim = 256
dropout = 0.5
lr = 0.005
batch_size = 20000
walk_length = 2
runs = 10
epochs = 30
num_steps = 30
```

Metapath2vec:

```bash
embedding_dim = 128
lr = 0.01
batch_size = 20000
walk_length = 64
epochs = 5
```

#### Result:

```bash
All runs:
Highest Valid: 50.88 ± 0.18
   Final Test: 49.69 ± 0.22
```

| Model                            | Test Accuracy | Valid Accuracy | Parameters | Hardware          |
| -------------------------------- | ------------- | -------------- | ---------- | ----------------- |
| GraphSAINT + metapath2vec + FLAG | 49.69 ± 0.22  | 50.88 ± 0.18   | 309764724  | Tesla V100 (32GB) |


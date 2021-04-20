# GraphSAINT + metapath2vec + C&S
This is an improvement of the  [(GraphSAINT (R-GCN aggr))](https://github.com/snap-stanford/ogb/blob/master/examples/nodeproppred/mag/graph_saint.py)  model, using metapath2vec embedding. 

### ogbn-mag

+ Check out the model： [(GraphSAINT (R-GCN aggr))](https://github.com/snap-stanford/ogb/blob/master/examples/nodeproppred/mag/graph_saint.py)
+ Check out metapath2vec model：[metapath2vec](https://ericdongyx.github.io/papers/KDD17-dong-chawla-swami-metapath2vec.pdf)

#### Improvement Strategy：

+ adjust hidden_dim
+ add metapath2vec embedding
+ add C&S

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
num_correction_layers = 100
correction_alpha = 0.8
num_smoothing_layers = 100
smoothing_alpha = 0.8
scale = 1.
A1 = 'DAD'
A2 = 'DAD'
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
Highest Valid: 49.36 ± 0.24
   Final Test: 48.43 ± 0.24
```

| Model                           | Test Accuracy   | Valid Accuracy  | Parameters | Hardware          |
| ------------------------------- | --------------- | --------------- | ---------- | ----------------- |
| GraphSAINT + metapath2vec + C&S | 0.4843 ± 0.0024 | 0.4936 ± 0.0024 | 309764724  | Tesla V100 (32GB) |


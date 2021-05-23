# R-GSN + metapath2vec

This is an improvement of the [R-GSN](https://github.com/xjtuwxliang/R-GSN/tree/main) model, using metapath2vec embedding. 

[**Check out the OGBn-Mag LeaderBoard!**](https://ogb.stanford.edu/docs/leader_nodeprop/#ogbn-mag)

Our paper is available at [https://arxiv.org/pdf/2105.08330.pdf](https://arxiv.org/pdf/2105.08330.pdf).

### ogbn-mag

+ Check out the model： [R-GSN](https://github.com/xjtuwxliang/R-GSN/tree/main)
+ Check out metapath2vec model：[metapath2vec](https://ericdongyx.github.io/papers/KDD17-dong-chawla-swami-metapath2vec.pdf)

#### Improvement Strategy：

+ adjust hidden_dim
+ add metapath2vec embedding

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

   Delete history feat to prevent errors.
   
   ```bash
   cd rgsn+metapath2vec/
rm -r feat/
   ```
   
   Run rgsn+metapath2vec.
   
   ```bash
   python rgsn.py --use_attack True
   ```

#### Detailed Hyperparameter:

R-GSN:

```bash
+-----------------+-------+
| Parameter       | Value |
+-----------------+-------+
| device          | 0     |
+-----------------+-------+
| num_layers      | 2     |
+-----------------+-------+
| hidden_channels | 256   |
+-----------------+-------+
| dropout         | 0.500 |
+-----------------+-------+
| lr              | 0.004 |
+-----------------+-------+
| epochs          | 5     |
+-----------------+-------+
| runs            | 10    |
+-----------------+-------+
| batch_size      | 1024  |
+-----------------+-------+
| test_batch_size | 64    |
+-----------------+-------+
| opt             | adamw |
+-----------------+-------+
| early_stop      | 1     |
+-----------------+-------+
| feat_dir        | feat  |
+-----------------+-------+
| conv_name       | rgsn  |
+-----------------+-------+
| Norm4           | 1     |
+-----------------+-------+
| FDFT            | 1     |
+-----------------+-------+
| use_attack      | 1     |
+-----------------+-------+
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
Highest Train: 93.02 ± 0.07
Highest Valid: 52.95 ± 0.42
  Final Train: 79.91 ± 0.24
   Final Test: 51.09 ± 0.38
```

| Model                | Test Accuracy   | Valid Accuracy  | Parameters | Hardware          |
| -------------------- | --------------- | --------------- | ---------- | ----------------- |
| R-GSN + metapath2vec | 0.5109 ± 0.0038 | 0.5295 ± 0.0042 | 309777252  | Tesla V100 (32GB) |

```bash
Run 01:
Highest Train: 92.99
Highest Valid: 53.13
  Final Train: 80.13
   Final Test: 51.22
   
Run 02:
Highest Train: 93.04
Highest Valid: 52.14
  Final Train: 80.10
   Final Test: 50.66
   
Run 03:
Highest Train: 93.11
Highest Valid: 52.61
  Final Train: 80.03
   Final Test: 50.59
   
Run 04:
Highest Train: 92.99
Highest Valid: 53.56
  Final Train: 79.94
   Final Test: 51.72
   
Run 05:
Highest Train: 93.02
Highest Valid: 52.68
  Final Train: 80.04
   Final Test: 50.99
   
Run 06:
Highest Train: 93.10
Highest Valid: 52.80
  Final Train: 79.86
   Final Test: 50.64
   
Run 07:
Highest Train: 92.90
Highest Valid: 53.43
  Final Train: 79.31
   Final Test: 51.34
   
Run 08:
Highest Train: 93.01
Highest Valid: 53.02
  Final Train: 79.98
   Final Test: 51.06
   
Run 09:
Highest Train: 92.94
Highest Valid: 52.83
  Final Train: 79.97
   Final Test: 51.26
   
Run 10:
Highest Train: 93.12
Highest Valid: 53.26
  Final Train: 79.76
   Final Test: 51.43
```





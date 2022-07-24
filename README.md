# vansky-replication

## Setup

Open a terminal and navigate to an empty directory.

Download the language model:

`git clone 'https://github.com/vansky/neural-complexity.git'`

Download the natural stories corpus:

`git clone 'git@github.com:yatinlala/vansky-replication.git'`

Download the Wikitext corpus from Gulordava's "Colorless Green RNNs" [GitHub page](https://github.com/facebookresearch/colorlessgreenRNNs/tree/main/data):
```
mkdir full-wikitext
cd full-wikitext
wget 'https://dl.fbaipublicfiles.com/colorless-green-rnns/training-data/English/train.txt'
wget 'https://dl.fbaipublicfiles.com/colorless-green-rnns/training-data/English/valid.txt'
wget 'https://dl.fbaipublicfiles.com/colorless-green-rnns/training-data/English/test.txt'
wget 'https://dl.fbaipublicfiles.com/colorless-green-rnns/training-data/English/vocab.txt'
cd ..
```

Move natural stories and wikitext corpora into language model `data` directory:
```
mv full-wikitext neural-compexity/data/
mv vansky-replication/natstor neural-complexity/data/`
```

Make directories to store models and logs:
`mkdir logs`
`mkdir models`


## Train model

From the `neural-complexity` directory, run:
```
time python3 main.py --model_file 'full_wikitext.pt' --vocab_file './data/' --tied --cuda --data_dir './data/full-wikitext/' --trainfname 'train.txt' --validfname 'valid.txt' >> logs/FULL-WIKITEXT.TRAIN
```

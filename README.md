# vansky-replication

## Setup

The following directions should be followed sequentially:

- Open a terminal and navigate to an empty directory.

- Download the language model:

    `git clone 'https://github.com/vansky/neural-complexity.git'`

- Download the natural stories corpus:

    `git clone 'https://github.com/yatinlala/vansky-replication.git'`

- Download the Wikitext corpus from Gulordava's "Colorless Green RNNs" [GitHub page](https://github.com/facebookresearch/colorlessgreenRNNs/tree/main/data):
    ```
    mkdir full-wikitext
    cd full-wikitext
    wget 'https://dl.fbaipublicfiles.com/colorless-green-rnns/training-data/English/train.txt'
    wget 'https://dl.fbaipublicfiles.com/colorless-green-rnns/training-data/English/valid.txt'
    wget 'https://dl.fbaipublicfiles.com/colorless-green-rnns/training-data/English/test.txt'
    wget 'https://dl.fbaipublicfiles.com/colorless-green-rnns/training-data/English/vocab.txt'
    cd ..
    ```

- Move natural stories and wikitext corpora into language model `data` directory:
    ```
    mv full-wikitext vansky-replication/natstor
    cp neural-complexity/data vansky-replication/natstor
    ```
- Make directories to store models and logs:
    ```
    cd neural-complexity
    mkdir logs models
    ```
## Train model

From the `neural-complexity` directory, run:

`time python3 main.py --model_file './models/full-wikitext.pt' --vocab_file './data/full-wikitext/vocab.txt' --tied --batch_size 128 --lr 2 --dropout .2 --nhid 650 --emsize 650 --cuda --data_dir './data/full-wikitext/' --trainfname 'train.txt' --validfname 'valid.txt' > logs/FULL-WIKITEXT.TRAIN`

##  Obtain incremental complexity estimates

From the `neural-complexity` directory, run:

`time python3 main.py --model_file './models/full-wikitext.pt' --vocab_file './data/full-wikitext/vocab.txt' --cuda --single --data_dir './data/natstor/' --testfname 'naturalstories.linetoks' --test --words > logs/FULL-WIKITEXT.SURPRISAL`

## Adapt model to natural stories corpus

From the `neural-complexity` directory, run:

`time python3 main.py --model_file './models/full-wikitext.pt' --vocab_file './data/full-wikitext/vocab.txt' --cuda --single --data_dir './data/natstor/' --testfname 'naturalstories.linetoks' --test --words --adapt --adapted_model 'models/wikitext.naturalcorpus.1.pt' > logs/FULL-WIKITEXT.NATURALCORPUS.1.SURPISAL`


## Misc

Use model interactively
`time python3 main.py --model_file './models/full-wikitext.pt' --vocab_file './data/full-wikitext/vocab.txt' --cuda --interact`

TAT-DQA: Towards Complex Document Understanding By Discrete Reasoning
====================

**TAT-DQA** is a large-scale Document VQA dataset, which is constructed by extending the [TAT-QA](https://github.com/NExTplusplus/TAT-QA). It aims to stimulate progress of QA research over more complex and realistic visually-rich documents with rich tabular and textual content, especially those requiring numerical reasoning.


You can download our TAT-DQA dataset via [TAT-DQA Dataset](https://drive.google.com/drive/folders/1SGpZyRWqycMd_dZim1ygvWhl5KdJYDR2).
               
For more information, please refer to our [TAT-DQA Website](https://nextplusplus.github.io/TAT-DQA/) or read our ACM MM 2022 paper [PDF](https://arxiv.org/pdf/2207.11871.pdf).

## MHST Model

### Requirements

To create an environment with [MiniConda](https://docs.conda.io/en/latest/miniconda.html) and activate it.

```bash
conda create -n tat-dqa python==3.7.10
conda activate tat-dqa
pip install -r requirement.txt
pip install torch-scatter -f https://pytorch-geometric.com/whl/torch-1.7.0+${CUDA}.html
```


### Training & Testing

#### Preprocessing dataset

We heuristicly generate the "facts" and "block_mapping" fields based on raw dataset.


#### Prepare dataset

```bash
PYTHONPATH=$PYTHONPATH:$(pwd):$(pwd) python etr/prepare_dataset_tatdqa.py  —-encoder=layoutlm_v2 --mode [train/dev/test]
```

#### Train & Evaluation 
```bash
CUDA_VISIBLE_DEVICES=2 PYTHONPATH=$PYTHONPATH:$(pwd) python etr/trainer.py --data_dir dataset_tatdqa/ --save_dir ./checkpoint/model  --batch_size 64 --eval_batch_size 32 --max_epoch 30 --warmup 0.06 --optimizer adam --learning_rate 5e-4 --weight_decay 0.01 --seed 123 --gradient_accumulation_steps 8 --bert_learning_rate 1.5e-5 --bert_weight_decay 0.01 --tree_learning_rate 5e-4 --tree_weight_decay 0.01 --log_per_updates 50 --eps 1e-5 --encoder layoutlm_v2
```

Note: The training process may take around 2 days using a single 32GB v100.

### Citation

__Please kindly cite our work if you use our dataset or codes, thank you.__
```bash
@inproceedings{zhu2021tatqa,
    title = "{TAT}-{QA}: A Question Answering Benchmark on a Hybrid of Tabular and Textual Content in Finance",
    author = "Zhu, Fengbin  and
      Lei, Wenqiang  and
      Huang, Youcheng  and
      Wang, Chao  and
      Zhang, Shuo  and
      Lv, Jiancheng  and
      Feng, Fuli  and
      Chua, Tat-Seng",
    booktitle = "Proceedings of the 59th Annual Meeting of the Association for Computational Linguistics and the 11th International Joint Conference on Natural Language Processing (Volume 1: Long Papers)",
    month = aug,
    year = "2021",
    address = "Online",
    publisher = "Association for Computational Linguistics",
    url = "https://aclanthology.org/2021.acl-long.254",
    doi = "10.18653/v1/2021.acl-long.254",
    pages = "3277--3287"
}

@inproceedings{zhu2022towards,
  title={Towards complex document understanding by discrete reasoning},
  author={Zhu, Fengbin and Lei, Wenqiang and Feng, Fuli and Wang, Chao and Zhang, Haozhou and Chua, Tat-Seng},
  booktitle={Proceedings of the 30th ACM International Conference on Multimedia},
  pages={4857--4866},
  year={2022}
}
```

### Any Question?

For any issues please create an issue [here](https://github.com/nextplusplus/TAT-DQA/issues) or kindly email us at:
Fengbin Zhu [zhfengbin@gmail.com](mailto:zhfengbin@gmail.com), thank you.

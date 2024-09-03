# **SPrint: Self-Paced Continual Learning with Forgettable Samples**<br>
<img width="842" alt="overview3" src="https://github.com/user-attachments/assets/34e7a3a4-683c-4f30-80c0-d159e8013095">

## Abstract
Continual learning addresses the challenge of learning new concepts progressively without forgetting previously acquired knowledge, a problem known as catastrophic forgetting. While existing methods have shown high performance on specific datasets or model architectures, they often lack generalizability across diverse learning scenarios. To overcome this limitation, we propose a novel continual learning method, which dynamically adjust the difficulty of both training samples and in-memory samples in a self-paced manner based on the model’s evolving learning capacity. We empirically demonstrate that SPrint robustly outperforms state-of-the-art methods despite its simplicity.

## Getting Started
### Requirements 

- Python3
- Pytorch (>1.0)
- torchvision (>0.2)
- numpy
- pillow~=6.2.1
- torch_optimizer
- randaugment
- easydict
- pandas~=1.1.3

### Datasets
All the datasets are saved in `dataset` directory by following formats as shown below.

```angular2html
[dataset name] 
    |_train
        |_[class1 name]
            |_00001.png
            |_00002.png 
            ...
        |_[class2 name]
            ... 
    |_test (val for ImageNet)
        |_[class1 name]
            |_00001.png
            |_00002.png
            ...
        |_[class2 name]
            ...
```

### Usage 
To run the experiments in the paper, you just run `experiment.sh`.
```angular2html
bash experiment.sh 
```
For various experiments, you should know the role of each argument. 

- `MODE`: CIL methods. Our method is called `sprint`.
  (`joint` calculates accuracy when training all the datasets at once.)
- `MEM_MANAGE`: Memory management method. `default` uses the memory method which the paper originally used.
  [default, random, reservoir, uncertainty, prototype].
- `RND_SEED`: Random Seed Number 
- `DATASET`: Dataset name [cifar10, cifar100, imagenet100]
- `EXP`: Task setup [disjoint, blurry10]
- `MEM_SIZE`: Memory size
- `TRANS`: Augmentation. Multiple choices [cutmix, cutout, randaug, autoaug]

### Results
There are three types of logs during running experiments; logs, results, tensorboard. 
The log files are saved in `logs` directory, and the results which contains accuracy of each task 
are saved in `results` directory. 
```angular2html
root_directory
    |_ logs 
        |_ [dataset]
            |_{mode}_{mem_manage}_{stream}_msz{k}_rnd{seed_num}_{trans}.log
            |_ ...
    |_ results
        |_ [dataset]
            |_{mode}_{mem_manage}_{stream}_msz{k}_rnd{seed_num}_{trans}.npy
            |_...
```

In addition, you can also use the `tensorboard` as following command.
```angular2html
tensorboard --logdir tensorboard
```

# **SPrint: Self-Paced Continual Learning with Forgettable Samples**<br>
<img width="1269" alt="image" src="https://github.com/sperospera1225/SPrint/assets/67995592/5ffae4ed-7a24-450f-901b-f65f8e3b3275">

## Abstract
Continual learning(CL) addresses the challenge of learning new concepts progressively without forgetting previously acquired knowledge, a problem known as catastrophic forgetting. To tackle such challenge, we argue the significance of progressively incorporating samples from simple to complex into the training of new concepts, mirroring human learning strategies. We propose a method called **S**elf-**P**aced Continual Lea**r**n**in**g with Forge**t**table Samples (**SPrint**),  which performs back-propagation only on easy samples at each iteration. By measuring the forgetting events during training, we prioritize the inclusion of samples prone to forgetting in the episodic memory for future training sessions. We empirically demonstrate that SPrint outperforms state-of-the-art methods, despite its simplicity.

<!--
## Overview of the results of RM
The table is shown for last accuracy comparison in various datasets in Blurry10-Online.
If you want to see more details, see the [paper](https://arxiv.org/pdf/2103.17230.pdf).

| Methods   | MNIST      | CIFAR100   | ImageNet |
|-----------|------------|------------|----------|
| EWC       | 90.98±0.61 | 26.95±0.36 | 39.54    |
| Rwalk     | 90.69±0.62 | 32.31±0.78 | 35.26    |
| iCaRL     | 78.09±0.60 | 17.39±1.04 | 17.52    |
| GDumb     | 88.51±0.52 | 27.19±0.65 | 21.52    |
| BiC       | 77.75±1.27 | 13.01±0.24 | 37.20    |
| **RM w/o DA** | **92.65±0.33** | 34.09±1.41 | 37.96    |
| **RM**        | 91.80±0.69 | **41.35±0.95** | **50.11**    |

## Updates
- April 2nd, 2021: Initial upload only README
- April 16th, 2021: Upload all the codes for experiments 
- Jan 18th, 2022: Upload the notebooks to make blurry or disjoint dataset
-->

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
You can easily download the dataset following above format.

- MNIST: https://github.com/hwany-j/mnist_png
- CIFAR-10: https://github.com/hwany-j/cifar10_png
- CIFAR-100: https://github.com/hwany-j/cifar100_png

For ImageNet, you should download the public site.

- train: http://www.image-net.org/challenges/LSVRC/2012/nnoupb/ILSVRC2012_img_train.tar
- validation: http://www.image-net.org/challenges/LSVRC/2012/nnoupb/ILSVRC2012_img_val.tar

If you have custom datasets, you can make disjoint or blurry datasets of each task using `make_dataset_per_task.ipynb`. 

### Usage 
To run the experiments in the paper, you just run `experiment.sh`.
```angular2html
bash experiment.sh 
```
For various experiments, you should know the role of each argument. 

- `MODE`: CIL methods. Our method is called `sprint`. [joint, gdumb, icarl, rm, ewc, rwalk, bic, rm]
  (`joint` calculates accuracy when training all the datasets at once.)
- `MEM_MANAGE`: Memory management method. `default` uses the memory method which the paper originally used.
  [default, random, reservoir, uncertainty, prototype].
- `RND_SEED`: Random Seed Number 
- `DATASET`: Dataset name [mnist, cifar10, cifar100, imagenet]
- `STREAM`: The setting whether current task data can be seen iteratively or not. [online, offline] 
- `EXP`: Task setup [disjoint, blurry10, blurry30]
- `MEM_SIZE`: Memory size cifar10: k={200, 500, 1000}, mnist: k=500, cifar100: k=2,000, imagenet: k=20,000
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

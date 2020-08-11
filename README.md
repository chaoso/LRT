# AdaCorr

This is the code for the paper:

**<a> Error-Bounded Correction of Noisy Labels </a>**
<br>
Songzhu Zheng, Pengxiang Wu, Aman Goswami, Mayank Goswami, Dimitris Metaxas, Chao Chen
</br>
Presented at [ICML 2020](https://icml.cc/Conferences/2020)

If you find this code useful in your research please cite:
```
@inproceedings{jiang2018mentornet,
  title={Error-Bounded Correction of Noisy Labels},
  author={Songzhu Zheng, Pengxiang Wu, Aman Goswami, Mayank Goswami, Dimitris Metaxas, Chao Chen},
  booktitle={ICML},
  year={2020}
}
```

## Introduction 

AdaCorr is an algorithm that is designed to perform robustly when label noise is presented in your training data. This algorithm will try to correct mislabeled data points during training process relying on current network's confidence. 

Specifically, for each input data point
- (1) Likelihood ratio test (LRT) is performed to test the correctness of its current label. If the label is rejected by the test, the algorithm will set the new label to be the current MLE. 
- (2) Network will keep trainning using the new labels, which refines the power of the test

Steps (1) and (2) are conducted iteratively until the learning procedure converges.

## Environment Setting

The environment setup for AdaCorr is listed in environment.yml. To install, run:

```bash
conda env create -f environment.yml
source activate torch1.6
```

## Running AdaCorr 

There are several command-line flags that you can use to configure the input/output and hyperparameters to be applied by AdaCorr.

```bash
python LRTcorrect.py 
[--dataset] 
[--network]  
[--noise_type]
[--noise_level]
[--lr] 
[--n_epochs] 
[--epoch_start] 
[--epoch_update] 
[--epoch_interval] 
[--every_n_epoch] 
[--two_stage] 
[--gpu] 
[--n_gpus] 
[--seed]
```

- `--dataset : The dataset to be used in the experiment. Current version supports mnist/cifar10/cifar100/pc. The default is mnist.`
- `--network : The network architecture to be used as the backbone. Available options are cnn/resnet18/resnet34/preact_resnet18/preact_resnet34/preact_resnet101/pc. The default is preact_resnet34.`
- `--noise_type : Choose noise type to be applied to data's labels. Options are uniform/asymmetric.`
- `--noise_level : Set the noise level. Must be in the range [0, 1].`
- `--lr : Learning Rate. The default is 1e-3.`
- `--n_epochs : Number of epochs to train.`
- `--epoch_start : The epoch that retroactive loss is introduced.`
- `--epoch_update : The epoch that start to perform correction.`
- `--epoch_interval : Interval between the update of retroactive loss.`
- `--every_n_epoch : Sliding window for calculating network confidence.`
- `--two_stage : Use two stage training. Retrain the network from scratch using corrected labels. Default is 0. Two enable this feature set it to be 1.`
- `--gpu : The index of GPU to be used. The default is 0. If torch.cuda.is_available() is false the CPU will be used.`
- `--n_gpus : Number of GPUS to be used. The default is 1.`
- `--seed : Set the random seeds for your experiment.`

For example, to run AdaCorr on CIFAR10 with 20% uniform noisy level with $L_{ce}$ introduced at epoch 25 and correction starting at 30, you could run:
```bash
python LRTcorrect.py --dataset cifar10 --network preact_resnet34 --noise_type uniform --noise_level 0.2 --n_epochs 180 --epoch_start 25 --epoch_update 30
```


## Parameter Setting for Experiment Results

## Performance

## Algorithm

## Reference


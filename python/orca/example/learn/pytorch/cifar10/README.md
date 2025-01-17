# PyTorch Cifar10 example
We demonstrate how to easily run synchronous distributed PyTorch training using PyTorch Estimator of Project Orca in BigDL. We use a simple convolutional nueral network model to train on Cifar10 dataset, which is a dataset for image classification. See [here](https://pytorch.org/tutorials/beginner/blitz/cifar10_tutorial.html) for the original single-node version of this example provided by PyTorch. We provide three distributed PyTorch training backends for this example, namely "spark", "ray" and "bigdl".

## Prepare the environment

We recommend you to use Anaconda to prepare the environment, especially if you want to run on a yarn cluster:

```
conda create -n bigdl python=3.7  # "bigdl" is conda environment name, you can use any name you like.
conda activate bigdl
pip install torch
pip install torchvision
pip install matplotlib

# For spark backend
pip install bigdl-orca
pip install tqdm  # progress bar

# For ray backend
pip install bigdl-orca[ray]
pip install tqdm  # progress bar

# For bigdl backend
pip install bigdl-orca
pip install jep==3.9.0
pip install six cloudpickle
```

## Run on local after pip install

The default backend is `spark`.

```
python cifar10.py
```

You can run with `ray` backend via:

```
python cifar10.py --backend ray
```

You can run with `bigdl` backend via:

```
python cifar10.py --backend bigdl
```

## Run on yarn cluster for yarn-client mode after pip install

```
export HADOOP_CONF_DIR=the directory of the hadoop and yarn configurations
python cifar10.py --cluster_mode yarn-client
```

The default backend is `spark`. You can also run with `ray` or `bigdl` by specifying the backend.

## Results

**For "ray" and "spark" backend**

Final test results will be printed at the end:
```
num_samples : 10000
Accuracy : tensor(0.5378)
val_loss : 1.3078322240829467
```

**For "bigdl" backend**

You can find the logs for training as follows:
```
2020-12-03 15:25:30 INFO  DistriOptimizer$:426 - [Epoch 2 47680/50000][Iteration 24420][Wall Clock 497.634203315s] Trained 4 records in 0.022554577 seconds. Throughput is 177.3476 records/second. Loss is 0.82751834.
```

Final test results will be printed at the end:
```
Accuracy of the network on the test images: {'Top1Accuracy': 0.541100025177002}
```


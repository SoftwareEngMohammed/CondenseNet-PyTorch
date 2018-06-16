# CondenseNet-Pytorch

A pytorch implementation of [CondenseNet: An Efficient DenseNet using Learned Group Convolutions](https://arxiv.org/pdf/1711.09224.pdf)

### Project structure:
```
├── agents
|  └── condensenet.py # the main training agent for the dcgan
├── graphs
|  └── models
|  |  └── condensenet.py
|  |  └── denseblock.py
|  |  └── layers.py
|  └── losses
|  |  └── loss.py # contains the binary cross entropy 
├── datasets  # contains all dataloaders for the project
|  └── cifar10.py # dataloader for cifar10 dataset
├── data
|  └── cifar10  # contains raw dataset
├── utils # utilities folder containing metrics , config parsing, etc
|  └── assets
├── main.py
├── run.sh
```

### Data:
Dataloader is responsible for downloading (first time only) and preparing cifar10 data. 

### Model:
To be able to reproduce the results from the official implementation, we use the default model of cifar10 and its configs as given [here](https://github.com/ShichenLiu/CondenseNet)

| CondenseNet                | Feature map     |
| -------------------------- |:---------------:|
| 3x3 Conv (stride =1)       |     32x32       |
|![](./utils/assets/CodeCogsEqn1.png)|     32x32       |
| 2×2 average pool, stride 2 |     16x16       |
|![](./utils/assets/CodeCogsEqn2.png)|     16x16       |
| 2×2 average pool, stride 2 |      8x8        |
|![](./utils/assets/CodeCogsEqn3.png)|      8x8        |
| 8x8 global average pool    |      1x1        |
| 10-dim fully-connected     |                 |

### Experiment configs:
```
- Input size: 32x32x3
- Batch size: 64
- Learning rate: 0.1 following a consine type
- Optimizer: SGD
- Number of epochs: 300
- Condensation Stages: [14, 14, 14]
- Growth Rate: [8, 16, 32]
```
### Usage:
- To run the project, you need to add your configurations into the folder ```configs/``` as found here [here](https://github.com/hagerrady13/CondenseNet-Pytorch/blob/master/configs/condensenet_exp_0.json)
- ``` sh run.sh ```
- To run on a GPU, you need to enable cuda in the config file.

### Results:
| Metric       | Reproduced  | Official    |
| ------------ |:-----------:|:-----------:|
| Top1 error   |    4.78%    |             |
| Top5 error   |    0.15%    |             |

### Requirements:
- Pytorch: 0.4.0
- torchvision: 0.2.1
- tensorboardX: 1.2

### ToDo:
* Add network profiling for FLOPS counting
* Implement the condensation layers to optimize the model for inference

### References:
* CondenseNet official implementation in Pytorch: https://github.com/ShichenLiu/CondenseNet

### License:
This project is licensed under MIT License - see the LICENSE file for details.

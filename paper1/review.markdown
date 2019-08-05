---
pagetitle: DB-Net
title: "A Novel Deep Neural Network Architecture for Mars Visual Navigation"
author: "*Jiang Zhang, Yuanqing Xia, Ganghui Shen*"
output: html5_document
---

- There are two main methods for Mars visual navigation:
  - Blind: Navigation commands are pre-fed to rover by an engineer from the ground station.
  - AutoNav: Operates automously with human interference.

- AutoNav used algorithms like Dijkstra, A* or D* for finding path on a grid map.
- These are computationally heavy and memory comsuming algorithms which can easily explod as map size increases.
- Introduction of smarter and intellegent algorithms like neural networks, genetic algorithm, and swarm algorithms to solve Mars navigation problems efficiently.
- However pre-defined location of obstacles is required for these algorithms as well.
- Deploy DCNN for feature extraction from Mars visual images.
- Uses Imitation Learning which converts optimal policy finding problem to a supervised Learning problem.
- Replaces Value Information Module in VIN with Double Branch Architecture. Hence, *DB-Net*.

<center>

![](./img1.png "DB-Net")

</center>

- Branch one for extraction of global information whereas second branch extracts local feature Information.
- Performs better than VIN and gives an approx speed-up of 48% in training time compared to VIN.

<center>

|Architectures                 | DB-Net|  VIN  |
|:-----------------------------|:-----:|:-----:|
|Training accuracy             | 96.4% | 90.0% |
|Testing accuracy              | 95.6% | 89.8% |
|Training success rate         | 96.0% | 81.1% |
|Testing success rate          | 93.3% | 79.4% |
|Average time cost (each epoch)| 52.8s | 97.5s |

</center>

- Carried out model ablation experiment to check whether two-branch architecture and the residual convolutional layers are really necessary or not.
  - B1-Net: Removed branch one (Global feature extraction).
  - B2-Net: Replace residual convolutional layers of B1-Net with normal convolutional layers.
- Ablation experiment showed that both two-branch architecture and the residual convolutional layers are indespensible for best performance of DB-Net.

<center>

|28 x 28 grid map      |DB-Net|B1-Net|B2-Net|
|:---------------------|:----:|:----:|:----:|
|Training accuracy     |96.4% |86.2% |13.8% |
|Testing accuracy      |95.6% |85.8% |12.8% |
|Training success rate |96.0% |63.2% |1.1%  |
|Testing success rate  |93.3% |63.2% |1.3%  |

</center>

- Increase in accuracy and efficiency is also evident through the value function map of DB-Net and VIN.
- DB-Net correctly assigns high value (light colour) near target and low value (dark colour) near risky areas and looks similar to actual martian terrain. Whereas VIN's value function map fails to capture the risky areas.

<center>

![](./value_func.png "Value function")

</center>

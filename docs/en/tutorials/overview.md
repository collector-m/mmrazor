# Tutorial 1: Overview

MMRazor is an OpenMMLab model compression toolbox to help users slim their models, which includes 4 mainstream technologies: 1）Neural Architecture Search（NAS） 2）Pruning  3）Knowledge Distillation（KD）4）quantization（to do in next stage plan）

## Core Features

- Consistency: MMRazor's design and style are similar to OpenMMLab's, so MMRazor is friendly for the users of OpenMMLab's other codebases to slim their pre-trained models. You can even quickly apply our pruning and KD algorithms to your models without changing the model definition code.
- Flexibility: Several lightweight algorithms are loose coupling in MMRazor，which can be combined to use.
- Universality: It is loose coupling between lightweight algorithms and tasks. You can easily apply existing algorithms to new tasks.
- Scalability: MMRazor not only can support OpenMMLab, but also have the ability to support other framework based on PyTorch.

## Key Concepts

MMRazor consists of 4 main parts: 1) apis, 2) core, 3) models, 4) datasets. models is the most vital part, whose structure chart is as follows.

![overview](../imgs/tutorials/overview/overview.png)

- Algorithm: Specific implemented algorithm based on specific task, eg: SPOS (Single Path One-Shot Neural Architecture Search with Uniform Sampling) , applying one-shot NAS to classification. Algorithm consists of two main parts: architecture and algorithm components.
- Architecture: Model to be slimmed. There are different roles in different algorithm tasks, eg: architecture is supernet in NAS, also student net in KD, and float model in quantization.
- Algorithm components: Core functions providers of 4 lightweight algorithms. In each lightweight algorithm, there are serval classes to handle different types.
  - Mutator: Core functions provider of different types of NAS, mainly include some functions of changing the structure of architecture.
  - Pruner: Core functions provider of different types of pruning, mainly includes some functions of changing the structure of architecture and getting channel group.
  - Distiller: Core functions provider of different types of KD, mainly includes functions of  registering some forward hooks, calculate the kd-loss and so on.
  - Quantizer: Core functions provider of different types of quantization. It will come soon.
- Base components: Core components of architecture and some algorithm components
  - Op: Specific operation for building search space in NAS, eg: ShuffleBlock 3*3
  - Mutable: Searchable op for building searchable architecture in NAS. It mainly consists of op and mask,  and achieving searchable function by handling mask.
  - Loss: kd-loss for distiller.
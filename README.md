# ReMatching Dynamic Reconstruction Flow

**[Paper](https://arxiv.org/abs/2411.00705), [Project Page](https://research.nvidia.com/labs/toronto-ai/ReMatchingDynamicReconstructionFlow/)**

**ReMatching Dynamic Reconstruction Flow**<br>
Sara Oblak,
[Despoina Paschalidou](https://paschalidoud.github.io/),
[Sanja Fidler](https://www.cs.toronto.edu/~fidler/),
[Matan Atzmon](https://matanatz.github.io/)
<br>

Abstract: *Reconstructing dynamic scenes from image inputs is a fundamental computer
vision task with many downstream applications. Despite recent advancements, existing approaches still struggle to achieve high-quality reconstructions from unseen
viewpoints and timestamps. This work introduces the ReMatching framework,
designed to improve generalization quality by incorporating deformation priors into
dynamic reconstruction models. Our approach advocates for velocity-field-based
priors, for which we suggest a matching procedure that can seamlessly supplement
existing dynamic reconstruction pipelines. The framework is highly adaptable
and can be applied to various dynamic representations. Moreover, it supports
integrating multiple types of model priors and enables combining simpler ones to
create more complex classes. Our evaluations on popular benchmarks involving
both synthetic and real-world dynamic scenes demonstrate a clear improvement in
reconstruction accuracy of current state-of-the-art models.*




## Run our code

### Environment setup
This repository is based on [Deformable 3D Gaussians for High-Fidelity Monocular Dynamic Scene Reconstruction](https://github.com/ingra14m/Deformable-3D-Gaussians) code.

```bash
git clone https://github.com/nv-tlabs/ReMatching.git --recursive
cd ReMatching/code

conda create -n rematching python=3.7
conda activate rematching

pip install torch==1.13.1+cu116 torchvision==0.14.1+cu116 --extra-index-url https://download.pytorch.org/whl/cu116
pip install -r requirements.txt
```
### Datasets
We conducted our evaluation on [D-NeRF](https://www.albertpumarola.com/research/D-NeRF/index.html), [HyperNerf](https://hypernerf.github.io/) and [Dynamic Scenes](https://research.nvidia.com/publication/2020-06_novel-view-synthesis-dynamic-scenes-globally-coherent-depths) datasets.

### ReMatching setup
The following ReMatching framework hyperparameters can be set in *./rematching/arguments.conf*:

- ### general
  - rm_weight [ReMatching loss weight]
  - angle_weight [split used for the angle/speed evaluation of ReMatching loss]
- ### prior
  - name [selected prior, currently supporting the following options]
    - *rematching.rematching_loss.DiscreteReMatchingLoss_P1*
    - *rematching.rematching_loss.DiscreteReMatchingLoss_AdaptivePriors_P3*
    - *rematching.rematching_loss.DiscreteReMatchingLoss_AdaptivePriors_P4*
    - *rematching.rematching_loss.DiscreteReMatchingLoss_AdaptivePriors_P1_P3*
    - *rematching.rematching_loss.DiscreteReMatchingLoss_AdaptivePriors_P1_P4*
    - *rematching.rematching_loss.FunctionReMatchingLoss_Image_P3*
  - adaptive_prior
    - K [number of prior classes in adaptive prior]
    - t_multires [hyperparameter for W prediction]
    - W_hidden_dim [hyperparameter for W prediction]
    - entropy_weight [entropy loss weight for W prediction]
  - P1
    - V [selection of tensors as base for P1 prior]
  - P3
    - B [hyperparameter for P3 loss]
  - cam_time [camera selection for the image-level ReMatching loss]


### Training

```bash
python train.py -s path/to/your/dataset -m output/exp-name --eval --is_blender
```

## Contributing

Pull requests are welcome. For major changes, please open an issue first
to discuss what you would like to change.

## License
Copyright &copy; 2025, NVIDIA Corporation & affiliates. All rights reserved.
This work is made available under the [Nvidia Source Code License](LICENSE.txt).

## Acknowledgement

This repo is based on https://github.com/ingra14m/Deformable-3D-Gaussians.


## Citation
```
@article{
  oblak2024rematching,
  title={ReMatching Dynamic Reconstruction Flow},
  author={Oblak, Sara and Paschalidou, Despoina and Fidler, Sanja and Atzmon, Matan},
  journal={arXiv preprint arXiv:2411.00705},
  year={2024}
}
```

# Details on GBA implementation and vestibular schwannoma cross-modal segmentation pipeline

This repository summarizes implementation details related to the article "Cross-modal tumor segmentation using generative blending augmentation and self-training" 
by Guillaume Sallé, Gustavo Andrade-Miranda, Pierre-Henri Conze, Nicolas Boussion, Julien Bert, Dimitris Visvikis and Vincent Jaouen.

## Link to the Docker image
Our docker image is publicly available on Docker Hub through [this link](https://hub.docker.com/r/guillaumesallecrossmoda/latimcrossmoda2022chmod).
To download our docker image, you can use the following command :

```docker pull guillaumesallecrossmoda/latimcrossmoda2022chmod```

To use it, please refer to the [official guideline](https://crossmoda2022.grand-challenge.org/instructions-for-submission/) from CrossMoDA's organisers, 
section "Test your Docker container".

[CycleGAN](https://github.com/junyanz/pytorch-CycleGAN-and-pix2pix) and [nnU-Net](https://github.com/MIC-DKFZ/nnUNet) were trained using the official implementations without major change.

## GBA implementation details

GBA is based on [SinGAN's code](https://github.com/tamarott/SinGAN).

- We modified the functions `np2torch` from files `SinGAN/functions.py` and `SinGAN/imresize.py` in order to accept grayscale images correctly.
- We replaced line 55 from `harmonization.py` : ```out = (1-mask)*real+mask*out``` by ```out = (1-mask)*ref+mask*out```, allowing to harmonize any structures on the `ref` image and keep it as background.
- Please note that the argument `harmonization_start_scale` refers (in our paper) to `K-k*`.

The jupyter notebook `GBA.ipynb` describes the process in more details and gives an overview on how to apply GBA or its naive version on a set of images.

# Citation

Please cite this work using `@article{salle2023cross,
  title={Cross-modal tumor segmentation using generative blending augmentation and self training},
  author={Sall{\'e}, Guillaume and Conze, Pierre-Henri and Bert, Julien and Boussion, Nicolas and Visvikis, Dimitris and Jaouen, Vincent},
  journal={arXiv preprint arXiv:2304.01705},
  year={2023}
}
`.



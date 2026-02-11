# Psychophysically-Guided Training for Fingerprint Presentation Attack Detection

Official GitHub repository for the paper: Samuel Webster, Walter Scheirer, and Adam Czajka, "Psychophysically-Guided Training for Fingerprint Presentation Attack Detection,"  IEEE Transactions on Biometrics, Behavior, and Identity Science (T-BIOM) **([TechRxiv](https://www.techrxiv.org/users/1011473/articles/1371555-psychophysically-guided-training-for-fingerprint-presentation-attack-detection) | [IEEEXplore](https://ieeexplore.ieee.org/))**

![Paper teaser graphic](teaser.png)

We collected visual salient annotations and text descriptions, supporting decisions of humans detecting fake fingerprints, and used these features in psychophysically-guided model training paradigms to offer effective methods for fingerprint presentation attack detection.

## Table of contents
* [Abstract](#abstract)
* [Datasets](#datasets)
* [Model weights](#weights)
* [Citation](#citation)
* [Acknowledgment](#acknowledgment)

<a name="abstract"/></a>
## Abstract

Psychophysically-guided training, which directs model learning based on human-perceptual annotations, has demonstrated generalization improvements across various vision tasks, including biometric presentation attack detection (PAD). In saliency-guided training, model's decision-making is aligned to image regions marked by human annotators. In perceptually-weighted training, human psychophysical measurements weigh per-sample loss, prioritizing samples with greater 'difficulty'. This paper presents the first application of both strategies to fingerprint PAD. We conducted a 50-participant study to perceptually annotate 800 fingerprint samples, producing human-sourced saliency maps and annotation-duration-based perceptual weighting coefficients. These are utilized alongside algorithmically-generated "pseudosaliency" (minutiae-based, quality-based, and autoencoder-generated) and additional perceptual weighting coefficients derived from minutiae count and sample quality. Evaluating on the 2021 Fingerprint Liveness Detection Competition testing set, we explore various configurations within nine distinct training scenarios to assess the impact of psychophysically-guided training on accuracy and generalization. Our findings demonstrate the effectiveness of psychophysically-guided training for fingerprint PAD in both limited and large data contexts, and we present multiple configurations capable of earning the first place on the LivDet-2021 benchmark. Our results highlight psychophysically-guided training's promise for increased model generalization capabilities, its effectiveness when data is limited, and its potential to scale to larger datasets in fingerprint PAD. All collected saliency maps, perceptual weighting coefficient sets, and trained models are released with the paper to support reproducible research.

<a name="datasets"/></a>
## Datasets

### Human Fingerprint Annotation Dataset

In our acquisition of human-annotative saliency as well as annotation duration perceptual weights, we conducted a 50-participant fingerprint annotation collection. Participants annotated samples from the 2015, 2017, 2019, and 2021 editions of the LivDet-Fingerprint competition. Each participant hand-annotated 16 bonafide and 16 spoof samples, producing 800 doubly-annotated fingerprints. Additionally, individual annotation stroke times (mouse down/up) are recorded, participants predicted the liveness (bonafide/spoof) for each sample, and, participants could textually describe their annotated region. 

We offer human annotations with the paper. However, we are not allowed (according to the dataset sharing license) to re-release the official LivDet-Fingerprint competition datasets. To access original files, please follow instructions provided by the competition organizers at [LivDet datasets page](https://livdet.org/registration.php).

### Algorithmically-sourced Pseudosaliency and Perceptual Weights

Our saliency-guided training experiments use pseudosaliency produced via various algorithmic means: minutiae-based regions (Neurotechnology VeriFinger SDK), low-quality maps (NIST Biometric Image Software), and human-mimicking autoencoder annotations. Similarly, our perceptually-weighted training experiments use algorithmically-sourced perceptual weighting coefficient sets: minutiae count weighting coefficients (Neurotechnology VeriFinger SDK) and sample quality weighting coefficients (NIST Biometric Image Software). We offer these algorithmically-sourced pseudosaliency maps and perceptual weighting coeffecients with the paper.

### Obtaining Copies of the Datasets

Instructions on how to request a copy of the fingeprint annotation study data, saliency maps, and perceptual weighting coefficients used in this paper can be found at [the CVRL webpage](https://cvrl.nd.edu/projects/data/) (look for ND-FINGER-IJCB-2025 Dataset).

<a name="weights"/></a>
## Trained Fingerprint PAD models

Our trained fingerprint presentation attack detection (PAD) models explore nine training scenarios. These scenarios aim to present a variety of implementation environments that are dependent on data availability and choice of training style. 

The models are available in the following Box Folders:

1. [Training Scenarios 1-5 (Baseline, Saliency-Guided Training)](https://notredame.box.com/s/rvrvz8d5eeuldeeffv7f8z6jdi3jala4).
2. Training Scenarios 6-9 (Perceptually-Weighted Training, Combined Methods) [Link to be added once available]

### Box Contents

Models are divided into subdirectories that identify the scenario in which they were trained. Scenarios that explore saliency-guided or perceptually weighted training are further divided into subdirectories, following the format `{scenario}/{saliency type}/{saliency granularity/` or `{scenario}/{weighting coefficient set}`. All model weight filenames (`.pth` files) contain the necessary information to identify how they were trained respective to their training scenario.

#### Scenarios 1-5 (Box Folder #1)

- `s1-large-xent/`: Models are trained on a large data availability context using cross entropy loss only. Model filenames are formatted as `s1_{CNN architecture}_{# indep. run}.pth`.
- `s2-limited-xent/`: Models are trained on a limited data availability context using cross entropy loss only. Model filenames are formatted as `s2_{CNN architecture}_{# indep. run}.pth`.
- ` s3-limited-cyborg/`: Models are trained on a limited data availability context using loss-based saliency guidance and a variety of saliency types. Model filenames are formatted as `s3_{saliency type}-{saliency granularity}_{CNN architecture}_alpha-{alpha value}_{# indep. run}.pth`.
- `s4-limited-blurring/`: Models are trained on a limited data availability context using blur-based saliency guidance and a variety of saliency types. Model filenames are formatted as `s4_{saliency type}-{saliency granularity}_{CNN architecture}_{# indep. run}.pth`.
- `s5-large-cyborg/`: Models are trained on a large data availability context using loss-based saliency guidance and a variety of saliency types. Model filenames are formatted as `s5_{saliency type}-{saliency granularity}_{CNN architecture}_alpha-{alpha value}_{# indep. run}.pth`.

#### Scenarios 6-9 (Box Folder #2)

- `s6-limited-perceptual-weighting/`: Models are trained on a limited data availability context using the human-perceptual sample weighting strategy. Model filenames are formatted as `s6_{weighting coefficient set}-{low/high priority}_{CNN architecture}_{# indep. run}.pth`.
- `s7-large-perceptual-weighting/`:Models are trained on a large data availability context using the human-perceptual sample weighting strategy. Model filenames are formatted as `s7_{weighting coefficient set}-{low/high priority}_{CNN architecture}_{# indep. run}.pth`.
- `s8-limited-combined/`: Models are trained on a limited data availability context using combined implementations of saliency-guided and perceptually-weighted training. Model filenames are formatted as `s8_{saliency type}-{saliency granularity}_{weighting coefficient set}-{low/high priority}_alpha-{alpha value}_{combination strategy (ce/cyborg/both)}_{CNN architecture}_{# indep. run}.pth`.
- `s9-large-combined/`: Models are trained on a large data availability context using combined implementations of saliency-guided and perceptually-weighted training. Model filenames are formatted as `s9_{saliency type}-{saliency granularity}_{weighting coefficient set}-{low/high priority}_alpha-{alpha value}_{combination strategy (ce/cyborg/both)}_{CNN architecture}_{# indep. run}.pth`.

<a name="citation"/></a>
### Citation

<!-- If you find this work useful in your research, please cite the following paper: -->

Citation details will be added once available.


<a name="acknowledgment"/></a>
### Acknowledgment
This material is based upon work partially supported by the National Science Foundation under Grants No. 2237880 and No. 1942151. Any opinions, findings, and conclusions
or recommendations expressed in this material are those of the authors and do not necessarily reflect the views of the National Science Foundation.

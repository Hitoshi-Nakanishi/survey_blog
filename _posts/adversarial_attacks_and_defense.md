# Overview of Adversarial Attacks and Defences

- Adversarial Attacks and Defences: A Survey
(2018-09-28)
https://arxiv.org/pdf/1810.00069.pdf

- Deloitte analytics
https://www2.deloitte.com/jp/ja/pages/deloitte-analytics/articles/defending-against-adversarial-ai.html

- Adversarial Examples in Modern Machine Learning: A Review
https://arxiv.org/pdf/1911.05268.pdf


### The Attack Surface
1. Evasion Attack: adjusting malicious samples during testing phase
1. Poisoning Attack: contamination of the training data
1. Exploratory Attack: try to gsin as much knowledge as possible about the learning algorithm

Training Phase Capabilities
1. Data Injection
1. Data Modification
1. Logic Corruption

Testing Phase Capabilities
- White-Box attacks: adversary has total knowledge about the model used for classification. The attacker has information about the algorithm, their full parameters, and training data distribution.
- Black-Box attacks: no knowledge about the model. They can be further classified into the following categories
    1. Non-Adaptive Black-Box Attack
    1. Adaptive Black-Box Attack
    1. Strict Black-Box Attack

### Adversarial Goals
1. Confidence Reduction
1. Misclassification
1. Targeted Misclassification
1. Source / Target Misclassification


|||
|---|---|
| Exploratory Attacks | Model Inversion <br> Membership Inference attack <br> Model Extraction via APIs <br> Information Inference |
| Evasion Attacks | Adversarial Examples Generation <br> Generative Adversarial Networks (GAN) <br> GAN based attack in collaborative learning <br> Intrusion Detection Systems <br> Adversarial Classification |
| Poisoning Attacks | Support Vector Machine Poisoning <br> Poisoning on collaborative filtering systems <br> Anomaly Detection Systems |

## Adversarial Examples Generation
### Training Phase Modification
1. Label Manipulation
1. Input Manipulation
### Testing Phase Generation
#### White-Box Attacks

The framework is split into two phases a) direction sensitivity estimation and b) perturbation selection.
We can formalize the adversarial samples as the following optimization problem:

\begin{equation}
 X* = X + \arg\min{\|\delta X\|: F(X + \delta X) != F(X) }
\end{equation}

* Direction Sensitivity Estimation
    1. L-BFGS (制約付き最適化)
    1. Fast Gradient Sign Method (FGSM) (勾配ベースの最適化)
        1. Target Class Method
        1. Basic Iterative Method
    1. Jacobian Based Method

#### Black-Box Attacks
1. 決定境界面近似 -> Papernotらにより提唱されたSubstitute Black-Box Attack
1. 勾配近似 -> ZOO(Zeroth Order Optimization)
1. 進化アルゴリズム -> One Pixel Attack
1. 探査ベース -> NNA (Natural Adversarial Attack)

### Pertubation Selection
1. Perturb all the input dimensions
1. Perturb a selected input dimensions

### Adversarial Defense
1. Adversarial Training
1. Adversary Detector Network (ADN)

### Model Summary
* Adversarial Attacks
    * L-BFGS Attack 12/ Fast Gradient Sign Method / Basic Iterative Method / Iterative Least-Likely Class Method / R+FGSM / Adversarial Manipulation of Deep Representations / DeepFool / Jacobian-based Saliency Map Attacks / Substitute Blackbox Attack / Hot/Cold Attack / Carlini & Wagner Attacks / Universal Adversarial Perturbation / Data-Free UAP / VAE Attacks / Adversarial Transformation Networks / Dense Adversary Generation / Zeroth Order Optimization / One-Pixel Attack / Houdini / Momentum Iterative Fast Gradient Sign Method / AdvGAN / Boundary Attack / Natural Adversarial Attack / Spatially Transformed Adversarial Attack / Expectation Over Transformation / Backward Pass Differentiable Approximation / Simultaneous Perturbation Stochastic Approximation Attack / Decoupled Direction and Norm Attack / CAMOU
* Towards Real World Adversarial Attacks
    * Printed Adversarial Examples / Adversarial Eyeglasses / Adversarial Stop Signs / Adversarial 3D Printed Turtle / Adversarial Patch / ShapeShifter / Non-physical Adversaries in the Real World

* Defenses against Adversarial Attacks
    * Increasing Robustness of Machine Learning Models / Adversarial Training / Deep Contractive Network / Defensive Distillation / MagNet / PGD Adversarial Training / Ensemble Adversarial Training / Random Resizing and Padding as a Defense / Stochastic Activation Pruning / Total Variance Minimization and Quilting Thermometer Encoding / PixelDefend / Defense-GAN / WRM: A Distributionally Robust Optimization with Adversarial Training / High-Level Representation Guided Denoiser / Adversarial Logit Pairing / Fortified Networks / Feature Denoising Block / Analysis by Synthesis / Web-Scale Nearest-Neighbor Search / ME-Net /Detecting Adversarial Attacks / Early Methods: PCA, Softmax, and Reconstruction of Adversarial Images / Adversary Detector Networks / Kernel Density and Bayesian Uncertainty Estimates / Feature Squeezing / Reverse Cross-Entropy

### Related works
**ZOO** Chen, Pin-Yu, et al. "Zoo: Zeroth order optimization based black-box attacks to deep neural networks without training substitute models." Proceedings of the 10th ACM Workshop on Artificial Intelligence and Security. 2017.

**One Pixel Attack** Su, J., D. V. Vargas, and K. Sakurai. "One pixel attack for fooling deep neural networks. CoRR abs/1710.08864 (2017)."

**Natural Adversarial Attack** Zhao, Zhengli, Dheeru Dua, and Sameer Singh. "Generating natural adversarial examples." arXiv preprint arXiv:1710.11342 (2017).

**Adversary Detector Network (ADN)** Metzen, Jan Hendrik, et al. "On detecting adversarial perturbations." arXiv preprint arXiv:1702.04267 (2017).


# 「敵対的摂動 (Adversarial Perturbation) に対するモデルの頑健性の測り方」
Sansan's blog
* https://buildersbox.corp-sansan.com/entry/2019/06/28/110000
* https://buildersbox.corp-sansan.com/entry/2019/07/29/110000#f-1652c336

## TL;DR
学習されたDNNがAdversarial Perturbation に対してどのくらい頑健であるかを測定する。
## 測定アプローチ
1. Attack Based Approach - モデルへの強い敵対的攻撃アルゴリズムを設計して、敵対的摂動が与えられたものと、元のものとの間のずれを測定する方法
1. Verification Based Approach (CLR と CLEVER) - 攻撃方法に関わらない、モデルが受ける最小の影響やその下界を見つけることを目的


## Related works
1. Cross-Lipschitz Regularization を用いる手法
1. CLEVER (Cross Lipschitz Extreme Value for Network Robustness)
1. POPQORN (Propagated Output Quantified Robustness for RNNs)


### CLEVER
#### Contributions
1. 攻撃方法に依存せず頑健性の評価が可能.
1. 任意の NN 系 のモデルに応用が可能.
1. 強い理論保証あり.
1. 大きなネットワークであっても, 計算が可能.
#### Discussion
RNN 系のモデルに対する頑健性の評価をできない -> 発展的なモデルへ


# Towards Robust Detection of Adversarial Examples
NIPS 2018 |
## TL;DR
Reverse cross-entropy (RCE) を提案、DNNがよりadversarial examples を区別するような潜在表現を学習するように encourage する。
## Contributions
## Keypoints
## How evaluated?
## Discussion
## Related works

---

# Manifold Regularization for Adversarial Robustness
2020-03-09 | https://github.com/charlesjin/adversarial_regularization

## TL;DR
Manifold regularization を使った adversarial defence. adversarial example を使わないため標準の adversarial training よりも高速。PGD adversary に対して、CIFAR-10 で 70% の robust accuracy で SoTA

## Contributions

## Keypoints

## How evaluated?
200-step PGD adversary in CIFAR-10

## Discussion
論文として微妙だった。コードも実装されていない。

## Related works
**Project Gradient Descent (PGD) defence** - Aleksander Madry, Aleksandar Makelov, Ludwig Schmidt, Dimitris Tsipras, and Adrian Vladu. Towards deep learning models resistant to adversarial attacks, 2017
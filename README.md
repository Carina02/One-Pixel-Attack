# One pixel attack for fooling deep neural networks

Official repository for the paper: One pixel attack for fooling deep neural networks 

<p align="center">
    <a href="https://arxiv.org/abs/1710.08864/">Paper link</a> 
</p>

## Introduction

The repository includes a code example for one(n) pixel attack and some additional comments. For the code, note that the attack target is not CNN but a pretrained vision transformer. Both targeted and non-targeted attacks are included.


## Some additional comments about the paper

The original motivation of this work is to propose a general-purpose methodology for testing the robustness of image encoders. The one-pixel attack presented in the paper should be understood as merely a special case of this broader framework.

This general methodology is designed to evaluate a given image encoder (for example, the encoder component of a transformer-based model) by examining its robustness against artificially constructed, small-magnitude perturbations to the input image. These perturbations may be identified using differential evolution or other optimization methods, and can take the form of extremely sparse modifications, such as altering a single pixel. The key characteristic of this approach is that it treats the image model as a black box, focusing exclusively on the relationship between inputs and outputs without relying on any assumptions about the model’s internal structure. As a result, this method is equally applicable to CNNs, ViTs, and any future image encoder architectures.

Why we focus on a single pixel in particular? Primarily because it is interesting to modify just one pixel and observere how model performs under such extremely limited attack. When the one-pixel attack was originally proposed, mainstream CNNs predominantly operated on relatively small images, such as 32×32 CIFAR images or 224×224 ImageNet images. In contrast, for modern Vision Transformers, a single-pixel perturbation is clearly insufficient to pose a serious challenge. This naturally leads to new questions: How many pixels are required to fool contemporary ViTs or even multimodal foundation models? More generally, how much perturbation—in terms of both the number of modified pixels and the magnitude of their changes—can a state-of-the-art image encoder tolerate before it is taken by the attack?

Reframed this way, the minimum number of pixels and minimum perturbation magnitude required for a successful attack can serve as a universal quantitative measure of model robustness.

To build intuition, consider a more mature visual system, such as the human visual system. When faced with a one-pixel or few-pixel perturbation that is either too sparse or too subtle to affect human perception, a human observer’s judgment should remain identical to that for the unperturbed image. If, however, the perturbation is sufficient to obscure or distort critical visual details, the human response would likely be more nuanced: the image appears to depict a certain object, but some specific details are occluded or corrupted, preventing confident recognition.

Such a graded and uncertainty-aware response was fundamentally unattainable for CNN-based systems due to architectural limitations. However, the emergence of MAE-style models and multimodal architectures has made this type of output possible. This suggests that, beyond raw performance gains attributable to the transformer architecture itself, transformers have also brought substantial improvements in robustness and representational flexibility. In fact, with appropriate prompting, such nuanced responses can already be realized in practice, representing a qualitative shift rather than a mere quantitative improvement. Future work can therefore focus primarily on refining precision and reliability. But at the same time, the introduction of additional modalities inevitably expands the attack surface, creating new potential vulnerabilities.

Finally, regarding differential evolution: for small-scale images such as those in CIFAR or ImageNet, DE can be an efficient method for searching adversarial pixel locations and perturbation values. However, for the high-resolution images commonly processed by modern large multimodal models, applying DE to one-pixel or even few-pixel attacks becomes analogous to searching for a needle in a haystack. The combinatorial explosion of the discrete search space requires prohibitively large population sizes and iteration counts for convergence, rendering such attacks primarily of demonstrative rather than practical significance in these settings.

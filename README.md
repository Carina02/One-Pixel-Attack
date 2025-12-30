# One pixel attack for fooling deep neural networks

Official repository for the paper: One pixel attack for fooling deep neural networks 

<p align="center">
    <a href="https://arxiv.org/abs/1710.08864/">Paper link</a> 
</p>

## Introduction

The repository includes a code example for one(n) pixel attack and some additional comments.


## Some additional comments about the paper

The original motivation of this work is to propose a general-purpose methodology for testing the robustness of image encoders. The one-pixel attack presented in the paper should be understood as merely a special case of this broader framework.

This general methodology is designed to evaluate a given image encoder (for example, the encoder component of a transformer-based model) by examining its robustness against artificially constructed, small-magnitude perturbations to the input image. These perturbations may be identified using differential evolution or other optimization methods, and can take the form of extremely sparse modifications, such as altering a single pixel. The key characteristic of this approach is that it treats the image model as a black box, focusing exclusively on the relationship between inputs and outputs without relying on any assumptions about the model’s internal structure. As a result, this method is equally applicable to CNNs, ViTs, and any future image encoder architectures.

Why we focus on a single pixel in particular? Primarily because it is interesting to modify just one pixel and observere how model performs under such extremely limited attack. When the one-pixel attack was originally proposed, mainstream CNNs predominantly operated on relatively small images, such as 32×32 CIFAR images or 224×224 ImageNet images. In contrast, for modern Vision Transformers, a single-pixel perturbation is clearly insufficient to pose a serious challenge. This naturally leads to new questions: How many pixels are required to fool contemporary ViTs or even multimodal foundation models? More generally, how much perturbation—in terms of both the number of modified pixels and the magnitude of their changes—can a state-of-the-art image encoder tolerate before it is taken by the attack?

Reframed this way, the minimum number of pixels and minimum perturbation magnitude required for a successful attack can serve as a universal quantitative measure of model robustness.

To build intuition, consider a more mature visual system, such as the human visual system. When faced with a one-pixel or few-pixel perturbation that is either too sparse or too subtle to affect human perception, a human observer’s judgment should remain identical to that for the unperturbed image. If, however, the perturbation is sufficient to obscure or distort critical visual details, the human response would likely be more nuanced: the image appears to depict a certain object, but some specific details are occluded or corrupted, preventing confident recognition.

Such a graded and uncertainty-aware response was fundamentally unattainable for CNN-based systems due to architectural limitations. However, the emergence of MAE-style models and multimodal architectures has made this type of output possible. This suggests that, beyond raw performance gains attributable to the transformer architecture itself, transformers have also brought substantial improvements in robustness and representational flexibility. In fact, with appropriate prompting, such nuanced responses can already be realized in practice, representing a qualitative shift rather than a mere quantitative improvement. Future work can therefore focus primarily on refining precision and reliability. But at the same time, the introduction of additional modalities inevitably expands the attack surface, creating new potential vulnerabilities.

Finally, regarding differential evolution: for small-scale images such as those in CIFAR or ImageNet, DE can be an efficient method for searching adversarial pixel locations and perturbation values. However, for the high-resolution images commonly processed by modern large multimodal models, applying DE to one-pixel or even few-pixel attacks becomes analogous to searching for a needle in a haystack. The combinatorial explosion of the discrete search space requires prohibitively large population sizes and iteration counts for convergence, rendering such attacks primarily of demonstrative rather than practical significance in these settings.

## 中文版追记
本文的初衷亦在提出一种用于测试图像encoder的泛用方法。论文中的一像素攻击只是这个方法的一个特例。
这个泛用的方法是用于测试某一个图像encoder(比如transformer的encoder部分)，对于图像中一个人为设置(比如使用differential evolution法找到的，也可以是使用其他最优化方法)的微小扰动(比如一个像素的修改)的鲁棒性测试。这种测试将图像模型作为一个黑箱，只关注模型的输入和输出而不深究它的具体结构，所以此方法可以用于测试CNN，或者VIT，或者未来的其他任何的图像encoder。

为什么是一个像素？因为有趣: 只修改一个像素是一种极限条件。此攻击被提出时，主流的CNN主要处理32像素的cifar图像和224像素的imagenet图像。但是一像素对于目前的vit来说显然是不够看了，那么就又引出了新的问题。如果要fool目前的vit甚至多模态大模型，需要多少像素。或者说一个目前最SOTA的图像处理器能忍受最多多少像素的攻击?换句话说，最低限度的攻击所需要的像素的个数和改变值的大小可以成为衡量模型鲁棒性的一个普遍方法。

想象一个较为完善的视觉系统，比如人类的视觉系统，会如何应对一像素或者少数像素攻击。在这些被攻击的像素因为数量过少或者修改的程度不够而完全不足以影响人眼的判断时，人给出的判断结果应该跟完全没有被攻击过的图片一致。如果被攻击的像素足以混淆或掩盖图片上的一些重要细节以至于严重影响处理判断时，人类给出的反馈会是，这张图片看起来像是某个东西，但是某些(具体的)细节被遮盖，我无法确认。

这种输出结果在CNN时代因为CNN构造的问题是无法做到的。但是后来的MAE和多模态模型使得这种输出成为可能。这说明抛开transformer架构本身带来的纯粹性能提升，transformer在提高图像处理的鲁棒性上也取得了重大进展。甚至于，通过提供合适的prompts，上述的完美回答已经是可以被实现的了-这实现了质的提升，而今后的工作就可以专注于量(精度)的提升了。但是同时，更多模态的导入意味着更多可能的漏洞和攻击手段。

关于differential evolution。在cifar和imagenet这种小尺寸图片上，DE可以比较效率地用来搜索用于攻击的像素和修改值。但是对于目前LLM处理的大尺寸图片，使用DE进行one-pixel-attack甚至few pixel attack，在如此庞大的离散空间中寻找那几个能让模型误判的“关键像素”，就像在大海捞针，DE 算法需要极大的种群规模和迭代次数才能收敛，使得这种攻击方式变得只有示范意义。


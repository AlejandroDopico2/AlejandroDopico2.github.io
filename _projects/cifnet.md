---
layout: page
title: CIFNet
description: Making AI Learning Smarter and More Efficient
img: assets/img/projects/cifnet/Abstract.drawio-1.png
importance: 1
category: research
related_publications: true
---

Imagine you train an **Artificial Intelligence (AI)** to recognize cats. Later, you want to teach it to recognize dogs. The problem is that, when learning about dogs, it might "forget" what it knew about cats! This is called **"catastrophic forgetting."** It's a huge challenge, especially when the AI needs to run on devices with limited resources, like a mobile phone or a Raspberry Pi.

Many current solutions for this problem are powerful, but they also consume a lot of resources and take a long time to train.

This is where **CIFNet (Class Incremental and Frugal Network)** comes in. This project is a new way to teach AI incrementally, but in a **super efficient and sustainable way**. CIFNet is a big step towards making continuous learning in AI more practical and accessible for everyone, especially when we already have very well-trained "AI brains" (or powerful pre-trained models) available.

---

### 🧠 Why It Matters

The real world is constantly changing. New data keeps popping up: new animal species, new fashion trends... Just like humans learn new things without forgetting old ones, AI systems need to evolve without losing their past knowledge.

Imagine if every time there was a new category of data, your AI had to **relearn _everything_ from scratch**. That would be very inefficient! Think about the memory you'd need, data privacy concerns, and, most importantly, the massive computational cost and energy consumption. This is especially critical for small devices or in energy-sensitive environments.

Our goal behind CIFNet was to create an adaptive and sustainable AI system that could:

- **Efficiently** learn new categories of information.
- Maintain its **good performance** on what it had already learned.
- **Minimize computational overhead** and energy consumption.

CIFNet tackles this problem head-on, finding the perfect balance between adapting AI to new information and being incredibly efficient, especially when we can leverage strong pre-trained knowledge bases.

---

### 💡 How It Works

CIFNet lies in combining three key components that work together for a super-efficient, **single-step learning process**:

- **Frozen Pre-trained Feature Extractor (Fθ)**: Instead of re-training the entire AI "brain" (the neural network backbone) every time, CIFNet uses a powerful, already-trained feature extractor that stays fixed. This is a game-changer! It shifts the heavy lifting from expensive backbone fine-tuning to much more efficient classification based on high-quality, pre-processed data.
- **ROLANN Classifier Layer (Gϕ)**: This is our clever classification layer. Unlike typical AI training that requires many repetitive updates over several "epochs," ROLANN learns in a **single, direct step**. It simply expands its architecture by adding new output "neurons" for each new class it learns. This drastically cuts down training time.
- **Compressed Data Buffer (B)**: This smart buffer stores highly compact "feature representations" (like a distilled version of the original data) instead of raw images. This means a huge reduction in memory needed (e.g., 75x less memory than raw ImageNet images). It's crucial for preventing the AI from favoring the newest information by exposing it to distilled memories of past classes, ensuring everything stays balanced. To handle imbalances, we use a clever "temporal oversampling" trick.

<div class="row justify-content-sm-center">
  <div class="col-sm-8 mt-3 mt-md-0">
    {% include figure.liquid path="assets/img/projects/cifnet/Model.drawio-1.png" title="CIFNet architecture" class="img-fluid rounded z-depth-1" %}
  </div>
</div>
<div class="caption">
CIFNet architecture: How our system learns new things without forgetting the old.
</div>

---

### 🛠️ Under the Hood

My main contribution was designing and testing this new approach to make Class-Incremental Learning incredibly efficient in terms of computation and energy.

Key technical highlights include:

- **Single-Step Optimization**: This is possible thanks to the combo of the fixed AI backbone and the ROLANN classifier. It allows CIFNet to learn new classes efficiently without needing many repeated updates.
- **Memory Efficiency**: The compressed data buffer dramatically reduces memory use, making the method scalable and perfect for devices with limited resources.
- **Catastrophic Forgetting Mitigation**: CIFNet effectively prevents the AI from forgetting old information at the classification stage, keeping accuracy high on previously learned tasks. The expansion buffer makes sure all the new knowledge is properly integrated with the old.

---

### 🎉 Final Thoughts

CIFNet not only performs competitively on standard benchmarks (like CIFAR-100 and ImageNet-100), but it also brings **order-of-magnitude improvements** in training time, energy consumption, and estimated carbon emissions compared to other advanced methods that re-train their entire AI backbones. This work is a significant step towards making advanced AI learning more accessible and sustainable for real-world applications.

**Wondering if it can be applied to some scenario?** CIFNet is designed in the context of the **PILLAR Robots project**! Here, the goal is for a robot to **progressively learn new objects bit by bit** without consuming many resources. Imagine a robot learning to recognize a new toy every week, without forgetting the old ones, and without needing a supercomputer by its side – that's the kind of practical, efficient AI we're building!

<div class="row justify-content-sm-center">
  <div class="col-sm-8 mt-3 mt-md-0">
    {% include figure.liquid path="assets/img/projects/cifnet/comparison_curves_cifar-100-1.png" title="CIFAR-100 Performance" class="img-fluid rounded z-depth-1" %}
  </div>
</div>

<div class="row justify-content-sm-center">
  <div class="col-sm-8 mt-3 mt-md-0">
    {% include figure.liquid path="assets/img/projects/cifnet/comparison_curves_imagenet-100-1.png" title="ImageNet-100 Performance" class="img-fluid rounded z-depth-1" %}
  </div>
</div>

<div class="row justify-content-sm-center">
  <div class="col-sm-8 mt-3 mt-md-0">
    {% include figure.liquid path="assets/img/projects/cifnet/sustainability_metrics.png" title="Comparative Sustainability Metrics" class="img-fluid rounded z-depth-1" %}
  </div>
</div>
<div class="caption">
CIFNet's Impact on Sustainability: These graphs clearly demonstrate how CIFNet (shown in yellow) dramatically reduces training time, carbon emissions (kg CO₂-eq), and energy consumption (kWh) compared to other state-of-the-art incremental learning methods. This highlights CIFNet's role in making AI learning not just faster, but also significantly more environmentally friendly.
</div>

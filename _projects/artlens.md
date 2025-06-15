---
layout: page
title: ArtLens
description: HackUDC 2025 Edition
img: assets/img/projects/artlens/icon.jpeg
importance: 1
category: hackathons
related_publications: true
---

Have you ever visited a museum and, without a guide, felt a little lost—standing in front of incredible works of art, but not really knowing what you're looking at?

That was the motivation behind **ArtLens**, a mobile app we built during **[HackUDC 2025](https://hackudc.gpul.org/)** to bring context, story, and voice to any museum visit. With just your phone, ArtLens can recognize a painting (or sculpture), describe it in detail, adapt it to your profile, and even read it aloud.

<div class="row justify-content-sm-center">
  <div class="col-sm-8 mt-3 mt-md-0">
    {% include figure.liquid path="assets/img/projects/artlens/team.jpg" title="ArtLens team" class="img-fluid rounded z-depth-1" %}
  </div>
</div>
<div class="caption">
ArtLens was developed in 36 hours and won the "Best Mobile App" prize sponsored by NomaSystems.
</div>

---

### 🧠 Motivation

Museums are full of stories—but if you’re not an art historian or don’t have a guided tour, those stories often stay hidden. We wanted to change that, using AI to create a more **inclusive and personalized museum experience**.

ArtLens tries to answer the questions many of us have when visiting a museum:

> **What am I looking at?**  
> **Why is this artwork important?**  
> **What’s the story behind it?**

---

### 📱 How it works

The app has three simple screens that guide the whole experience:

<div class="row">
  <div class="col-sm mt-3 mt-md-0">
    {% include figure.liquid path="assets/img/projects/artlens/home.jpeg" title="1. Choose your profile" class="img-fluid rounded z-depth-1" %}
  </div>
  <div class="col-sm mt-3 mt-md-0">
    {% include figure.liquid path="assets/img/projects/artlens/scan.jpeg" title="2. Take a photo of the artwork" class="img-fluid rounded z-depth-1" %}
  </div>
  <div class="col-sm mt-3 mt-md-0">
    {% include figure.liquid path="assets/img/projects/artlens/result.jpeg" title="3. Get your audio description" class="img-fluid rounded z-depth-1" %}
  </div>
</div>
<div class="caption">
<strong>The app flow:</strong><br>
① <em>Home</em> – Choose your visitor profile (e.g., child, tourist, art student...)<br>
② <em>Scan</em> – Take a photo of an artwork directly in the museum<br>
③ <em>Result</em> – Get a personalized description, read out loud, with a link to explore more
</div>

---

### 🛠️ Under the hood

I worked on the **backend and the AI system**, and this project was full of firsts for me:

- ✅ First time using **CLIP** (by OpenAI) for visual understanding
- ✅ First time working with **Milvus**, an embedding database for fast similarity search
- ✅ First time building **real-time text-to-speech**, using the super simple `gTTS` library

To ensure privacy and keep things lightweight, we also ran a **local LLM** (LLaMA 3.2 via **Ollama**) on-device. That way, the entire process could run offline—an important feature in a place like a museum.

---

### 🔄 Full pipeline

Here’s how the system worked end-to-end:

1. The visitor selects a profile (e.g., child, tourist…)
2. Takes a photo of the artwork
3. We extract image **embeddings** using **CLIP**
4. We search those embeddings in a **Milvus** database of artworks (focused on Museo del Prado)
5. Once we identify the artwork, we generate a **prompt** for the local **LLM**, tailored to the visitor's profile
6. The LLM creates a natural, friendly explanation of the piece
7. We convert that text into **speech** using `gTTS`, providing an instant, personalized audio guide

---

### 🖼️ Custom dataset from Museo del Prado

One big challenge was the lack of existing datasets for the **Museo del Prado**—especially in Spanish. So we built our own:  
scraping, curating, and annotating a **small dataset of iconic artworks**. It was a great exercise in data wrangling and making AI more culturally grounded.

<div class="row justify-content-sm-center">
  <div class="col-sm-8 mt-3 mt-md-0">
    {% include figure.liquid path="assets/img/projects/artlens/garden.jpg" title="The Garden of Earthly Delights" class="img-fluid rounded z-depth-1" %}
  </div>
  <div class="col-sm-4 mt-3 mt-md-0">
    {% include figure.liquid path="assets/img/projects/artlens/meninas.jpg" title="Las Meninas" class="img-fluid rounded z-depth-1" %}
  </div>
</div>
<div class="caption">
We focused on the Prado Museum in Madrid, but the same system could be adapted to any collection.
</div>

---

### 🎉 Final thoughts

We built ArtLens in just 36 hours during the **HackUDC 2025** hackathon.  
We didn’t sleep much, but we learned a lot—and somehow, it all worked.

Winning the **Best Mobile App** award (thanks to **NomaSystems**) was the cherry on top.  
But more than that, we were proud to create something that used AI not for automation or speed, but for **curiosity** and **cultural connection**.

Because sometimes, all you need is one simple question to unlock a masterpiece:

> **“Tell me what I’m looking at.”**

---
title: 'Alejandro Dopico | Frugal AI Researcher'
date: 2025-03-28
type: landing

design:
  background:
    color: '#f8f9fa'
    image:
      # Add your image background to `assets/media/`.
      filename: bg-hue.svg

sections:
  - block: resume-biography
    content:
      username: admin
    design:
      biography:
        style: 'text-align: justify; font-size: 0.9em;'
  - block: features
    content:
      title: My Research Pillars
      items:
      - name: Federated Learning
        description: "Building AI models that learn across decentralized devices while ensuring privacy and efficiency."
        icon: server
      - name: Continuous Learning
        description: "Enabling AI systems to adapt and evolve over time without requiring full retraining."
        icon: infinity
      - name: Frugal AI
        description: "Optimizing AI for low-resource environments, making it more accessible and sustainable."
        icon: leaf
    design:
      columns: '3'
      spacing: 
        padding: ['20px', '0', '20px', '0']
      align: center
  - block: markdown
    content:
      title: Latest Work
      text: |
        **CIFNet**: Class-Incremental Frugal Network.  
        Submitted to [ECML PKDD 2025](https://ecmlpkdd.org/2025/) (Under Review).  
        📂 GitHub: [CIFNet](https://github.com/AlejandroDopico2/CIFNet)
  - block: cta-button-list
    content:
      title: Get in Touch
      buttons:
        - text: Connect on LinkedIn
          icon: brands/linkedin
          url: https://www.linkedin.com/in/alejandro-dopico-castro-063845239/
        - text: Explore CIFNet (GitHub)
          icon: brands/github
          url: https://github.com/AlejandroDopico2/CIFNet
        - text: Email Me
          icon: at-symbol
          url: mailto:your-email@udc.es
    design:
      align: center

  - block: markdown
    content:
      title: Hackathon Achievements
      text: |
        🏆 **HackUDC 2024 NomaSystem's Challenge Winner**  
        **[ArtLens](https://devpost.com/software/artlens)**: AI-powered museum guide. Built a vision-based mobile app to identify artworks and provide real-time descriptions.
      design:
        align: justify
    design:
      align: justify
      background:
        color: 'rgba(0, 0, 0, 0.03)'  # Light gray background for contrast
---

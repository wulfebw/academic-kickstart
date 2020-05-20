---
# Documentation: https://sourcethemes.com/academic/docs/managing-content/

title: "Language Modeling with Recurrent Generative Adversarial Networks"
summary: <a href="https://arxiv.org/abs/1406.2661" class="md-link">GANs</a> have had a lot of success in generating images; can they be applied with similar effect to natural language? Since natural language is discrete, we formulate this task as a reinforcement learning problem, and use REINFORCE to train a recurrent generative network to maximize rewards produced by a discriminating network. We found this approach did not scale well to the vocab sizes used in realistic datasets (> 60,000 words), but believe improved training methods (e.g., <a href="https://arxiv.org/abs/1502.05477" class="md-link">TRPO</a>) and curriculum learning (e.g., <a href="https://arxiv.org/abs/1511.06732" class="md-link">MIXER</a>) might overcome these issues.
authors: []
tags: []
categories: []
date: 2016-05-19

# Optional external URL for project (replaces project detail page).
external_link: ""

# Featured image
# To use, add an image named `featured.jpg/png` to your page's folder.
# Focal points: Smart, Center, TopLeft, Top, TopRight, Left, Right, BottomLeft, Bottom, BottomRight.
image:
  caption: ""
  focal_point: ""
  preview_only: false

# Custom links (optional).
#   Uncomment and edit lines below to show custom links.
# links:
# - name: Follow
#   url: https://twitter.com
#   icon_pack: fab
#   icon: twitter

url_code: "https://github.com/wulfebw/adversarial_rl"
url_pdf: "files/cs224d_final_paper.pdf"
url_slides: ""
url_video: ""

# Slides (optional).
#   Associate this project with Markdown slides.
#   Simply enter your slide deck's filename without extension.
#   E.g. `slides = "example-slides"` references `content/slides/example-slides.md`.
#   Otherwise, set `slides = ""`.
slides: ""
---

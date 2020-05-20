---
# Documentation: https://sourcethemes.com/academic/docs/managing-content/

title: "Playing Atari with Hierarchical Deep Reinforcement Learning"
summary: How can artificial agents autonomously learn increasingly complex behavior? The <a href="http://people.idsia.ch/~juergen/subgoals.html" class="md-link">traditional</a> <a href="https://people.cs.umass.edu/~mahadeva/papers/hrl.pdf" class="md-link">approach</a> to solving this problem is to identify subgoals, and then to learn options (i.e., skills) useful for achieving those subgoals. In this research, we instead take a bottom-up approach to HRL, wherein the sequential, primitive actions of an agent are modeled as the result of latent variables, which may themselves be used as options (similar in concept to the approach taken <a href="http://www.ausy.tu-darmstadt.de/uploads/Site/EditPublication/Daniel2016JMLR.pdf" class="md-link">here</a>). This research makes an initial step in this direction, using hierarchical recurrent neural networks within a <a href="https://arxiv.org/abs/1507.06527" class="md-link">Recurrent Q-Network</a>.
authors: []
tags: []
categories: []
date: 2017-05-19

# Optional external URL for project (replaces project detail page).
external_link: ""

# Featured image
# To use, add an image named `featured.jpg/png` to your page's folder.
# Focal points: Smart, Center, TopLeft, Top, TopRight, Left, Right, BottomLeft, Bottom, BottomRight.
image:
  caption: ""
  focal_point: ""
  preview_only: true

# Custom links (optional).
#   Uncomment and edit lines below to show custom links.
# links:
# - name: Follow
#   url: https://twitter.com
#   icon_pack: fab
#   icon: twitter

url_code: "https://github.com/wulfebw/hierarchical_rl"
url_pdf: "files/cs239_final_paper.pdf"
url_slides: ""
url_video: ""

# Slides (optional).
#   Associate this project with Markdown slides.
#   Simply enter your slide deck's filename without extension.
#   E.g. `slides = "example-slides"` references `content/slides/example-slides.md`.
#   Otherwise, set `slides = ""`.
slides: ""
---

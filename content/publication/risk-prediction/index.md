---
# Documentation: https://sourcethemes.com/academic/docs/managing-content/

title: "Intermediate-Horizon Automotive Risk Prediction"
authors: [Blake Wulfe, Sunil Chintakindi, Sou-Cheng T. Choi, Rory Hartong-Redden, Anuradha Kodali, Mykel J. Kochenderfer]
date: 2018-02-05
doi: ""

# Schedule page publish date (NOT publication's date).
publishDate: 2020-05-19T22:05:06-07:00

# Publication type.
# Legend: 0 = Uncategorized; 1 = Conference paper; 2 = Journal article;
# 3 = Preprint / Working Paper; 4 = Report; 5 = Book; 6 = Book section;
# 7 = Thesis; 8 = Patent
publication_types: ["1"]

# Publication name and optional abbreviated publication name.
publication: "Autonomous Agents and Multi-Agent Systems"
publication_short: "AAMAS"

abstract: "Advanced collision avoidance and driver hand-off systems can benefit from the ability to accurately predict, in real time, the probability a vehicle will be involved in a collision within an intermediate horizon of 10 to 20 seconds. The rarity of collisions in real-world data poses a significant challenge to developing this capability because, as we demonstrate empirically, intermediate-horizon risk prediction depends heavily on high-dimensional driver behavioral features. As a result, a large amount of data is required to fit an effective predictive model. In this paper, we assess whether simulated data can help alleviate this issue. Focusing on highway driving, we present a three-step approach for generating data and fitting a predictive model capable of real-time prediction. First, high-risk automotive scenes are generated using importance sampling on a learned Bayesian network scene model. Second, collision risk is estimated through Monte Carlo simulation. Third, a neural network domain adaptation model is trained on real and simulated data to address discrepancies between the two domains. Experiments indicate that simulated data can mitigate issues resulting from collision rarity, thereby improving risk prediction in real-world data."

# Summary. An optional shortened abstract.
summary: "This research considers the problem of predicting whether a car will suffer a collision in the time period 10-20 seconds in the future. We formulate this task as policy evaluation in a MDP with a high-dimensional, continuous state space, and a reward function dominated by rare events (collisions). We then demonstrate that simulated data and domain adaptation models can be used to improve prediction performance on real-world data."

tags: []
categories: [policy evaluation, mdp, risk prediction, autonomous driving]
featured: false

# Custom links (optional).
#   Uncomment and edit lines below to show custom links.
# links:
# - name: Follow
#   url: https://twitter.com
#   icon_pack: fab
#   icon: twitter

url_pdf: https://arxiv.org/abs/1802.01532
url_code: https://github.com/wulfebw/risk_prediction
url_dataset:
url_poster:
url_project:
url_slides:
url_source:
url_video:

# Featured image
# To use, add an image named `featured.jpg/png` to your page's folder. 
# Focal points: Smart, Center, TopLeft, Top, TopRight, Left, Right, BottomLeft, Bottom, BottomRight.
image:
  caption: ""
  focal_point: ""
  preview_only: false

# Associated Projects (optional).
#   Associate this publication with one or more of your projects.
#   Simply enter your project's folder or file name without extension.
#   E.g. `internal-project` references `content/project/internal-project/index.md`.
#   Otherwise, set `projects: []`.
projects: []

# Slides (optional).
#   Associate this publication with Markdown slides.
#   Simply enter your slide deck's filename without extension.
#   E.g. `slides: "example"` references `content/slides/example/index.md`.
#   Otherwise, set `slides: ""`.
slides: ""
---

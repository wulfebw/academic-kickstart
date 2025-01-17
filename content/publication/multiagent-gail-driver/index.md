---
# Documentation: https://sourcethemes.com/academic/docs/managing-content/

title: "Multi-Agent Imitation Learning for Driving Simulation"
authors: [Raunak P. Bhattacharyya, Derek J. Phillips, Blake Wulfe, Jeremy Morton, Alex Kuefler, Mykel J. Kochenderfer]
date: 2018-03-02
doi: ""

# Schedule page publish date (NOT publication's date).
publishDate: 2020-05-19T22:14:02-07:00

# Publication type.
# Legend: 0 = Uncategorized; 1 = Conference paper; 2 = Journal article;
# 3 = Preprint / Working Paper; 4 = Report; 5 = Book; 6 = Book section;
# 7 = Thesis; 8 = Patent
publication_types: ["1"]

# Publication name and optional abbreviated publication name.
publication: "International Conference on Intelligent Robots and Systems"
publication_short: "IROS 2018"

abstract: "Simulation is an appealing option for validating the safety of autonomous vehicles. Generative Adversarial Imitation Learning (GAIL) has recently been shown to learn representative human driver models. These human driver models were learned through training in single-agent environments, but they have difficulty in generalizing to multi-agent driving scenarios. We argue these difficulties arise because observations at training and test time are sampled from different distributions. This difference makes such models unsuitable for the simulation of driving scenes, where multiple agents must interact realistically over long time horizons. We extend GAIL to address these shortcomings through a parameter-sharing approach grounded in curriculum learning. Compared with single-agent GAIL policies, policies generated by our PS-GAIL method prove superior at interacting stably in a multi-agent setting and capturing the emergent behavior of human drivers."

# Summary. An optional shortened abstract.
summary: "One potential method for validating autonomous vehicles is to evaluate them in a simulator. For this to work, you need highly realistic models of human driving behavior. Existing research learned human driver models using generative adversarial imitation learning, but did so in a single-agent environment. As a result, the model fails when you execute many of the learned policies simultaneously. This research performs training in a multi-agent setting to address this problem."

tags: []
categories: [rl, imitation learning]
featured: false

# Custom links (optional).
#   Uncomment and edit lines below to show custom links.
# links:
# - name: Follow
#   url: https://twitter.com
#   icon_pack: fab
#   icon: twitter

url_pdf: https://arxiv.org/abs/1803.01044
url_code: https://github.com/sisl/ngsim_env
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

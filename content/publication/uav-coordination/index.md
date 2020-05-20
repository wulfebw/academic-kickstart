---
# Documentation: https://sourcethemes.com/academic/docs/managing-content/

title: "Collision Avoidance for Unmanned Aircraft Using Coordination Tables"
authors: [Rachael E Tompa, Blake Wulfe, Michael P Owen, Mykel J Kochenderfer]
date: 2016-09-25
doi: ""

# Schedule page publish date (NOT publication's date).
publishDate: 2020-05-19T22:29:31-07:00

# Publication type.
# Legend: 0 = Uncategorized; 1 = Conference paper; 2 = Journal article;
# 3 = Preprint / Working Paper; 4 = Report; 5 = Book; 6 = Book section;
# 7 = Thesis; 8 = Patent
publication_types: ["1"]

# Publication name and optional abbreviated publication name.
publication: "Digital Avionics Systems"
publication_short: "DASC"

abstract: "The safe integration of unmanned aircraft into the airspace requires reliable systems to keep aircraft separated. Unmanned aircraft will likely have to use horizontal maneuvers, in contrast with manned aircraft collision avoidance systems, which use only vertical maneuvers. Coordination of horizontal maneuvers is much less straightforward than vertical maneuvers because in some situations it is better for both aircraft to maneuver in the same direction and in other situations it is better to maneuver in opposite directions. This paper uses dynamic programming to generate a coordination scheme that is represented as a lookup table. Different aircraft that may have different collision avoidance systems can use this table to produce complementary maneuvers. The robustness of the table to various policies is measured in terms of safety and efficiency. The empirical results suggest that a coordination table can improve safety for encounters involving different collision avoidance systems."

# Summary. An optional shortened abstract.
summary: "How can UAVs with different collision avoidance strategies coordinate maneuvers so as to minimize collisions? This research presents an approach that enforces reasonable requirements on the behavior of UAVs, and as a result dramatically improves safety in dangerous encounters. The method is essentially to ensure that UAV maneuvers align with the directions of those advised by an optimal joint solution."

tags: []
categories: [planning]
featured: false

# Custom links (optional).
#   Uncomment and edit lines below to show custom links.
# links:
# - name: Follow
#   url: https://twitter.com
#   icon_pack: fab
#   icon: twitter

url_pdf: https://ieeexplore.ieee.org/abstract/document/7777958
url_code: https://github.com/sisl/HorizontalCoordUAVs
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

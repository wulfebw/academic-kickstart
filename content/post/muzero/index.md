---
# Documentation: https://sourcethemes.com/academic/docs/managing-content/

title: "MuZero"
subtitle: ""
summary: "Why should MuZero perform better than other DRL algorithms?"
authors: []
tags: []
categories: [rl, muzero]
date: 2019-12-09
lastmod: 2019-12-09
featured: false
draft: false

# Featured image
# To use, add an image named `featured.jpg/png` to your page's folder.
# Focal points: Smart, Center, TopLeft, Top, TopRight, Left, Right, BottomLeft, Bottom, BottomRight.
image:
  caption: ""
  focal_point: ""
  preview_only: false

# Projects (optional).
#   Associate this post with one or more of your projects.
#   Simply enter your project's folder or file name without extension.
#   E.g. `projects = ["internal-project"]` references `content/project/deep-learning/index.md`.
#   Otherwise, set `projects = []`.
projects: []
---

# Context
- [MuZero paper.](https://arxiv.org/pdf/1911.08265.pdf)
- [Tabular implementation.](https://github.com/wulfebw/muzero)
    + See that link for code description and some experiments.

# Question
- Why should MuZero be better than other deep RL algorithms (in particular DQN)?
- The paper, ["When to use parametric models in reinforcement learning?"](https://arxiv.org/pdf/1906.05243.pdf), goes into this question but with an emphasis on a [different](https://arxiv.org/pdf/1903.00374.pdf) model-based algorithm
    + They define planning in an unusual manner as using "more computation without additional data to improve predictions and behavior"
        * The "usual" definition being the use of a (learned) transition and reward model to compute a value function or policy
    + The reasons they give for why parameteric model-based planning might outperform non-parameteric (experience replay) planning are not that clear to me, but may include:
        1. Inductive bias of the parameteric model (improving generalization)
        2. Improved exploration through use of the model
        3. Improved credit assignment ("backward planning")
- To answer the question, I think the reason MuZero might outperfom DQN is the second reason: that it exhibits better exploration
    + This isn't the typical kind of improved exploration through model use that you get with e.g., [R-max](https://ie.technion.ac.il/~moshet/brafman02a.pdf).
    + Instead, because the learned value function is approximate, if the learned model is "good enough", then you can use additional computation to select better actions in the environment than you would if you behaved greedily with respect to the value function itself.
        * Where "additional computation" means running MCTS.
        * This means that the actions you take will, on average, be better.
        * Which intuitively should mean that you'll learn about the optimal policy and its value function more quickly.
            - And reach different parts of the state space that have higher value.
        * Which can be viewed as improved exploration.
    + This works for the definition of "better" as "more sample efficient"
        * But that additional computation takes more resources and time, so if you defined "better" as the algorithm that provides the best solution given some amount of time, DQN might outperform MuZero.

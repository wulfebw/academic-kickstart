---
# Documentation: https://sourcethemes.com/academic/docs/managing-content/

title: "Super Smash Bros. 64 AI: Behavioral Cloning"
subtitle: ""
summary: "Writeup on Super Smash Bros. 64 AI developed using behavioral cloning."
authors: []
tags: []
categories: [imitation learning, ssb64]
date: 2019-07-13
lastmod: 2019-07-13
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

# Summary
1. **Goal**: develop a Super Smash Bros. 64 AI that acts based on image input
2. **Approach**: start with behavioral cloning since it's simple
3. **Dataset**: Images and action sequences, and training and validation splits available [here](https://s3.console.aws.amazon.com/s3/buckets/ssb64-data-public/) ([s3 bucket](https://docs.aws.amazon.com/AmazonS3/latest/dev/RequesterPaysBuckets.html))
4. **Model and Training**: Convolutional and recurrent neural networks, implemented in pytorch, code available [here](https://github.com/wulfebw/ssb64bc)
5. **Deployment**: Through [gym-mupen64plus](https://github.com/mupen64plus)
6. **Evaluation**: Quantitative gameplay performance (damage, kills, lives lost)
7. **Demo**: See the description of the video for some interesting events
<iframe width="560" height="315" src="https://www.youtube.com/embed/Usr00SPbRHg" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

<!-- markdown-toc start - Don't edit this section. Run M-x markdown-toc-refresh-toc -->
**Table of Contents**

- [Summary](#summary)
- [Motivation](#motivation)
- [Related work](#related-work)
- [Dataset](#dataset)
- [Approach](#approach)
- [Experiments and Results](#experiments-and-results)
- [Conclusion and Future Work](#conclusion-and-future-work)
- [Appendix 1: Dataset collection](#appendix-1-dataset-collection)
- [Appendix 2: Imitation Learning](#appendix-2-imitation-learning)
- [Appendix 3: Model and training details](#appendix-3-model-and-training-details)
- [Appendix 4: N64 as an RL environment](#appendix-4-n64-as-an-rl-environment)
- [Appendix 5: RNNs why use them, how to optimize and regularize them](#appendix-5-rnns-why-use-them-how-to-optimize-and-regularize-them)

<!-- markdown-toc end -->

# Motivation
Build a Super Smash Bros. 64 (SSB64) AI agent to play against.

# Related work

## N64 and SSB64 AI
The only info on an SSB64 AI I could find online was this cs231n [project](http://cs231n.stanford.edu/reports/2016/pdfs/113_Report.pdf) with associated [videos](https://www.youtube.com/watch?v=c-6XcmM-MSk). It's a nice write up and was helpful in doing this project.

I thought implementing a similar project myself would be worth doing nevertheless because:
1. They don't provide access to any data or code
2. Their agent seems to behave a bit repetitively
3. I was curious whether a different action-space or model would work better
4. As stated, I wanted to play a better AI myself

[TensorKart](https://github.com/kevinhughes27/TensorKart) is a project that developed a Mario Kart 64 AI. That project (and associated blog [post](https://www.kevinhughes.ca/blog/tensor-kart)) was also helpful, and provided the technical approach roughly followed in this project.

## Game AI in general
There's a ton of work on game playing. Most of it focuses on reinforcement learning (RL). This is because RL / approximate dynamic programming is currently the best approach to the problem. See for example [OpenAI five](https://openai.com/five/) or Deepmind [starcraft II AI ](https://deepmind.com/blog/alphastar-mastering-real-time-strategy-game-starcraft-ii/) or [AlphaGo](https://deepmind.com/research/alphago/). RL is the best approach in these game playing scenarios because (among other reasons):
1. It's possible to collect a large amount of training data through simulation.
2. The training and testing distributions closely or exactly match.
3. The agent can benefit from [competitive self play](https://openai.com/blog/competitive-self-play/).
4. There's an easily accessible reward function (e.g., win/lose, damage, deaths) that aligns well with the true goal (developing a competitive agent).


# Dataset
The dataset consists of a set of matches. See [Appendix 1](#appendix-1-dataset-collection) for details. Main points:
1. [mupen64plus](https://mupen64plus.org/) was used for emulating the N64.
2. The dataset consists of a set of gameplay matches.
   - In total about 175,000 frames representing about 6 hours of gameplay.
3. Matches were played between blue DK and the highest level game AI Kirby.
   - This allows the network to identify which agent it controls.
   - Extending this to multiple characters would require e.g., adding a feature indicating the controlled character.
4. All matches were played on the dreamland stage.
5. Items were included to make it more interesting.

Here's a short clip selected from the dataset to give a sense for the behavior being imitated:
<iframe width="560" height="315" src="https://www.youtube.com/embed/K4bJlsvCliw" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

# Approach
I started with behavioral cloning (BC), which is supervised learning using a dataset of expert demonstrations, despite it being a worse-performing approach than RL because:
1. It's simpler to implement than RL methods.
   - Allows for becoming familiar with the emulator in a simplified setting.
2. It provides a nice baseline for comparison.
3. It has more predictable computational costs than RL.

The main disadvantages of behavioral cloning are:
1. It may take a lot of data to achieve good performance (see [Appendix 2](#appendix-2-imitation-learning)).
2. The resulting agent will not perform significantly better than the expert providing the data.
- It might perform slightly better due to decreased reaction time, but that's not particularly interesting or fun to play against.

## Observation space
- A requirement for this project was that the AI has to act on image observations.
  - There are some alternatives to this observation space (e.g., operating on the game [RAM](https://deepsense.ai/playing-atari-on-ram-with-deep-q-learning/)).
- A single image is not a Markovian representation of the state.
  - It's unclear to what extent multiple images would improve performance.
  - For this reason, different numbers of frames were considered as input (fixed history in the CNN case, and complete history in theory in the RNN case).

## Action space
I considered two action spaces:
1. Exclusive multiclass action space consisting of common SSB64 moves.
- This is what the cs231n project uses.
- The actions include  the buttons, the axes, and smash combinations (A + left, A + right, etc).

2. A multi-discrete action space with a value for each joystick axis, and one value for the button.
- This action space seemed like it should allow for more efficient learning.

## Models
1. A Resnet-9, multi-frame model.
- Using a four-frame history of grayscale images.

2. An RNN with Resnet feature extractor.
- This takes as input individual grayscale images at each timestep.
- Same visual feature extractor as the fixed-length history model.

The models were implemented in pytorch. See [Appendix 3](#appendix-3-model-and-training-details) for training details.

# Experiments and Results
- Edit (05/18/2020): I never ran this evaluation because gym-mupen64plus had a number of issues with it
  - See the appendix 4 for more details

### Deployment
The models were deployed using [gym-mupen64plus](https://github.com/bzier/gym-mupen64plus).

# Conclusion and Future Work
Despite not being the best approach to the problem, behavioral cloning was a helpful place to start in creating a SSB64 AI. I learned a fair amount about emulating the game (see [Appendix 4](#appendix-4-n64-as-an-rl-environment)), [pytorch ignite](https://github.com/pytorch/ignite) (see [training script](https://github.com/wulfebw/ssb64bc/blob/master/scripts/train.py)), regularizing RNNs (see [Appendix 5](#appendix-5-rnns-why-use-them-how-to-optimize-and-regularize-them)).

<br />
The main direction for future work is applying RL to the problem. As discussed in [Appendix 4](#appendix-4-n64-as-an-rl-environment), the N64 isn't the most convenient environment for RL for technical reasons, so most of the effort in applying RL would be in creating a convenient environment.

# Appendix 1: Dataset collection
- Images were collected by adapting the TensorKart codebase
  - See this script
- I collected the data on a mac. The [Inputs](https://github.com/zeth/inputs) python package used in TensorKart doesn't work on mac for joysticks, so I made some changes to the input plugin for mupen64plus to accept a command line argument for a filepath at which to store the actions received. See [here](https://github.com/wulfebw/mupen64plus-input-sdl) for the fork containing those changes.
- Image-action pairs were created by finding, for each image, the non-null action that occurred most recently following the collected image, up to a maximum of 0.05 seconds after the image, or if no non-null action occurred, a noop action was selected.

# Appendix 2: Imitation Learning
- Some <a href="/assets/imitation_learning_notes.pdf">notes</a> on the topic.

# Appendix 3: Model and training details
- See <a href="https://github.com/wulfebw/ssb64bc/blob/master/scripts/hparams.py">here</a> for the hyperparams used in the CNN case.

# Appendix 4: N64 as an RL environment
- mupen64plus seems to be the most popular N64 emulator.
- It is not designed for use in RL.
  - The design is based on a core module that has plugins for video, audio, controller input, etc.
  - The plugins don't communicate directly.
  - Providing a unified interface for RL would require a significant amount of effort, with the implementation options being:
    1. Wrap the core and all plugins in an adapter program.
      - And also interpret / provide access to the RAM.
    2. Use [BizHawk](http://tasvideos.org/BizHawk.html)
      - Bizhawk seems to have already [done](https://github.com/TASVideos/BizHawk/tree/master/libmupen64plus) option 1, and is typically used in tool-assisted SSB64 gameplay.
      - It only seems to work on windows for now, with linux support being [developed](https://github.com/TASVideos/BizHawk/issues/1430).
- Alternatively, you could use [gym-mupen64plus](https://github.com/bzier/gym-mupen64plus)
  - It takes screenshots of the game and parses them to compute rewards.
  - The main problems are:
    1. Because the observations are from screenshots, the hardware might influence the rate of observations and their alignment with actions taken.
       - This is complicated to deal with, as can be seen in the dataset [formatting details](https://github.com/wulfebw/ssb64bc/tree/master/ssb64bc/formatting) of this project.
    2. gym-mupen64plus for SSB64 attempts to automatically select characters in versus mode, but that didn't work in my case.
       - The implementation assumes the selector for the AI appears in the same location every time.
         - In my emulation of the game it was random.
       - Directly performing these tasks by operating on the RAM is clearly a better approach.
    3. Parsing the screen for the reward seems to work, but breaks with small changes.
       - Using the RAM directly would be faster and more reliable.

# Appendix 5: RNNs why use them, how to optimize and regularize them
## Why use an RNN?
- I tried using an RNN because I was curious to what extent it would improve performance.
  - The reasons it might improve performance are:
    1. A reasonable-size, fixed-frame history may not represent a Markovian representation of the environment.
    2. The inductive bias of the RNN may provide some benefits (e.g., consistency or smoothness).

## Optimizing and regularizing RNNs
- First, note that RNNs have gone out of fashion lately (at least in NLP).
  - [Transformer networks](https://arxiv.org/pdf/1706.03762.pdf) are generally being preferred.
  - [Here's](https://openreview.net/pdf?id=Hygxb2CqKm) a paper that tries to explain why.
- There are a lot of tricks for regularizing and optimizing RNNs.
  - This is a good [paper](https://arxiv.org/pdf/1708.02182.pdf) on it that is somewhat recent.
    - It focuses on NLP, but the advice seemed to help in my case.
  - I implemented or copied some of the regularization methods [here](https://github.com/wulfebw/ssb64bc/blob/master/ssb64bc/models/torch_utils.py).
- One decision to make in RNN training is whether to use "stateful" or "stateless" training.
  - See this [description](https://keras.io/examples/lstm_stateful/) and this [explanation](http://philipperemy.github.io/keras-stateful-lstm/).
    - The gist is that you need to use stateful (maintaining the hidden state across batches) training if you want the network to learn to maintain memory beyond the length of the BPTT.

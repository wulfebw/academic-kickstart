---
# Documentation: https://sourcethemes.com/academic/docs/managing-content/

title: "DQN Tips"
subtitle: ""
summary: "Tips and heuristics for training Deep Q-Networks"
authors: []
tags: []
categories: [rl, dqn]
date: 2017-04-15
lastmod: 2018-02-09
featured: false
draft: false

# Featured image
# To use, add an image named `featured.jpg/png` to your page's folder.
# Focal points: Smart, Center, TopLeft, Top, TopRight, Left, Right, BottomLeft, Bottom, BottomRight.
image:
  caption: "The Q-function in a UAV MDP, which is where I learned the tips/heuristics in this post"
  focal_point: ""
  preview_only: false

# Projects (optional).
#   Associate this post with one or more of your projects.
#   Simply enter your project's folder or file name without extension.
#   E.g. `projects = ["internal-project"]` references `content/project/deep-learning/index.md`.
#   Otherwise, set `projects = []`.
projects: []
---
- update: see [rainbow](https://arxiv.org/abs/1710.02298)
- sanity check the implementation
    + come up with a simple dataset and see if the DQN can correctly learn values for it 
    + an example is a contextual bandit problem where you have two possible states, and two actions, where one action is +1 and the other -1 
    + generally, an rl method should work on 1-step and 2-step mdps both with and without random rewards and transitions
- updating the target network 
    + check freeze rate
    + this should be between every 100 updates and every 40000
- batch size
    + this can be hard to set and depends on CPU vs GPU as well as the state dimensionality
    + start with 32 and increase
    + the goal should be to have each experience replayed some number of times on average
        * this is determined by the size of the replay memory and batch size
- replay memory 
    + replay memory size 1,000 to 10,000,000
- action selection
    + softmax vs e-greedy
        * softmax typically works better if the temperature is tuned well
- learning rate
    + try values between 0.01 and 0.00001 generally
- state sampling
    + only relevant when initial-state distribution can be controlled
    + if the important rewards are common then uniform sampling of the initial state might work
    + if the important reward is rare then you'll need to oversample these states
        * to do this in a principled manner, you need to know the relative probability of sampling states in the original MDP versus the proposal MDP (i.e., you need to do importance sampling)
    + prioritized sampling can also help if you are dealing with rare, significant rewards
- normalizing input
    + mean center and normalize 
    + to get the stats, if it's stationary, run it for 100,000 samples and compute mean and std dev 
    + or if the range of the input is available then you can use that 
        * subtract the average of the end points 
        * divide by half the total range
- max episode length
    + when ending an episode _not_ at a terminal state, be careful not to label that as a terminal state
    + this value will impact the distribution over the state space
- terminal states
    + you need to handle this so that the target value is zero if it's terminal
- discount 
    + < 1 unless finite horizon in which case <= 1
- initializing the network weights
    + this is consistently surprisingly important 
    + see http://cs231n.github.io/neural-networks-2/ (Weight Initialization)
- action space
    + if this is large then it can make learning slow
    + if this really should be continuous, then consider policy gradient methods
- regularization / dropout
    + many papers don't report using regularization or dropout
    + empirically it can help in certain situations
        * for example when the training MDP is different from the testing MDP and you need the policy to generalize
        * start with small values for l2 reg (0.00001)
        * dropout can vary dramatically in effectiveness (dropout ratio of 0.01 to 0.5)
- network hyperparams
    + number of layers
        - start small (2) and increase as needed
    + number of units
        - start small (32) and increase as needed
    + nonlinearity
        - start with relu or tanh 
        - maxout, elu, etc for getting extra benefit
        - common pitfall: applying a nonlinearity to the last output of the network 
            * this should just be a affine layer (dot(x,W) + b)
            * in the relu case, applying it to the last layer makes all the output positive, which will break it
- optimizer
    + start with adam or rmsprop 
    + then check out (http://cs231n.github.io/neural-networks-3/)
- rewards   
    + you can clip them between -1 and +1, but you lose a lot of information
    + if you have to use certain reward values larger than that, it can help to normalize them to be between -1 and +1
    + if you have control over the rewards, then consider using reward shaping
    + if the rewards are too large, then you can end up with e.g., relus dying
- dqn variations 
    + double dqn works a lot better, particularly if the rewards are negative
        * this is particularly easy to implement, so it's generally worth a shot
        * (https://arxiv.org/abs/1509.06461)
    + dueling network can be better
        * (https://arxiv.org/abs/1509.06461)
- replay memory variations
    + prioritized replay 
        * oversamples certain experiences based on td-error and uses importance sampling in the loss to maintain unbiased state distribution
        * helps a lot with sparse rewards
        * (https://arxiv.org/abs/1511.05952)

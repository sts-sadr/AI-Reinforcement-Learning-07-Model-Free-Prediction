# AI-Reinforcement-Learning-07-Model-Free-Prediction
Lecture 4: Model-Free Prediction by David Silver

Website: http://www0.cs.ucl.ac.uk/staff/D.Silver/web/Teaching.html

Videos: https://www.bilibili.com/video/av32149008/?p=4

- Monte-Carlo Reinforcement Learning
  - MC methods learn directly from episodes of experience
  - MC is model-free:
    - no knowledge of MDP transitions / rewards
  - MC learns from complete episodes:
    - no bootstrapping
  - MC uses the simplest possible idea:  value = mean return
  - Caveat:  can only apply MC to episodic MDPs
    - All episodes must terminate
  - Catalogue
    - First-Visit Monte-Carlo Policy Evaluatio
    - Every-Visit Monte-Carlo Policy Evaluatio
  - Incremental Monte-Carlo Updates
    - Update V(s) incrementally after episode
    - For each state St with return Gt
      - N(St) = N(St) + 1
      - V(St) = V(St) + 1 / N(St) * (Gt - V(St)
    - In non-stationary problems, it can be useful to track a running mean, i.e.  forget old episodes
      - (St) = V(St) + α (Gt − V(St))
      
- Temporal-Difference Learning
  - TD methods learn directly from episodes of experience
  - TD is model-free:  no knowledge of MDP transitions / rewards
  - TD learns from incomplete episodes, by bootstrapping 
  - TD updates a guess towards a guess
  - TD(0)
    - Update value V(St) toward estimated return
      - V(St) = α ( Rt+1 + γ * V(St+1) - V(St))
  - TD(λ)
    - The λ-return Gλt combines all n-step returns G(n)
    - Using weight (1 − λ)λ^(n−1)
  - Forward-view TD(λ)
    - Update value function towards the λ-return
    - Forward-view looks into the future to compute Gλt
    - Like MC, can only be computed from complete episode
  - Backward View TD(λ)
    - Update online, every step, from incomplete sequences
    - Keep an eligibility trace for every state s
    - Update value V(s) for every state s
    - In proportion to TD-error δt and eligibility trace
    
<img src="https://github.com/ChenBohan/AI-Reinforcement-Learning-07-Model-Free-Prediction/blob/master/readme_img/%CE%BB-return.png" width = "70%" height = "70%" div align=center />

<img src="https://github.com/ChenBohan/AI-Reinforcement-Learning-07-Model-Free-Prediction/blob/master/readme_img/Forward-view%20TD(%CE%BB).png" width = "70%" height = "70%" div align=center />

<img src="https://github.com/ChenBohan/AI-Reinforcement-Learning-07-Model-Free-Prediction/blob/master/readme_img/Eligibility%20Traces.png" width = "70%" height = "70%" div align=center />

<img src="https://github.com/ChenBohan/AI-Reinforcement-Learning-07-Model-Free-Prediction/blob/master/readme_img/Backward%20View%20TD(%CE%BB).png" width = "70%" height = "70%" div align=center />
    
- Advantages and Disadvantages of MC vs. TD
  - TD can learn before knowing the final outcome
    - TD can learn online after every step
    - MC must wait until end of episode before return is known
  - TD can learn without the final outcome
    - TD can learn from incomplete sequences
    - MC can only learn from complete sequences
    - TD works in continuing (non-terminating) environments
    - MC only works for episodic (terminating) environments
  - MC has high variance, zero bias
    - Good convergence properties
    - (even with function approximation)
    - Not very sensitive to initial value
    - Very simple to understand and use
  - TD has low variance, some bias
    - Usually more efficient than MC
    - TD(0) converges to vπ(s)
    - (but not always with function approximation)
    - More sensitive to initial value
    
- Bias/Variance Trade-Off 
  - Return Gt is unbiased estimate of vπ(St)
  - True TD target Rt+1 + γ * V(St+1) is unbiased estimate of vπ(St)
  - TD target is biased estimate of vπ(St)
  - TD target is much lower variance than the return:
    - Return depends on many random actions, transitions, rewards
    - TD target depends on one random action, transition, reward
    
- Bootstrapping: update involves an estimat
  - MC does not bootstrap
  - DP bootstraps
  - TD bootstraps
- Sampling:  update samples an expectation
  - MC samples
  - DP does not sample
  - TD samples
  
  

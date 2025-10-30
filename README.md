```
Recommendation System: A/B Test System Design (Business Scope)
Recommendation System: A/B Test System Design (Business Scope)
Feb 2024 - Feb 2024Feb 2024 - Feb 2024
1. Metrics: Primary, Secondary, and Guardrails
• Primary metric is the single main outcome used to judge success. It must be attributable, sensitive, and stable.
• Examples: daily engagement rate per user, average time spent, 7-day retention.
• Secondary metrics support understanding, explain why results changed, or uncover side effects.
• Examples: share rate, cold-start content views, creator diversity.
• Guardrail metrics protect user experience, system performance, and business health.
• Examples: latency (p95/p99), crash rate, content quality, policy violations, ad revenue.
• Rule: Primary decides go/no-go; guardrails ensure we don’t “win dirty.”

2. Power & Sample Size
• Use historical data to estimate baseline metrics and plug into a calculator or internal tooling.
• Apply techniques to reduce sample size:
• Trigger-based sampling: include only exposed/affected users
• Variance reduction (e.g. CUPED): use pre-experiment behavior as a covariate
• Adjust for clustering: feeds aren’t IID, so real sample needs may be higher (see next)

4. Feed-Specific Statistical Considerations
• Feeds violate the IID assumption — user and content exposures are highly correlated.

Design strategies:
• Use user-level randomization to avoid users seeing both treatment and control
• Trigger-based: only count users who open the feed
• Use switchback experiments when testing infrastructure (alternate by time slot or geography)

Analysis strategies:
• Aggregate metrics at the user-day level
• Use cluster-robust standard errors to account for within-user correlations
• Pre-bucket users to stabilize variance across experiments
• Use inverse propensity weighting or position correction if needed at impression level

Leakage control:
• Avoid splitting viral content or creators across groups
• For highly interconnected systems, consider ghost experiments (logging-only) or community-level randomization





Recommendation System: A/B Test System Design (Implementation Details)
Recommendation System: A/B Test System Design (Implementation Details)
Jan 2024 - Jan 2024Jan 2024 - Jan 2024
1. Trustworthiness: SRM, Stopping Rules, Multiplicity
• SRM (Sample Ratio Mismatch): check that control/treatment ratios match expectations.
• Use chi-square test; if mismatched, pause and investigate routing or triggering logic.

Stopping rules: pre-register window and analysis plan.
• Don’t peek and stop early without correction — it increases false positive risk.
• Use alpha-spending or Bayesian approaches for valid early stopping.

Multiple comparisons:
• Stick to one primary metric
• For secondary metrics or multiple variants, apply FDR correction (e.g. Benjamini-Hochberg)
• When running multiple variants, bandits are useful, but final rollout should be confirmed with traditional testing

2. Practical Execution Plan
• 1. Define goal and thresholds
– “We aim for a +1% lift in daily engagement.”
– MDE = +1%, alpha = 0.05, power = 0.8

• 2. Estimate sample size
– Use historical data and tools to calculate triggered users per group

• 3. Randomization
– User-level bucketing
– Include only triggered users (e.g. those opening the feed)
– Avoid creator/content leakage across groups

• 4. Variance reduction
– Use historical behavior (e.g. previous 7-day averages) as covariates

• 5. Metric computation and significance
– Aggregate at user-day level
– Use cluster-robust t-tests or regression

• 6. Health checks
– Sample Ratio Mismatch (SRM)
– Latency, crash rate
– Guardrail metrics (e.g. harmful content, user complaints)

• 7. Interpretation and rollout
– Check if primary passed, and guardrails held
– Analyze heterogeneity (e.g. new vs. existing users)
– Decide: roll out, iterate, or rollback
– Optionally run follow-up experiment to confirm long-term effects (e.g. 28-day retention)
```



### Seleted Projects
![image](https://github.com/user-attachments/assets/d8554f23-e3b4-4a15-93ce-e840d53606df)

- VMAF Netflix Enhancing Video Streaming Quality Through Advanced Encoding and Evaluation Techniques https://github.com/TeleViaBox/vid-stream-quality-public
- my App 1: RAG (retrieval augmented generation) LLM chat app (deployed and hosted on GCP) https://github.com/TeleViaBox/society-llm-opinions-public
- my App 2: RealEstateProject https://github.com/TeleViaBox/RealEstateProject_beautified_beau_new_upload

# Open Source Contributions

## Recommendation Systems
- Spotify/Pedalboard: Fixed #411. [Method] Added 20-line PortAudio guard that raises RunTime Error when an output device vanishes, [Issue] eliminating an infinite-block bug that could [Impact] stall Spotify’s Safe-and-Sound pipelines (used to vet 7 M+ podcasts for 696 M MAU)

- Meta-RecSys/Generative-Recommenders: Fixed #308. [Method] Added a gin-configurable HSTU attention backend dispatcher (auto→C++ on Hopper, else logs safe fallback) without changing defaults. [Issue] Addresses the H100 efficiency / missing integration called out. [Impact] Hopper gets the optimized attention path without public-pipeline changes; HSTU underpins large-scale GR incl. context-parallel, and is referenced in NVIDIA RecSys examples.

## ML System (Inference, Serving, ...)

## Autonomus Driving and Vision-Language-Action (VLA) models (Robotics)

### about me
##### skill sets
- Lang: c, c++, matlab, python, java
- Language skills: Object-oriented programming, Large system's scalability design
- Hardware related: signal processing, image processing, encoding/decoding computation
- Software related: vmware, postman

### Finished projects' list
1. light-weight search engine deployed on GCP (Google Compute Engine), with LLM chatting features, by preprocessing novels from Project Gutenberg using RAG (retrieval augmented generation). [Link](https://github.com/TeleViaBox/search-engine)
2. sepolia blockchain (ethereum based testnet) deployment of smart contract for real estate trading, and full-stack website (using flask app) deployed on GCP. [Link](https://github.com/TeleViaBox/blockchain-market)


### current projects
1. https://github.com/TeleViaBox/vidtrans/
2. https://github.com/TeleViaBox/vqaeffic/blob/main/README.md
3. "not yet for public": https://github.com/TeleViaBox/leos-vehicle-network

### not-yet finished projects' list
3. Machine learning toolbox for information-space search task, vector database, loss functions.
4. dashboard webiste for easy-to-use data import and visualization
5. travel spot search and visualization project
6. Page rank and reverse-connected network analysis
7. Tubluar machine and system-stability controller hyperparameter optimization, with heuristic approaches
8. "Course" Operating System experiments [Link](https://github.com/TeleViaBox/pintos-prac)
9. "Course" Computer Security experiments
10. "Course" Computer Networks experiments
11. "Course" Algorithm Analysis and Design
12. Hard problems solving [Link](https://github.com/TeleViaBox/hard-prob-solv)
13. My understanding in computer science [Link](https://github.com/TeleViaBox/my-understanding-cs/)
14. JAVA: building a multimedia 2d windows desktop application
15. data science EDA with my school's course list
16. My understanding in IQA (Image quality assessment) and VQA (Video quality assessment) [Link](https://github.com/TeleViaBox/iqa-vqa-study)
17. My understanding in Optimization theory design [Link](https://github.com/TeleViaBox/opt-theory-study)
18. My understanding in Computer Network

### not-yet started projects' list
14. Pac-man design
15. Whats-app design

### interview: ML aspects

### interview: Search engine aspects

### interview: Algorithm aspects

### interview: System and network aspects
- topics: distributed system, network system, operating system

### reading list
- Argmax Flows and Multinomial Diffusion: Learning Categorical Distributions
: https://www.youtube.com/watch?v=150ceiAVDCY
- Breaking the Sample Size Barrier in Reinforcement Learning via Model-Based Algorithms: https://www.youtube.com/watch?v=7PYfv9KRZfQ
- Improving and Generalizing Flow-Based Generative Models with Minibatch Optimal Transport | Alex Tong
: https://www.youtube.com/watch?v=UhDtH7Ia9Ag

### Appendix: How to prepare repos
- Application-oriented purpose: I want to create a code for cancer image recognition.
- Integrate and utilize two large repositories: [Case One: [Case Two:
- High difficulty replication is also possible.
- My preparation status update for Leetcode
- git commit good-practice (Semantic Commit Messages): https://gist.github.com/joshbuchea/6f47e86d2510bce28f8e7f42ae84c716


<!--
**TeleViaBox/TeleViaBox** is a ✨ _special_ ✨ repository because its `README.md` (this file) appears on your GitHub profile.

Here are some ideas to get you started:

- 🔭 I’m currently working on ...
- 🌱 I’m currently learning ...
- 👯 I’m looking to collaborate on ...
- 🤔 I’m looking for help with ...
- 💬 Ask me about ...
- 📫 How to reach me: ...
- 😄 Pronouns: ...
- ⚡ Fun fact: ...
-->

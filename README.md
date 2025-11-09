Hi 👋

I’m building the next generation of **LLM search** and practical AI systems you can actually run.

### What I work on
- 🧠 **LLM Search & RAG** — retrieval pipelines, vector DBs, hybrid search, agentic workflows  
- 🎥 **Video IQA/VQA & streaming quality** — VMAF, encoding & evaluation tooling  
- 📈 **Recommendation systems** — experiment design, metrics, guardrails, and trustworthy analysis  
- 🛠 **Distributed backends** — gRPC services, event buses, background workers  
- 🔗 **Blockchain + full-stack demos** — Sepolia smart contracts, GCP deployments

---

## Backend Stack

**External Interface (B2B / B2C Users)**
- **GraphQL API (HTTP):** Q&A requests, text uploads, job status queries, and result fetching from frontend/web.
- **GraphQL Subscriptions:** Real-time updates (job progress, streaming tokens).

**Internal Communication (between backend services)**
- **gRPC:** Fast, type-safe calls across embedding, retrieval, generation, classification services.
- **Event Bus (SNS→SQS or Kafka/Redpanda):** Async, decoupled workflows for indexing, streaming updates, long-job orchestration.

**Background Task Processing**
- **Celery** (recommended) or **RQ:** Long-running tasks like indexing, embedding generation, offline analysis, batch reporting.

**Persistent Storage & Dependencies**
- **Chroma / Vector DB:** Embedding storage for semantic retrieval (already in use).
- **Redis:** Task-queue broker (Celery/RQ), cache, and pub/sub for GraphQL subscriptions.
- **(Optional) PostgreSQL:** Tenants, billing, quotas, audit logs, job metadata.
- **Object Storage (S3 or equivalent):** Original files, intermediate artifacts, exported results.

---

## Recommendation System: A/B Test System Design

<details>
<summary><b>Business Scope</b> (Feb 2024)</summary>

**1) Metrics: Primary, Secondary, Guardrails**
- **Primary:** single main outcome; attributable, sensitive, stable.  
  *Examples:* daily engagement per user, average time spent, 7-day retention.  
- **Secondary:** aid understanding & side effects.  
  *Examples:* share rate, cold-start content views, creator diversity.  
- **Guardrails:** protect UX, performance, and business health.  
  *Examples:* latency (p95/p99), crash rate, content quality, policy violations, ad revenue.  
- **Rule:** Primary decides go/no-go; guardrails prevent “winning dirty.”

**2) Power & Sample Size**
- Use historical baselines + calculator/internal tooling.
- Reduce sample size via:
  - **Trigger-based sampling:** include only exposed/affected users.
  - **Variance reduction (CUPED):** pre-experiment behavior covariates.
  - **Clustering adjustment:** feeds aren’t IID → real sample needs may be higher.

**4) Feed-Specific Stats Considerations**
- **Design:** user-level randomization; trigger-based (only users who open feed); switchback tests for infra (alternate by time/geography).
- **Analysis:** aggregate at user-day; cluster-robust SEs; pre-bucket users; IPW/position correction at impression level.
- **Leakage control:** avoid splitting viral content/creators; for highly connected systems consider ghost experiments or community-level randomization.
</details>

<details>
<summary><b>Implementation Details</b> (Jan 2024)</summary>

**1) Trustworthiness: SRM, Stopping Rules, Multiplicity**
- **SRM:** chi-square check for expected control/treatment ratios; investigate routing/triggering if mismatched.
- **Stopping rules:** pre-register window & analysis; avoid peeking without correction; use alpha-spending or Bayesian approaches.
- **Multiple comparisons:** one primary metric; FDR (Benjamini–Hochberg) for secondaries/variants; bandits for exploration, confirm final rollout with traditional testing.

**2) Practical Execution Plan**
1. **Define goal & thresholds**  
   – e.g., “+1% lift in daily engagement,” MDE=+1%, α=0.05, power=0.8  
2. **Estimate sample size**  
   – historical data → triggered users per group  
3. **Randomization**  
   – user-level bucketing; include only triggered users; prevent creator/content leakage  
4. **Variance reduction**  
   – use previous 7-day behavior as covariates  
5. **Metrics & significance**  
   – aggregate at user-day; cluster-robust t-tests or regression  
6. **Health checks**  
   – SRM; latency/crash; guardrails (harmful content, complaints)  
7. **Interpretation & rollout**  
   – primary passed + guardrails stable; analyze heterogeneity; roll out / iterate / rollback; optional follow-up for long-term effects (e.g., 28-day retention)
</details>

---

## Selected Projects

![preview](https://github.com/user-attachments/assets/d8554f23-e3b4-4a15-93ce-e840d53606df)

- **VMAF Netflix — Enhancing Video Streaming Quality**  
  Advanced encoding & evaluation techniques  
  https://github.com/TeleViaBox/vid-stream-quality-public

- **my App 1 — RAG LLM Chat App (GCP)**  
  Retrieval-augmented generation chat application, deployed & hosted on GCP  
  https://github.com/TeleViaBox/society-llm-opinions-public

- **my App 2 — RealEstateProject**  
  Full-stack project  
  https://github.com/TeleViaBox/RealEstateProject_beautified_beau_new_upload

---

## Open Source Contributions

### Recommendation Systems
- **Spotify/Pedalboard — Fixed #411**  
  *Method:* 20-line PortAudio guard that raises `RuntimeError` when an output device vanishes.  
  *Issue:* Eliminates an infinite-block bug that could stall Spotify’s Safe-and-Sound pipelines (used to vet 7M+ podcasts for 696M MAU).

- **Meta-RecSys/Generative-Recommenders — Fixed #308**  
  *Method:* Gin-configurable HSTU attention backend dispatcher (auto→C++ on Hopper; safe fallback otherwise) without changing defaults.  
  *Issue:* Addresses H100 efficiency / missing integration.  
  *Impact:* Hopper gets the optimized attention path without public-pipeline changes; HSTU underpins large-scale GR incl. context-parallel and appears in NVIDIA RecSys examples.


---

## About Me

#### Skill sets
- **Languages:** C, C++, MATLAB, Python, Java  
- **Software engineering:** OOP, large-scale system scalability design  
- **Hardware-adjacent:** signal & image processing; encoding/decoding computation  
- **Tools:** VMware, Postman

---

## Finished Projects
1. **Light-weight search engine on GCP (Compute Engine)** with LLM chat via RAG on Project Gutenberg novels.  
   [Repo](https://github.com/TeleViaBox/search-engine)
2. **Sepolia smart contract for real-estate trading** + full-stack website (Flask) deployed on GCP.  
   [Repo](https://github.com/TeleViaBox/blockchain-market)

## Current Projects
1. https://github.com/TeleViaBox/vidtrans/  
2. https://github.com/TeleViaBox/vqaeffic/blob/main/README.md  
3. “not yet for public”: https://github.com/TeleViaBox/leos-vehicle-network

## Not-yet Finished
3. ML toolbox for information-space search (vector DB, loss functions)  
4. Dashboard website for easy data import & visualization  
5. Travel-spot search & visualization  
6. PageRank & reverse-connected network analysis  
7. Tabular machine & system-stability controller hyper-parameter optimization (heuristics)  
8. **Course:** Operating Systems — [pintos-prac](https://github.com/TeleViaBox/pintos-prac)  
9. **Course:** Computer Security experiments  
10. **Course:** Computer Networks experiments  
11. **Course:** Algorithm Analysis & Design  
12. Hard problems solving — [repo](https://github.com/TeleViaBox/hard-prob-solv)  
13. My understanding in computer science — [repo](https://github.com/TeleViaBox/my-understanding-cs/)  
14. Java: multimedia 2D Windows desktop application  
15. Data-science EDA with school course list  
16. IQA (Image) & VQA (Video) study — [repo](https://github.com/TeleViaBox/iqa-vqa-study)  
17. Optimization theory study — [repo](https://github.com/TeleViaBox/opt-theory-study)  
18. My understanding in Computer Network

## Not-yet Started
14. Pac-Man design  
15. WhatsApp design

---

## Interview Notes
- **ML aspects**  
- **Search engine aspects**  
- **Algorithm aspects**  
- **System & network aspects:** distributed systems, networking, operating systems

---

## Reading List
- **Argmax Flows and Multinomial Diffusion: Learning Categorical Distributions** — https://www.youtube.com/watch?v=150ceiAVDCY  
- **Breaking the Sample Size Barrier in RL via Model-Based Algorithms** — https://www.youtube.com/watch?v=7PYfv9KRZfQ  
- **Improving & Generalizing Flow-Based GMs with Minibatch Optimal Transport (Alex Tong)** — https://www.youtube.com/watch?v=UhDtH7Ia9Ag

---

## Appendix: How I Prepare Repos
- Application-oriented goals (e.g., cancer image recognition)  
- Integrate & utilize two large repositories (Case One / Case Two)  
- High-difficulty replication where needed  
- Prep status updates for LeetCode  
- **Semantic commit messages:** https://gist.github.com/joshbuchea/6f47e86d2510bce28f8e7f42ae84c716

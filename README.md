## Hi, I'm Yun 👋

MS student at **Carnegie Mellon University** (School of Computer Science), graduating Dec 2026. Previously SDE intern on **AWS SageMaker Unified Studio** (AI Platform).

I build infrastructure for running LLMs in production: **LLM serving**, **ML platforms**, and **agent runtimes**. I care about systems that stay correct under failure and benchmarks that actually measure what they claim to.

---

### 🔧 Featured projects

#### [Dynamic Multi-LoRA Serving on vLLM](https://github.com/yunzhuj/dynamic-multi-lora)
Popularity-aware multi-LoRA serving on stock vLLM. The hottest adapter `H` is merged into the base weights, so its requests pay **zero LoRA overhead**. Every other adapter `C` is served as an exact delta LoRA `C − H`, because `(W + H) + (C − H) = W + C`.

- **OpenAI-compatible router** with a sliding-window popularity tracker and a guarded switch policy (share threshold, margin, cooldown)
- **Zero-downtime blue-green switching**: start the new vLLM profile, health-check it, promote it, then drain and stop the old one
- **Results on A100**: matches a static pre-merged oracle under stable skew, gives **over 2× lower latency** than vanilla vLLM multi-LoRA after the hot adapter changes, and makes **0 vs. 3** spurious switches against a naive policy under fluctuating traffic

`Python` `vLLM` `PyTorch` `FastAPI` `Modal`

#### [Adaptive-Precision KV Cache + GPU Evaluation Pipeline (KIVI fork)](https://github.com/yunzhuj/KIVI)
Position-based **8/4/2-bit mixed-precision KV cache** for Mistral-7B and Llama, built on top of KIVI, plus the infrastructure used to evaluate it.

- **Cloud GPU evaluation pipeline on Modal** (A100/L40S): 9 LongBench tasks run as parallel per-task containers, with detached execution, persistent volumes and **crash-safe resume**
- **One benchmark harness for FP16, KIVI and the adaptive cache**: warmup, fixed decode length, separate weight vs. KV memory, OOM-aware batch backoff
- **Controlled 8K-context comparison**: memory is **0.73× FP16** (on par with KIVI-4bit), but decode is **2.2× slower**. Profiling traced the slowdown to the 8-bit segment falling back to unfused PyTorch dequantization.

`Python` `PyTorch` `Hugging Face` `CUDA/Triton` `Modal`

---

### 🛠 Tech

**Languages** Python · Java · Go · C/C++ · SQL
**LLM / ML systems** vLLM · PyTorch · Hugging Face · Modal · Amazon Bedrock · FastAPI
**Cloud & infra** AWS · Kubernetes · Docker · Spring Boot · Kafka · Redis · Elasticsearch

### 💼 Experience
- **AWS**, SageMaker Unified Studio: AI-assisted infrastructure authoring and an evaluation framework for agent-generated blueprints (86% → 95% accuracy)
- **eBay**, Cloud Infra: distributed trace analysis over 60K+ daily trace IDs, cutting root-cause debugging time by 60%
- **GE Healthcare**: Kubernetes-deployed AI verification microservice
- **Z.AI × Tsinghua KEG**: RAG system with dense retrieval, +71% retrieval accuracy

---

📫 [LinkedIn](https://www.linkedin.com/in/zhuyunj/) · yunzhu@cs.cmu.edu

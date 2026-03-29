# LLM Acceleration: From Algorithms to Systems

A holistic view of the LLM acceleration field, showing how algorithmic choices ripple through models, training, inference, hardware, compilers, and systems.

### Act I — The Model (Lectures 1–6)

**Lecture 1 — Dark Silicon + Scaling Laws / Data**

The end of Dennard scaling means that shrinking transistors no longer delivers free performance gains — the traditional hardware scaling path is a dead end, just as traditional programming models can no longer extract more from general-purpose processors. But at the same time, we are in an era of data explosion — more text, images, and code than ever before — and scaling laws show us how to convert that abundance of data into model capability under fixed compute budgets. We then push this further with "Textbooks Are All You Need," showing that it's not just data quantity but data quality that matters — expert-curated data can replace brute-force scaling, fundamentally reshaping how we think about the compute-data-quality tradeoff that drives every design decision in this course.

Required readings:
1. Esmaeilzadeh et al., "Dark Silicon and the End of Multicore Scaling", ISCA 2011 — https://cseweb.ucsd.edu/~hadi/doc/paper/2011-isca-dark_silicon.pdf
2. Kaplan et al., "Scaling Laws for Neural Language Models", 2020 — https://arxiv.org/abs/2001.08361
3. Hoffmann et al., "Training Compute-Optimal Large Language Models" (Chinchilla), NeurIPS 2022 — https://arxiv.org/abs/2203.15556
4. Gunasekar et al., "Textbooks Are All You Need", 2023 — https://arxiv.org/abs/2306.11644

**Lecture 2 — Gradient Descent / Optimization**

Lecture 1 showed us what to optimize for — now we ask how. Backpropagation gives us the mechanism to compute gradients through deep networks, but naive gradient descent fails at scale due to vanishing gradients and slow convergence — ResNet's residual connections and regularization via weight decay solved the depth problem and became the architectural backbone that transformers later inherited. Adam then solved the optimizer problem by adapting learning rates per-parameter, and it remains the optimizer behind virtually every LLM training run today.

Required readings:
1. Rumelhart, Hinton & Williams, "Learning Representations by Back-Propagating Errors", Nature 1986 — https://www.nature.com/articles/323533a0
2. Goodfellow, Bengio & Courville, "Deep Learning" Chapter 8: Optimization for Training Deep Models, 2016 — https://www.deeplearningbook.org/contents/optimization.html
3. He et al., "Deep Residual Learning for Image Recognition" (ResNet), CVPR 2016 — https://arxiv.org/abs/1512.03385
4. Kingma & Ba, "Adam: A Method for Stochastic Optimization", ICLR 2015 — https://arxiv.org/abs/1412.6980

**Lecture 3 — Learning Paradigms + Alignment**

Before we can build models, we need to understand how they learn. We start with the foundational paradigms — supervised, unsupervised, and self-supervised learning — then see how GPT-1 demonstrated that self-supervised pretraining on raw text followed by supervised fine-tuning became the dominant recipe for language models. We then trace how RLHF added human preferences into the training loop to produce useful assistants, and how DeepSeek-R1's GRPO eliminated the need for both reward models and critics, unlocking the reasoning model era at a fraction of the cost.

Required readings:
1. Goodfellow, Bengio & Courville, "Deep Learning" Chapters 5 + 15: Supervised/Unsupervised Learning, 2016 — https://www.deeplearningbook.org/
2. Radford et al., "Improving Language Understanding by Generative Pre-Training" (GPT-1), 2018 — https://cdn.openai.com/research-covers/language-unsupervised/language_understanding_paper.pdf
3. Ouyang et al., "Training Language Models to Follow Instructions with Human Feedback" (InstructGPT/RLHF), NeurIPS 2022 — https://arxiv.org/abs/2203.02155
4. DeepSeek-AI, "DeepSeek-R1: Incentivizing Reasoning Capability in LLMs via Reinforcement Learning", 2025 — https://arxiv.org/abs/2501.12948

Optional readings:
- Alammar, "The Illustrated GPT-2 (Visualizing Transformer Language Models)", 2019 — https://jalammar.github.io/illustrated-gpt2/

**Lecture 4 — Attention, Transformers + Diffusion**

With learning paradigms and optimization established, we now build the architectures that dominate modern AI. We start with the original transformer's encoder-decoder design and self-attention mechanism, then trace how the decoder-only variant won for language — with Llama demonstrating the modern recipe of RoPE, RMSNorm, SwiGLU, and GQA that every open model now follows. We then cross into generative vision, where Stable Diffusion brought encoder-decoder back via latent diffusion with U-Net, before DiT replaced U-Net with a transformer backbone — showing that the attention mechanism is converging as the universal compute primitive across both language and vision.

Required readings:
1. Vaswani et al., "Attention Is All You Need", NeurIPS 2017 — https://arxiv.org/abs/1706.03762
2. Touvron et al., "LLaMA: Open and Efficient Foundation Language Models", 2023 — https://arxiv.org/abs/2302.13971
3. Rombach et al., "High-Resolution Image Synthesis with Latent Diffusion Models" (Stable Diffusion), CVPR 2022 — https://arxiv.org/abs/2112.10752
4. Peebles & Xie, "Scalable Diffusion Models with Transformers" (DiT), ICCV 2023 — https://arxiv.org/abs/2212.09748

Optional readings:
- Alammar, "The Illustrated Transformer", 2018 — https://jalammar.github.io/illustrated-transformer/
- Sennrich et al., "Neural Machine Translation of Rare Words with Subword Units" (BPE), ACL 2016 — https://arxiv.org/abs/1508.07909
- Su et al., "RoFormer: Enhanced Transformer with Rotary Position Embedding" (RoPE), 2021 — https://arxiv.org/abs/2104.09864

**Lecture 5 — Model Capabilities: MoE, Multimodal, Reasoning**

Now that we understand the transformer, we ask how to make it stronger. Mixture of Experts achieves scale without proportional compute cost through sparse activation — DeepSeek-V3 shows why routing tokens to specialized experts works better than running everything through a dense network, activating only 37B of 671B parameters per token. We then extend the model's senses with LLaVA's vision-language architecture, before turning to reasoning — where we contrast explicit reasoning (chain-of-thought, generating visible thinking tokens as in o1/R1) with implicit reasoning (Coconut, where the model reasons in continuous latent space without producing language tokens), a distinction that has profound implications for acceleration since explicit reasoning multiplies token generation cost while implicit reasoning adds compute without token overhead.

Required readings:
1. DeepSeek-AI, "DeepSeek-V3 Technical Report", 2024 — https://arxiv.org/abs/2412.19437
2. Liu et al., "Visual Instruction Tuning" (LLaVA), NeurIPS 2023 — https://arxiv.org/abs/2304.08485
3. Wei et al., "Chain-of-Thought Prompting Elicits Reasoning in Large Language Models", NeurIPS 2022 — https://arxiv.org/abs/2201.11903
4. Hao et al., "Training Large Language Models to Reason in a Continuous Latent Space" (Coconut), ICLR 2025 — https://arxiv.org/abs/2412.06769

**Lecture 6 — RAG, Agentic RAG, Agentic Systems**

With powerful models in hand, we now make them useful in the real world. RAG grounds language models in external knowledge by retrieving relevant documents at inference time, and ReAct generalizes this into a full agent loop of reasoning, acting, and observing — with MemGPT addressing the real engineering challenge of managing the finite context window as a scarce resource through OS-style virtual memory. We close with Self-RAG as a concrete example of agentic RAG in action: the model autonomously decides when to retrieve, what to retrieve, and critiques its own outputs — demonstrating what happens when you combine retrieval with agentic decision-making.

Required readings:
1. Lewis et al., "Retrieval-Augmented Generation for Knowledge-Intensive NLP Tasks", NeurIPS 2020 — https://arxiv.org/abs/2005.11401
2. Yao et al., "ReAct: Synergizing Reasoning and Acting in Language Models", ICLR 2023 — https://arxiv.org/abs/2210.03629
3. Packer et al., "MemGPT: Towards LLMs as Operating Systems", 2023 — https://arxiv.org/abs/2310.08560
4. Asai et al., "Self-RAG: Learning to Retrieve, Generate, and Critique through Self-Reflection", ICLR 2024 — https://arxiv.org/abs/2310.11511

---

### Act II — Training + Making It Efficient (Lectures 7–9)

**Lecture 7 — Distributed Training**

Having completed the model-side story, we now face the practical question: how do you actually train a 671B parameter model? No single GPU can hold it, so we need to decompose the problem across thousands of devices. Megatron-LM introduced tensor parallelism — splitting individual attention and MLP layers across GPUs using AllReduce over NVLink — while ZeRO eliminated the memory redundancy of data parallelism by sharding optimizer states, gradients, and parameters. The real challenge is composing these strategies: the Megatron-LM v2 paper shows how tensor, pipeline, and data parallelism must be orchestrated together, with communication primitives carefully mapped to the hardware topology — AllReduce over NVLink intra-node for tensor parallelism, point-to-point over InfiniBand inter-node for pipeline parallelism — a design philosophy validated at scale by Meta's Llama 3 training across 16K GPUs with 4D parallelism.

Required readings:
1. Shoeybi et al., "Megatron-LM: Training Multi-Billion Parameter Language Models Using Model Parallelism", 2019 — https://arxiv.org/abs/1909.08053
2. Narayanan et al., "Efficient Large-Scale Language Model Training on GPU Clusters Using Megatron-LM", SC 2021 — https://arxiv.org/abs/2104.04473
3. Meta, "Scaling Llama 3 Training with Efficient Parallelism Strategies", ISCA 2025 — https://aisystemcodesign.github.io/papers/Llama3-ISCA25.pdf

**Lecture 8 — Efficient Inference Architectures**

Now that we know how to train models at scale, we turn to making inference affordable. The autoregressive bottleneck — generating one token at a time, memory-bandwidth-bound — is the central problem, and this lecture covers two major attack vectors. The first reduces the cost per token: GQA/MQA share key-value heads to shrink the KV cache, and Mamba replaces quadratic attention entirely with linear-time recurrence. The second generates multiple tokens at once: speculative decoding uses a small draft model to propose multiple tokens that the large model verifies in parallel, turning the memory-bound decode phase into a compute-bound verification — achieving 2–3x speedups without changing the output distribution.

Required readings:
1. Leviathan et al., "Fast Inference from Transformers via Speculative Decoding", ICML 2023 — https://arxiv.org/abs/2211.17192
2. Ainslie et al., "GQA: Training Generalized Multi-Query Transformer Models from Multi-Head Checkpoints", EMNLP 2023 — https://arxiv.org/abs/2305.13245
3. Gu & Dao, "Mamba: Linear-Time Sequence Modeling with Selective State Spaces", ICLR 2024 — https://arxiv.org/abs/2312.00752

Optional readings:
- Shazeer, "Fast Transformer Decoding: One Write-Head is All You Need" (MQA), 2019 — https://arxiv.org/abs/1911.02150
- Lieber et al., "Jamba: A Hybrid Transformer-Mamba Language Model", 2024 — https://arxiv.org/abs/2403.19887

**Lecture 9 — Model Compression: Quantization, LoRA, Sparsity**

Before we move to hardware, we first make the model smaller. This lecture covers three complementary compression axes that stack: quantization reduces bits per weight (FP16 → INT4), LoRA reduces trainable parameters during fine-tuning by learning low-rank weight updates that merge back at zero inference cost, and N:M sparsity zeros out weights in hardware-friendly patterns that NVIDIA's Sparse Tensor Cores accelerate at 2x throughput. The key insight is these are orthogonal — you can prune a model to 2:4 sparsity, quantize it to INT4, and add LoRA adapters for task-specific fine-tuning, compounding the compression without compounding the quality loss.

Required readings:
1. Frantar et al., "GPTQ: Accurate Post-Training Quantization for Generative Pre-trained Transformers", ICLR 2023 — https://arxiv.org/abs/2210.17323
2. Hu et al., "LoRA: Low-Rank Adaptation of Large Language Models", ICLR 2022 — https://arxiv.org/abs/2106.09685
3. Mishra et al., "Accelerating Sparse Deep Neural Networks", 2021 — https://arxiv.org/abs/2104.08378

---

### Act III — Running It (Lectures 10–15)

**Lecture 10 — GPU Architecture + Flash Attention / Kernel Optimizations**

With compressed models ready to deploy, we now need to understand the hardware that runs them. Modern GPUs are no longer just arrays of generic CUDA cores — they are systems-on-chip packed with specialized accelerators: tensor cores for matrix math, texture units, ray tracing cores, DMA engines, and dedicated memory controllers, all connected through a deep memory hierarchy where performance lives or dies by data movement, not arithmetic. We dissect the Hopper GPU architecture through microbenchmarking — streaming multiprocessors, warp scheduling, the registers → shared memory → L2 → HBM hierarchy, tensor cores with FP8 support, and NVLink interconnect. FlashAttention then demonstrates these principles in action — by tiling attention computation to fit in SRAM and fusing the entire kernel to avoid writing the N×N attention matrix to HBM, it achieves 2–4x speedup through pure IO awareness. FlashAttention-2 improved parallelism and work partitioning across warps, and FlashAttention-3 goes further by exploiting Hopper-specific features: warp-specialized asynchrony to overlap tensor core computation with TMA data movement, interleaved GEMM-softmax pipelining, and FP8 block quantization — reaching 75% utilization on H100 (up from 35% with FA-2) and 1.2 PFLOPs/s in FP8. FlashAttention-4 then confronts the Blackwell generation's asymmetric hardware scaling: tensor core throughput doubles from Hopper to B200 while shared memory bandwidth and exponential function units stagnate, so FA-4 redesigns the pipeline with software-emulated exponentials on FMA units, conditional softmax rescaling, and Blackwell's new tensor memory and 2-CTA MMA mode — reaching 1.6 PFLOPs/s (71% utilization) on B200, and notably implemented entirely in CuTe-DSL (Python) with 20–30× faster compile times than C++ templates.

Required readings:
1. Luo et al., "Benchmarking and Dissecting the Nvidia Hopper GPU Architecture", IPDPS 2024 — https://arxiv.org/abs/2402.13499
2. Dao et al., "FlashAttention: Fast and Memory-Efficient Exact Attention with IO-Awareness", NeurIPS 2022 — https://arxiv.org/abs/2205.14135
3. Dao, "FlashAttention-2: Faster Attention with Better Parallelism and Work Partitioning", ICLR 2024 — https://arxiv.org/abs/2307.08691
4. Shah et al., "FlashAttention-3: Fast and Accurate Attention with Asynchrony and Low-precision", NeurIPS 2024 — https://arxiv.org/abs/2407.08608
5. Zadouri et al., "FlashAttention-4: Algorithm and Kernel Pipelining Co-Design for Asymmetric Hardware Scaling", 2026 — https://arxiv.org/abs/2603.05451

Optional readings:
- Huerta et al., "Analyzing Modern NVIDIA GPU cores", 2025 — https://arxiv.org/abs/2503.20481
- Lindholm et al., "NVIDIA Tesla: A Unified Graphics and Computing Architecture", IEEE Micro 2008

**Lecture 11 — Domain-Specific Accelerators: TPUs, Groq, PIM**

Having understood GPUs as flexible but complex SoCs, we now ask: what if we threw away the generality entirely? The TPU v1 bet on systolic arrays and deterministic execution for inference, and TPUv2/v3 evolved this into a full training accelerator with VLIW cores, scalar/vector/matrix units, HBM, and bfloat16 — co-designed with the XLA compiler from the start. Groq pushed further with SRAM-only inference and fully deterministic scheduling, eliminating HBM entirely to remove the memory bandwidth bottleneck at the cost of model size limitations. Processing-in-Memory represents the emerging frontier — rather than moving data to compute, move compute to data — addressing the fundamental bottleneck that dominates LLM inference.

Required readings:
1. Jouppi et al., "In-Datacenter Performance Analysis of a Tensor Processing Unit", ISCA 2017 — https://arxiv.org/abs/1704.04760
2. Norrie et al., "The Design Process for Google's Training Chips: TPUv2 and TPUv3", IEEE Micro 2021 — https://ieeexplore.ieee.org/document/9351692
3. Abts et al., "Think Fast: A Tensor Streaming Processor (TSP) for Accelerating Deep Learning Workloads" (Groq), ISCA 2020 — https://ieeexplore.ieee.org/stamp/stamp.jsp?tp=&arnumber=9138986
4. Kwon et al., "AIM: Energy-Efficient Aggregation Inside the Memory for Large Language Models", ISCA 2025 — https://arxiv.org/abs/2407.12397

**Lecture 12 — Compiler Optimizations**

The DSAs from lecture 11 are entirely software-controlled — there are no caches or out-of-order execution to hide programmer mistakes, so the compiler must orchestrate every data movement and computation explicitly. TVM established the end-to-end framework: graph-level optimizations like operator fusion, operator-level tiling and vectorization, and learning-based auto-tuning to search the optimization space across diverse hardware. MLIR then tackled the multi-target problem head-on — its dialect system lets a single compiler infrastructure progressively lower from high-level tensor operations down to hardware-specific code for CPUs, GPUs, TPUs, and custom accelerators, generating optimized kernels at each abstraction level. We close with KernelBench, where Stanford's Scaling Intelligence Lab asks whether LLMs can bypass compilers entirely and directly write high-performance CUDA kernels from PyTorch specifications — reframing kernel engineering itself as a code generation problem.

Required readings:
1. Chen et al., "TVM: An Automated End-to-End Optimizing Compiler for Deep Learning", OSDI 2018 — https://arxiv.org/abs/1802.04799
2. Lattner et al., "MLIR: A Compiler Infrastructure for the End of Moore's Law", 2020 — https://arxiv.org/abs/2002.11054
3. Ouyang et al., "KernelBench: Can LLMs Write Efficient GPU Kernels?", 2025 — https://arxiv.org/abs/2502.10517

**Lecture 13 — LLM Serving Software**

This lecture assembles the serving software stack. Orca introduced continuous batching — scheduling at iteration granularity instead of request granularity — which lets the system insert and remove requests every decode step, making high-throughput LLM serving practical for the first time. SGLang recognized that real LLM workloads are not isolated requests but structured programs of chained calls with shared prefixes (agent loops, few-shot prompts, RAG pipelines), so its RadixAttention maintains a radix tree of cached KV states for automatic prefix reuse, while compressed finite state machines accelerate structured output decoding like JSON and function calls.

Required readings:
1. Yu et al., "Orca: A Distributed Serving System for Transformer-Based Generative Models", OSDI 2022 — https://www.usenix.org/conference/osdi22/presentation/yu
2. Zheng et al., "SGLang: Efficient Execution of Structured Language Model Programs", NeurIPS 2024 — https://arxiv.org/abs/2312.07104
3. Yang et al., "Context Parallelism for Scalable Million-Token Inference", 2024 — https://arxiv.org/abs/2411.01783

Discussion/Assignment — The Parallelism Matrix for LLM Serving:

You are the architect of a datacenter serving both short-context chatbot traffic and long-context document analysis. (1) Enumerate all parallelism dimensions (TP, PP, DP, CP, EP, PD, batching, KV reuse). (2) For each pair, classify as orthogonal, synergistic, or interfering. (3) Map parallelisms to hardware topology (NVLink intra-node, RDMA inter-node, disaggregation) and justify using Amdahl's Law, Little's Law, and prefill/decode asymmetry.

**Lecture 14 — KV Cache Management + Prefill-Decode Scheduling**

The KV cache is the central bottleneck of LLM serving — it grows dynamically, fragments GPU memory, and must be transferred or reused across requests. vLLM solved the memory management problem by borrowing virtual memory and paging from OS design: KV cache blocks are stored in non-contiguous physical memory mapped through page tables, eliminating fragmentation and enabling copy-on-write sharing for parallel sampling. Mooncake then elevated the KV cache to a first-class distributed resource — disaggregating prefill and decode onto separate GPU clusters while building a distributed KV cache pool across CPU, DRAM, and SSD that enables cross-request reuse and prefix caching at the scale of Kimi's production workload. DistServe formalized the case for PD disaggregation: because prefill is compute-bound and decode is memory-bound, colocating them on the same GPU forces one phase to suffer — DistServe co-optimizes resource allocation and parallelism independently for each phase, serving 7.4× more requests within SLO. But Sarathi-Serve challenges full disaggregation with a simpler alternative: chunked prefills break long prefills into small chunks that interleave with ongoing decodes on the same GPU, exploiting the arithmetic intensity slack during decode iterations to get the benefits of separation without the network overhead of KV cache transfer.

Required readings:
1. Kwon et al., "Efficient Memory Management for Large Language Model Serving with PagedAttention", SOSP 2023 — https://arxiv.org/abs/2309.06180
2. Qin et al., "Mooncake: A KVCache-centric Disaggregated Architecture for LLM Serving", FAST 2025 (Best Paper) — https://arxiv.org/abs/2407.00079
3. Zhong et al., "DistServe: Disaggregating Prefill and Decoding for Goodput-optimized Large Language Model Serving", OSDI 2024 — https://arxiv.org/abs/2401.09670
4. Agrawal et al., "Taming Throughput-Latency Tradeoff in LLM Inference with Sarathi-Serve", OSDI 2024 — https://arxiv.org/abs/2403.02310

**Lecture 15 — Network Infrastructure + DPUs**

The final lecture zooms out from software to the physical infrastructure that makes everything possible. ShadowServe asks: if KV cache transfer is the data-plane bottleneck of prefix caching and PD disaggregation, why burn GPU or CPU cycles on it? It offloads KV cache fetching, decompression, and dequantization entirely to NVIDIA BlueField-3 DPUs, achieving interference-free prefix caching — the GPU focuses purely on model computation while the SmartNIC handles all data movement. This is the emerging architectural pattern: DPUs as infrastructure accelerators that free GPUs from non-model work. We close by zooming out to the physical network that connects everything: Meta's SIGCOMM paper reveals how they built one of the world's largest AI fabrics using RoCEv2, covering rail-optimized topology, ECMP load balancing for low-entropy GPU traffic, receiver-driven congestion control co-designed with NCCL, and how this infrastructure underpins both distributed training at 16K+ GPUs and the KV cache transfers that disaggregated serving depends on — connecting back through the entire course from Lecture 7 (distributed training) through Lecture 14 (PD disaggregation) to the wire.

Required readings:
1. Xiang et al., "ShadowServe: Interference-Free KV Cache Fetching for Distributed Prefix Caching", 2025 — https://arxiv.org/abs/2509.16857
2. Gangidi et al., "RDMA over Ethernet for Distributed Training at Meta Scale", ACM SIGCOMM 2024 — https://dl.acm.org/doi/10.1145/3651890.3672233

**Lecture 16 — Lookback: Laws and Design Philosophies**

**Quantitative laws.** Amdahl's Law bounds speedup by the serial fraction — the reason autoregressive decode can't be parallelized away and why PD disaggregation exists. Gustafson's Law is the escape: grow the problem with the hardware, and the serial fraction shrinks — which is exactly what LLM scaling does (bigger model, more GPUs, more data). Little's Law (L = λW) governs serving: concurrency equals throughput times latency, so to saturate GPUs you need enough requests in flight — the reason continuous batching and PagedAttention matter.

**Hardware.** RISC vs CISC: simple hardware + smart compiler beats complex hardware. VLIW pushed this further — let the compiler schedule everything statically — and failed for general-purpose code (Itanium) but succeeded for DSAs where workloads are predictable (TPUv2/v3 uses VLIW cores).

**Compilers.** Proebsting's Law is a tongue-in-cheek quip: compiler optimizations double performance every 18 years vs Moore's Law's 18 months. Nobody refuted it. On GP hardware the compiler adds little because OoO execution compensates dynamically; on DSAs the compiler is the *only* path to performance but still can't find optimizations like FlashAttention — a human had to. Compiler research for accelerators still has a long way to go, which is why KernelBench (Lecture 12) asks whether LLMs can write kernels instead.

**AI.** Sutton's Bitter Lesson: general methods that scale with compute beat hand-crafted domain knowledge.

**Systems.** Gabriel's "Worse is Better": implementation simplicity beats interface elegance — Unix, C, PyTorch, vLLM, CUDA all won this way.

**Integration.** Alan Kay (1982): "People who are really serious about software should make their own hardware" — Google TPU, Apple silicon, the entire DSA story.

**Synthesis.** Hennessy & Patterson's Turing Lecture: end of Moore's Law opens a new golden age for domain-specific co-design of hardware, compilers, and applications — the thesis of this entire course.

Required readings:
1. Sutton, "The Bitter Lesson", 2019 — http://www.incompleteideas.net/IncompleteIdeas/BitterLesson.html
2. Gabriel, "The Rise of Worse is Better", 1989 — https://www.dreamsongs.com/RiseOfWorseIsBetter.html
3. Proebsting, "Proebsting's Law: Compiler Advances Double Computing Power Every 18 Years" — http://proebsting.cs.arizona.edu/law.html
4. Kay, "People who are really serious about software should make their own hardware", Creative Think seminar, 1982
5. Hennessy & Patterson, "A New Golden Age for Computer Architecture", Communications of the ACM, 2019 — https://cacm.acm.org/magazines/2019/2/234352-a-new-golden-age-for-computer-architecture/fulltext

## Schedule — Spring 2026

MW 6:30–7:50p | 19 class sessions | 16 lectures + 3 flex slots

| # | Date | Day | Topic |
|---|------|-----|-------|
| 1 | Mar 30 | Mon | Lecture 1 — Dark Silicon + Scaling Laws / Data |
| 2 | Apr 01 | Wed | Lecture 2 — Gradient Descent / Optimization |
| 3 | Apr 06 | Mon | Lecture 3 — Autoencoders / Learning Paradigms |
| 4 | Apr 08 | Wed | Lecture 4 — Attention + Stable Diffusion |
| 5 | Apr 13 | Mon | Lecture 5 — Model Capabilities: MoE, Multimodal, Reasoning |
| 6 | Apr 15 | Wed | Lecture 6 — RAG, Agentic RAG, Agentic Systems |
| 7 | Apr 20 | Mon | Lecture 7 — Distributed Training |
| 8 | Apr 22 | Wed | Lecture 8 — Efficient Inference Architectures |
| 9 | Apr 27 | Mon | Lecture 9 — Model Compression |
| 10 | Apr 29 | Wed | Lecture 10 — GPU Architecture + Flash Attention / Kernel Opts |
| 11 | May 04 | Mon | Lecture 11 — DSAs: TPUs / Groq / PIM |
| 12 | May 06 | Wed | Lecture 12 — Compiler Optimizations |
| 13 | May 11 | Mon | Lecture 13 — LLM Serving Software |
| 14 | May 13 | Wed | Lecture 14 — KV Cache Management + Prefill-Decode Scheduling |
| 15 | May 18 | Mon | Lecture 15 — Network Infrastructure + DPUs |
| 16 | May 20 | Wed | Lecture 16 — Lookback: Design Philosophies |
| — | May 25 | Mon | NO CLASS — Memorial Day |
| 17 | May 27 | Wed | TBD (flex) |
| 18 | Jun 01 | Mon | TBD (flex) |
| 19 | Jun 03 | Wed | TBD (flex) |

Final exams: June 6–12

---

# Anonymous Task Assignment and Worker Payment in Mobile Crowdsensing (PTAP)

**PTAP** (Privacy-preserving Task Assignment and Payment) is a lightweight, high-performance framework designed for mobile crowdsensing (MCS). It leverages 

**Secure Multi-Party Computation (SMPC)** to protect worker anonymity and location privacy without the heavy computational overhead of blockchain or Zero-Knowledge Proofs.



## Core Security Pillars
* **Information-Theoretic Security (ITS):** Unlike systems relying on the hardness of mathematical problems (Computational Security), PTAP’s privacy is mathematically guaranteed. Even an adversary with infinite computing power cannot learn the worker's private data from the secret shares.
* **Asymmetric Design & Efficiency:** PTAP utilizes an asymmetric architecture where a third server facilitates the operations of the two primary servers. This design reduces heavy non-linear operations (e.g., secure comparisons) into **linear operations** with **constant rounds of communication**, significantly boosting throughput.
* **No Trusted Setup:** PTAP removes the need for a "Trusted Third Party" or complex initial parameter ceremonies (required by zk-SNARKs). This eliminates centralized points of failure and simplifies deployment.
* **Zero Gas Cost:** By avoiding blockchain interactions for verification, PTAP eliminates transaction fees and the latency associated with public ledgers.
* **Complete Unlinkability:** The framework ensures that worker identities, specific task locations, and payment records cannot be linked by the platform or curious servers.



---

## Threat Model: Semi-Honest Adversaries
PTAP is designed under the **semi-honest (honest-but-curious) model**, the standard security assumption for high-integrity cloud environments.

* **Server Behavior:** Servers $\mathcal{S}_1$, $\mathcal{S}_2$, and $\mathcal{S}_3$ are assumed to follow the protocol instructions exactly. They do not inject malicious data.
* **Curiosity:** An adversary may compromise at most one of the primary servers to monitor secret shares and attempt to infer worker IDs or mobility patterns.
* **Security Guarantee:** Privacy remains intact as long as the servers do not collude to combine their shares. No individual server ever views the plaintext data.



---

## Technical Architecture
PTAP utilizes **Additive Secret Sharing** over a prime field $\mathbb{Z}_p$ across a three-server architecture:

1.  **Registration:** Workers generate anonymous identities blinded as $[RID] = [ID] + [k]$.
2.  **Task Publishing:** A lightweight **challenge–reponse mechanism** validates eligibility while maintaining location privacy.
3.  **Reimbursement:** Secure token nullification via an asymmetric design that prevents linking payments back to specific tasks.
4.  **Trace:** Authorized recovery of identity from secret shares for dispute resolution and accountability.



---

## Getting Started

### Requirements
* **MP-SPDZ** framework (v0.3.8 or higher).
* Linux or macOS environment with `g++`, `python3`, and `libgmp-dev`.

### Installation & Running the Protocol
1.  **Clone the Framework:**
    Place the `PTAP.mpc` file into your `mp-spdz/Programs/Source/` directory.

2.  **Compile the Script:**
    Navigate to the root of the MP-SPDZ directory and run:
    ```bash
    ./compile.py -F 40 PTAP
    ```

3.  **Run with 3 Parties (Semi-honest):**
    To execute the protocol using the `semi2k` virtual machine on a single machine for testing:
    ```bash
    Scripts/semi.sh PTAP
    ```

---

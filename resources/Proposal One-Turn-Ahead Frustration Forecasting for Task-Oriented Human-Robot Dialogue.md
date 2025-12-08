**Draft Work-in-Progress Proposal** *One-Turn-Ahead Frustration Forecasting for Task-Oriented Human-Robot Dialogue*

---

### **1 Introduction & Motivation**

Social robots already detect a user’s *current* affect, but often react **after** frustration is voiced. Consequently the interaction feels corrective, not proactive. We propose to close this gap by developing and benchmarking a **one-turn-ahead binary predictor** that flags whether the *next* user utterance will become “dissatisfied / frustrated.” When deployed, Pepper can soften its language, offer clarification, or route to a human **before** negative affect erupts.

---

### **2 Related Work**

| Strand | Key papers | Take-aways & Gap |
| :---- | :---- | :---- |
| **Same-turn frustration detection** | Ang et al., 2002 — prosody-based frustration in IVR ([sri.com](https://www.sri.com/wp-content/uploads/2021/12/prosody-based_automatic_detection_of_annoyance_and_frustr.pdf?utm_source=chatgpt.com)); “Stupid robot…” COLING-Industry 2025 — LLM detects frustration in text logs ([aclanthology.org](https://aclanthology.org/2025.coling-industry.23.pdf?utm_source=chatgpt.com)) | Effective but *reactive*; no published anticipation. |
| **General ERC forecasting** | “Future Affective Reactions in HCD” IUI 2023 (valence/arousal 1-turn forecast, small corpus). | Shows feasibility, but not focused on frustration in task dialogue. |
| **HRI emotion adaptation** | User-VLM 360°: personalised VLM for Pepper, real-time affect sensing (Rahimi et al., 2025). | Supplies perception layer we can extend. |

**No public benchmark** yet measures *turn-ahead frustration* in task-oriented text. That is the opening we target.

---

### **3 Research Questions (RQs)**

| RQ | Statement |
| :---- | :---- |
| **RQ1** | *Can conversational context (≤5 previous turns) predict user frustration one turn ahead better than chance?* |
| **RQ2** | *Does adding Pepper’s vision-based user embeddings (User-VLM facial features) improve textual forecasting?* |
| **RQ3** | *Does early warning reduce human-escalation rate in a Wizard-of-Oz pilot?* |

---

### **4 Study Design**

#### 4.1 Data & Benchmark Construction

1. **Base corpus** — EmoWOZ (56 h, 5 emotions, includes *dissatisfied*)  
2. **Shifted labels** — For each user turn *t*, assign **label \= 1** if turn *t \+ 1* is “dissatisfied,” else 0\.  
3. **Splits** keep official train/dev/test user IDs (≈ 8 k / 1 k / 1 k instances).  
4. Public release: *EmoWOZ-Ahead* test split \+ generation script → first reproducible benchmark.

#### 4.2 Models & Features

| Tier | Inputs | Architecture |
| :---- | :---- | :---- |
| **M0** baseline | majority 0 | – |
| **M1** | last user utterance | BERT-CLS |
| **M2** | 3 previous turns (user+sys) | BERT \+ GRU context encoder |
| **M3** | M2 \+ Pepper vision embedding (128-D) | **User-VLM 360° text head \+ LoRA fusion** |

Hyper-params tuned on dev; LoRA rank \= 32; learning rate 2e-5.

#### 4.3 Evaluation Metrics

* **Macro-F1 (positive vs. negative)** – main reporting figure.  
* **AUC** – secondary (class imbalance).  
* **Latency** – ms per prediction on Pepper Jetson-NX.

---

### **5 Planned Experiments**

| Exp | Purpose | Datasets |
| :---- | :---- | :---- |
| **E1** | RQ1 – compare M0–M2 on EmoWOZ-Ahead test | EmoWOZ-Ahead |
| **E2** | RQ2 – add vision embeddings (M3) | EmoWOZ-Ahead (+ faces) |
| **E3** | Cross-domain robustness | Train EmoWOZ-Ahead; zero-shot test on shifted DailyDialog frustration proxy |
| **E4** | RQ3 – 30 live Pepper sessions (Wizard); measure human-escalation vs. rule baseline |  |

Power analysis: with test N≈1 k, ±3 pp F1 improvement is significant at α=0.05.

---

### **6 Expected Contributions**

1. **First open “turn-ahead” frustration benchmark** (*EmoWOZ-Ahead*).  
2. **Strong baselines \+ User-VLM fusion** (\>0.40 Macro-F1 target, vs. 0.23 BERT).  
3. **Demonstration of proactive repair** reducing escalations by ≥15 % in pilot.  
4. Dataset & code released under CC-BY-4.0 → reproducibility.

---

### **7 Timeline & Milestones**

| Week | Deliverable |
| :---- | :---- |
| 1 | Data shift script \+ benchmark card |
| 2 | M1, M2 baselines (BERT, GRU) |
| 3 | Integrate User-VLM facial encoder (M3) |
| 4 | Evaluation E1–E3; error analysis |
| 5 | Pepper socket integration; Wizard pilot protocol |
| 6 | Pilot (E4); collect user & operator feedback |
| 7 | Draft short paper (4 pages) \+ internal demo |
| 8 | Revisions → submit to *HRI 2026 Late-Breaking* |

---

### **8 Risks & Mitigation**

| Risk | Mitigation |
| :---- | :---- |
| Label sparsity (few positives) | Focal loss; up-sampling; threshold calibration |
| Pepper vision noise | Fall back to text-only at runtime if face unseen |
| Generalisation drop | Include DailyDialog test; plan future data collection |

---

### **9 Resources Needed**

* **Compute** – 1 × A100 (training); Pepper Jetson-NX (inference)  
* **Software** – HuggingFace, PEFT-LoRA, ROS bridge  
* **Personnel** – 1 MSc intern (8 weeks), 10 h/week mentor time

---

### **10 Alignment with Chetouani Lab Road-Map**

* Builds directly on **User-VLM 360°** bias-aware perception.  
* Advances lab theme of **anticipatory, trust-aware HRI** (ANITA project).  
* Provides a **public, reproducible benchmark** valuable to the wider ERC community.

---

### **References**

Ang et al. 2002\. *Prosody-Based Automatic Detection of Annoyance and Frustration in Human-Computer Dialog.* ICSLP. ([sri.com](https://www.sri.com/wp-content/uploads/2021/12/prosody-based_automatic_detection_of_annoyance_and_frustr.pdf?utm_source=chatgpt.com)) Hernandez Caralt et al. 2025\. *“Stupid robot, I want to speak to a human\!” User Frustration Detection in Task-Oriented Dialog Systems.* COLING-Industry. ([aclanthology.org](https://aclanthology.org/2025.coling-industry.23.pdf?utm_source=chatgpt.com)) (Additional references will be added in the full draft.)

---

**Contact:** Omar Jamal Hammad – [omarjh@kfupm.edu.sa](mailto:omarjh@kfupm.edu.sa) Dr. Mohamed Chetouani – ISIR, Sorbonne Université  

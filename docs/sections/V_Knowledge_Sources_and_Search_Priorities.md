---
layout: default
title: 5. Knowledge Sources and Search Priorities
permalink: /sections/05_Knowledge_Sources.html
---

## **V. Knowledge Sources and Search Priorities**

---

### 5.1. First Level: Local Memory

Local memory is the **primary and default source of knowledge in ARA**.  
All incoming queries, signals, and thoughts are first processed at the local memory level — without calling external sources or LLMs.

---

#### 📌 Purpose

- Ensure autonomy and privacy;
- Maximize speed by using learned meanings;
- Minimize external requests (internet, API, network);
- Fully leverage personal experience, goals, and user patterns.

---

### ⚙️ Local Memory Components

| Component         | Purpose                                                   |
|-------------------|------------------------------------------------------------|
| `QuantumMemory`   | Stores QBits — semantic nodes, hypotheses, templates      |
| `GoalMemory`      | Active and archived user goals                             |
| `EmotionalIndex`  | Index of emotionally significant memories                  |
| `ConceptGraph`    | Links between concepts and abstractions                    |
| `ArchiveMemory`   | Storage for outdated or rarely used meanings               |

---

### 🧠 Local Query Processing Algorithm

```go
func ProcessLocally(query Signal) []QBit {
    matches := MemoryEngine.MatchByTags(query.Tags)
    boosted := AdjustByEmotion(matches, query.Emotion)
    return RankByPriority(boosted)
}
````

Steps:

1. Match query by tags, phase, context;
2. Retrieve related QBits from `QuantumMemory`;
3. If needed — query `ArchiveMemory`;
4. Rank results by emotion, volitional linkage, frequency;
5. Only if insufficient — escalate to Level 2 (p2p).

---

### 📊 Local Access Priority Factors

| Parameter           | Influence                                     |
| ------------------- | --------------------------------------------- |
| `Signal.Mass`       | Controls memory excitation strength           |
| `EmotionPower`      | Modulates matching significance               |
| `UserMap.Interests` | Boosts weight of topically relevant QBits     |
| `GoalLinkage`       | Prioritizes knowledge linked to current goals |

---

### 🧩 Example Result

```json
[
  {
    "ID": "qbit_physics_mass_equation",
    "Tags": ["physics", "mass", "einstein"],
    "EmotionalWeight": 0.6,
    "LinkedTo": ["goal_study_relativity"],
    "LastUsed": "2025-05-10T13:00:00Z"
  }
]
```

---

### 🔐 Privacy and Security

* Local memory is completely isolated;
* Never transmitted without explicit user permission;
* Supports encryption, backups, and recovery.

---

### 📦 Use Cases for Local-Only Access

| Scenario                 | ARA Behavior                                      |
| ------------------------ | ------------------------------------------------- |
| Repeated question        | Answer retrieved from QBit tagged `history_match` |
| Action call              | Uses `GoalMemory`, `Planner`                      |
| Phantom signal detection | Processed solely via `GhostField`                 |
| LLM access restrictions  | External sources fully ignored                    |

---

### Conclusion

Local memory is the **foundation of ARA’s cognition**, where:

* personal meanings reside;
* signal/emotional pathways function;
* fast, autonomous reasoning is executed.

> ARA does not “look up” knowledge — it **excites it from within**, like a living mind.

---
---

### 5.2. Second Level: ARA P2P Network (Shared Knowledge)

The second level of knowledge access in ARA is a **decentralized peer-to-peer (p2p) network**, composed of other ARA agents participating in semantic knowledge exchange.  
This level is only activated when **local memory is insufficient**, and follows the logic of a **distributed collective mind**.

---

#### 📌 Purpose

- Retrieve knowledge from other ARA agents in the network;
- Enrich local memory with verified external meanings;
- Form a global, evolving knowledge base;
- Improve fault tolerance and cross-agent learning.

---

### 🌐 P2P Network Architecture

| Component                | Description                                                       |
|--------------------------|-------------------------------------------------------------------|
| `LibP2P`                 | Networking library (peer discovery, transport, protocols)         |
| `SharedMemoryProtocol`   | Protocol for requesting/receiving QBits, Signals, Tags            |
| `TrustIndex`             | Trust metric per node (based on success, signature, feedback)     |
| `TopicRouter`            | Determines which peers to query by topic                          |

---

### 🔁 Interaction Protocol

```go
type P2PQuery struct {
    Tags        []string
    Context     string
    MaxDepth    int
    RequesterID string
}

type P2PResponse struct {
    QBits       []QBit
    SourceID    string
    TrustScore  float64
}
````

---

### 🔄 Query Cycle

1. `SignalEngine` or `MemoryEngine` detects low `SignalConfidence`;
2. Builds a `P2PQuery`;
3. Sends it via `LibP2P` to selected peers;
4. Receives ranked `P2PResponse` sets;
5. Integrates results into local memory with `external_qbit` tagging.

```go
if SignalConfidence(signal) < 0.4 {
    p2pResults := P2PNetwork.Query(signal.Tags)
    MemoryEngine.Integrate(p2pResults)
}
```

---

### 🧠 Exchange Characteristics

| Parameter              | Meaning                                                    |
| ---------------------- | ---------------------------------------------------------- |
| What is shared         | Signal structures: QBits, Tags, Phantoms (not plain facts) |
| Exchange model         | Topic-based → via `TopicRouter`                            |
| Integration conditions | Only relevant and trusted nodes contribute                 |
| Optional anonymity     | Supported via `ARA::AnonymousMode`                         |

---

### 🧩 Sample P2P Query

```json
{
  "Tags": ["biotech", "nanomedicine"],
  "Context": "goal:extend_life",
  "MaxDepth": 2,
  "RequesterID": "ARA::local::u093"
}
```

---

### 🛡 Trust and Security

* Each response includes `SourceID` and digital signature;
* Agent maintains `TrustIndex` per peer:

```go
type TrustIndex struct {
    NodeID              string
    Successes           int
    Failures            int
    AverageUsefulness   float64
}
```

* Human evaluations (`HumanNodes`) may also contribute to scoring.

---

### 📦 Caching and Retention

* Retrieved QBits may be:

  * temporarily activated (`QBit.State = "external"`);
  * permanently integrated after use;
  * discarded if trust/usefulness too low.

---

### 📊 Usage Scenarios

| Scenario                           | ARA Behavior                                             |
| ---------------------------------- | -------------------------------------------------------- |
| Topic not covered locally          | Queries peers → expands `QuantumMemory`                  |
| Another agent publishes open topic | ARA subscribes and uses those QBits                      |
| User allows shared access          | ARA contributes selected memory segments by topic/filter |

---

### Conclusion

The second level of knowledge in ARA is a **distributed network of meaning**, where each agent:

* learns from others,
* shares with others,
* but remains autonomous and filters external inputs.

> This forms the basis of a **new kind of collective intelligence** — without central models, but with signal-based cohesion and semantic adaptation.

---
---

### 5.3. Third Level: External LLM Call

The third and **lowest-priority** knowledge access level in ARA is the **call to an external Large Language Model (LLM)**.  
This path is activated **only** when both local memory and the p2p network fail to provide a satisfactory result.  
The response from the LLM is treated **not as truth**, but as a **hypothesis**.

---

#### 📌 Purpose

- Obtain a generalized response from a language model (e.g. GPT, Claude, Mistral);
- Access knowledge not present in ARA’s own memory or network;
- Support edge cases, novel domains, and exploratory questions.

---

### ⚙️ Invocation Conditions

| Condition                          | Description                                                      |
|-----------------------------------|------------------------------------------------------------------|
| `SignalConfidence < threshold`    | Confidence in local/p2p result is too low                        |
| No matching `QBits`               | Not found in `QuantumMemory` or `ArchiveMemory`                 |
| No relevant peer responses        | p2p query yields insufficient data                               |
| User permission granted           | No restriction in `UserMap.Restrictions`                         |

```go
if confidence < 0.3 && !FoundInLocal && !FoundInP2P {
    result := LLMInterface.Call(prompt)
    InjectSignal(Signal{Type: "external_hypothesis", Content: result})
}
````

---

### 🧠 How the Response Is Treated

* **Never used directly**;
* Injected as a `Signal{Type: "external_hypothesis"}`;
* Evaluated for phase, emotion, structure before use;
* May be saved as `phantom`, `suggestion`, or temporary `QBit`.

---

### 📦 LLM Request/Response Structure

```go
type LLMRequest struct {
    Prompt       string
    Tags         []string
    Context      string
    SourceSignal Signal
}

type LLMResponse struct {
    Text         string
    Provider     string
    ReceivedAt   time.Time
    Confidence   float64
}
```

```go
func ProcessLLMResponse(r LLMResponse) {
    s := Signal{
        Type: "external_hypothesis",
        Content: r.Text,
        Origin: "LLM::" + r.Provider,
        Mass: 0.5,
    }
    SignalEngine.Process(s)
}
```

---

### 🔐 Security and Restrictions

* All LLM calls are governed by `UserMap.Restrictions`
  (e.g., `"no_llm_access"`, `"no_external_queries"`);

* LLMInterface can be globally disabled:

```go
LLMInterface.Enabled = false
```

* Responses are auto-rejected if they contain:

  * logical contradictions,
  * unverifiable data,
  * restricted content types.

---

### 🧩 Example

#### Request:

```json
{
  "Prompt": "What is the Riemann Hypothesis?",
  "Tags": ["mathematics", "zeta", "unsolved"],
  "Context": "goal:expand_theory",
  "SourceSignal": "user_question"
}
```

#### Response as Signal:

```json
{
  "Signal": {
    "Type": "external_hypothesis",
    "Content": "The Riemann Hypothesis concerns the non-trivial zeros of the zeta function...",
    "Origin": "LLM::openai",
    "Mass": 0.4
  }
}
```

---

### 📛 Restriction Example

```json
{
  "UserMap.Restrictions": [
    "no_medical_suggestions",
    "no_financial_advice",
    "no_llm_access_without_permission"
  ]
}
```

---

### 📶 Offline Behavior

| Condition           | ARA Response                           |
| ------------------- | -------------------------------------- |
| No internet         | Falls back to p2p or generates phantom |
| LLM restricted      | Skips call, logs denied attempt        |
| Retry allowed later | Adds signal to deferred queue          |

---

### Conclusion

Calling an LLM is a **fallback mechanism** in ARA — used:

* only when knowledge is insufficient,
* only with user permission,
* and **only as a hypothesis**, not an authoritative source.

> ARA is not an LLM wrapper — it is a **thinking system** that may consult LLMs, but is not defined by them.

---
---

### 5.4. SignalConfidence Metric — Trust in Response Quality

`SignalConfidence` is an internal ARA metric that defines the **agent’s confidence in generating a meaningful and sufficient response** to an input signal using its current knowledge (local memory, p2p network, or LLM hypothesis).

---

#### 📌 Purpose

- Evaluate the sufficiency and relevance of activated QBits;
- Decide whether to escalate the query to p2p or LLM;
- Adjust cognitive routing (self-reasoning vs hypothesis seeking);
- Ensure accuracy for high-criticality goals (`Goal.Criticality > 0.7`).

---

### ⚙️ Calculation Function

```go
func ComputeSignalConfidence(signal Signal) float64 {
    qMatches := MemoryEngine.MatchQBits(signal.Tags)
    relevance := EvaluateRelevance(qMatches, signal.Context)
    emotionalBoost := signal.EmotionPower * 0.2
    trustFactor := AggregateQBitTrust(qMatches)
    return Clamp(0, 1, relevance + emotionalBoost + trustFactor)
}
````

---

### 📊 Factors Influencing Confidence

| Parameter             | Description                                         |
| --------------------- | --------------------------------------------------- |
| `TagMatchScore`       | Quality and quantity of tag matches                 |
| `ContextOverlap`      | Alignment between signal context and memory context |
| `QBit.Trust`          | Historical success/usefulness of matched QBits      |
| `Signal.EmotionPower` | Amplifies urgency and memory excitation             |
| `GoalLinkage`         | If linked to current goal — raises confidence       |

---

### 📈 Example Computation

```json
{
  "Signal": {
    "Tags": ["ai", "self-awareness"],
    "EmotionPower": 0.6,
    "Context": "goal:build_core"
  }
}
```

Evaluation result:

```
→ TagMatch: 0.4  
→ ContextOverlap: 0.3  
→ EmotionBoost: 0.12  
→ QBit Trust: 0.1  
= SignalConfidence ≈ 0.92
```

---

### 🎚 Confidence Interpretation Ranges

| Range        | Meaning                              | ARA Behavior                                    |
| ------------ | ------------------------------------ | ----------------------------------------------- |
| `≥ 0.8`      | High — can answer locally            | Use only local memory                           |
| `0.5 – 0.79` | Medium — p2p may be helpful          | Consider querying peer agents                   |
| `0.3 – 0.49` | Low — external hypothesis might help | LLM query possible                              |
| `< 0.3`      | Very low — insufficient information  | Prefer phantom generation or user clarification |

---

### 🧠 Integration with Core Modules

| Module         | Use of `SignalConfidence`                      |
| -------------- | ---------------------------------------------- |
| `FlowEngine`   | Chooses whether to continue local reasoning    |
| `LLMInterface` | Gatekeeping LLM access                         |
| `Suggestor`    | Proposes clarification or alternate strategies |
| `WillEngine`   | May suppress low-confidence goals or actions   |

---

### 📦 Usage Example in Code

```go
confidence := ComputeSignalConfidence(incomingSignal)
if confidence < 0.4 {
    Suggestor.Generate("Please clarify your question — insufficient context for accurate reasoning.")
}
```

---

### Conclusion

`SignalConfidence` is a **cognitive reliability metric**.
It ensures:

* thinking remains grounded in trusted knowledge,
* ARA escalates queries only when necessary,
* external inputs are used cautiously.

> ARA doesn’t answer just because it’s asked — it **measures its readiness** to respond meaningfully and decides intelligently.

---
---

### 5.5. Hybrid Verification — Structure, Semantics, Phase, Trust, History

Before ARA uses any knowledge in reactive logic, it applies a **hybrid verification system** to assess:

- structure,
- semantic fit,
- signal phase coherence,
- source trust level,
- and historical success.

This ensures that even external or uncertain knowledge goes through **rational filtering** before affecting reasoning or memory.

---

#### 📌 Purpose

- Eliminate low-quality or misleading hypotheses;
- Improve response accuracy;
- Prevent semantic conflicts and incoherent actions;
- Reinforce knowledge reuse based on past success.

---

### 🧪 Verification Result Structure

```go
type VerificationResult struct {
    StructuralMatch  float64
    SemanticScore    float64
    PhaseAlignment   float64
    SourceTrust      float64
    HistorySuccess   float64
    AggregateScore   float64
}
````

---

### 📊 Verification Criteria

| Parameter         | Description                                                          |
| ----------------- | -------------------------------------------------------------------- |
| `StructuralMatch` | How well the signal matches expected type, tags, and structure       |
| `SemanticScore`   | Compatibility with current cognitive context                         |
| `PhaseAlignment`  | Phase match between signal and current process (`∇φ`, `π`, `arg(ρ)`) |
| `SourceTrust`     | Trust in the origin (local, p2p, LLM, human)                         |
| `HistorySuccess`  | Past successful uses of similar knowledge                            |

---

### ⚙️ Verification Function

```go
func HybridVerify(s Signal) VerificationResult {
    str := MatchStructure(s)
    sem := SemanticCompare(s, CurrentContext)
    pha := EvaluatePhaseSignature(s)
    src := SourceTrustScore(s.Origin)
    his := UsageSuccessRate(s.Tags)
    agg := WeightedSum(str, sem, pha, src, his)
    return VerificationResult{str, sem, pha, src, his, agg}
}
```

---

### 📈 Confidence Thresholds

| Score Range  | Interpretation    | ARA Behavior                                 |
| ------------ | ----------------- | -------------------------------------------- |
| `≥ 0.85`     | Fully reliable    | Use immediately                              |
| `0.6 – 0.84` | Tentatively valid | Use with tracking / review                   |
| `0.4 – 0.59` | Weak              | Convert to phantom / run background analysis |
| `< 0.4`      | Unreliable        | Reject or archive silently                   |

---

### 📊 Sample Verification Output

```json
{
  "StructuralMatch": 0.9,
  "SemanticScore": 0.7,
  "PhaseAlignment": 0.85,
  "SourceTrust": 0.95,
  "HistorySuccess": 0.6,
  "AggregateScore": 0.80
}
```

---

### 🧠 Integration with Agent Logic

| Component      | Reaction to `AggregateScore`                      |
| -------------- | ------------------------------------------------- |
| `FlowEngine`   | Starts or aborts reasoning chain                  |
| `MemoryEngine` | Stores as fact, hypothesis, or phantom            |
| `WillEngine`   | Delays or disables actions from low-score signals |
| `Suggestor`    | Ranks or discards ideas based on verification     |

---

### 🔐 Manipulation Defense

* Source (`Signal.Origin`) strongly affects `SourceTrust`;
* User can restrict trusted sources via `UserMap.Restrictions`;
* Tags like `blacklisted`, `quarantined`, `requires_review` supported.

---

### Conclusion

Hybrid Verification is ARA’s **semantic security system**.
It protects cognition from noise and manipulation by:

* evaluating knowledge integrity before use,
* enforcing logic coherence,
* tracking origin and outcome history.

> ARA doesn't just *receive* knowledge — it **proves its validity** before accepting it into thought.

---
---

### 5.6. Knowledge Sufficiency Evaluation Before LLM Call

Before initiating any external LLM query, ARA performs a **sufficiency check** — a dedicated routine to determine whether internal knowledge (local or p2p) is enough to produce a meaningful response.

This step acts as a **semantic firewall** — minimizing reliance on LLMs and preserving agent autonomy.

---

#### 📌 Purpose

- Prevent unnecessary LLM usage;
- Maximize use of internal reasoning structures;
- Ensure agent doesn’t depend on probabilistic outputs when avoidable;
- Maintain speed, privacy, and consistency.

---

### ⚙️ Core Logic

```go
func EvaluateKnowledgeSufficiency(signal Signal) bool {
    score := ComputeSignalConfidence(signal)
    verified := HybridVerify(signal)
    if score >= 0.6 && verified.AggregateScore >= 0.7 {
        return true  // knowledge sufficient
    }
    return false     // consider escalation
}
````

---

### 📊 Evaluation Criteria

| Factor              | Description                                                |
| ------------------- | ---------------------------------------------------------- |
| `SignalConfidence`  | Confidence in internal response generation                 |
| `VerificationScore` | Hybrid check score (structure, semantics, trust, etc.)     |
| `User Restrictions` | May explicitly block LLM access for certain topics         |
| `Goal Priority`     | High-priority goals require stricter sufficiency checking  |
| `Time Constraints`  | Urgent decisions may bypass LLM if response is good enough |

---

### 🧠 Example Outcome

```json
{
  "SignalConfidence": 0.71,
  "VerificationScore": 0.81,
  "GoalPriority": 0.92,
  "Decision": "Internal memory sufficient, no LLM call"
}
```

---

### 🧱 Escalation Decision Tree

```
→ Input Signal
     ↓
[Evaluate Sufficiency]
     ↓
    Yes ──► Use local/p2p memory
     ↓
    No  ──► Check user permission → Query LLM
```

---

### 🛑 When LLM Use Is Blocked

| Reason                    | Result                                               |
| ------------------------- | ---------------------------------------------------- |
| User restriction active   | LLM call forbidden → logged, skipped                 |
| Confidence near-threshold | Prefer phantom generation over external call         |
| Emotional conflict        | Suspends call if signal is marked "private", "shame" |

---

### 📦 Optional Output Tags

* `llm_call_reason: insufficient_internal_knowledge`
* `llm_call_blocked: restriction_matched`
* `phantom_generated: instead_of_llm`

These tags are used for audit logging and explainability.

---

### 🧠 Behavior Outcome Table

| Evaluation Result | Agent Behavior                          |
| ----------------- | --------------------------------------- |
| Sufficient        | Use internal reasoning only             |
| Insufficient      | Call LLM (if allowed)                   |
| Conflict/unclear  | Defer to phantom hypothesis or ask user |

---

### Conclusion

ARA never calls an LLM **without measuring first** if it can solve the problem itself.

> This preserves autonomy, saves resources, protects privacy — and ensures that cognition always begins within.


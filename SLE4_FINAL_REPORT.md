# SLE-4: Final Viva & Architecture Decision Record (ADR)

**Course:** 02AML204 – Introduction to Artificial Intelligence  
**PRN:** 25UAM059  
**Name:** Sanskruti Sandeep Danole  
**Division:** A  
**Date:** 10 October 2026  
**GitHub Repository:** SLE4-NEW

## PART A: Architecture Decision Record (ADR)

### Title: Use of a Separate Search Engine Container for BFS/DFS

**Status:** Accepted  
**Date:** 10 October 2026

### 1. Context

The SLE-2 project implements BFS and DFS on the same 20-node graph from A to T. The experiment repeats each search 10,000 times and records path, nodes expanded, and timing. For SLE-3, the same system was represented using the C4 model. The architecture separates input/control, graph data, search engine, result/trace, and Python runtime responsibilities.

### 2. Decision

The design uses a dedicated Search Engine as the main container for BFS and DFS traversal logic. At Component level, the Search Engine is decomposed into traversal selection, frontier management, visited tracking, target checking, and traversal output/path handling.

### 3. Alternatives Considered

- Keep all input, graph, search, and output logic in one module.
- Create separate top-level containers for BFS and DFS.
- Expand every container at Component level instead of focusing on the Search Engine.

### 4. Rationale / Justification

The SLE-2 experiment uses a 20-node graph and 10,000 benchmark runs for both BFS and DFS, so the search logic is the core part being measured. BFS uses a queue while DFS uses stack-based traversal, but both solve the same graph-search problem. SLE-3 therefore places both algorithms inside one Search Engine container. The C4 design separates Input/Control, Graph Data, Search Engine, Result/Trace, and Python Runtime. The Component view further separates traversal selection, visited tracking, frontier management, target checking, and output. This makes the architecture easier to explain and keeps responsibilities clear. It also connects directly to the actual bfs(), dfs(), benchmark(), graph data, and timing responsibilities in the implementation.

### 5. Consequences

**Positive:**
- Keeps the main search responsibility in one clear architectural location.
- Makes BFS and DFS easier to compare because they use the same Search Engine boundary.
- Supports clear C4 Context, Container, Component, and Code-level explanations.
- Improves readability and makes future changes to search logic easier to isolate.

**Negative / Trade-offs:**
- The Search Engine can become larger if many more search algorithms are added.
- A shared container requires careful separation between BFS-specific and DFS-specific frontier behaviour.

### 6. References

- SLE-1: ai-workflow-assistant
- SLE-2: IAI_SLE2
- SLE-3: SLE-3-C4-model

## PART B: Short Summary of My SLE Journey

SLE-1 established the BFS/DFS search project and its AI contribution documentation. SLE-2 compared BFS and DFS empirically on a 20-node graph using repeated 10,000-run benchmarks. SLE-3 converted the same system into a full C4 architecture with Context, Container, Component, and Code views. SLE-4 records the decision to keep BFS and DFS inside a dedicated Search Engine container and explains why that design is appropriate.

## PART C: AI Contribution Note

**AI tool used: ChatGPT.** AI assistance was used for organizing the ADR, connecting the previous SLE work, structuring the viva notes, and preparing documentation. The student selected and reviewed the BFS/DFS project, provided the previous SLE work, and is responsible for understanding and defending the decision in the viva.

## AI CONTRIBUTION

**AI Tool Used:** ChatGPT

**What AI helped with:** AI helped organize the SLE-4 ADR according to the required structure, connect SLE-1, SLE-2 and SLE-3 work, improve the explanation of the Search Engine container decision, and prepare concise viva points.

**My Contribution:** I selected the BFS/DFS architecture decision, provided and reviewed the previous SLE work, verified the final content, and am responsible for understanding and defending the ADR and AI-assisted work during the viva.

**Ownership Statement:** AI was used as an assistance tool for documentation and organization. The final architectural decision, project context, review, and viva defense are my responsibility.

## PART D: Viva Preparation Notes

- Why did you choose a separate Search Engine container?
- What alternatives did you consider and why did you reject them?
- What did SLE-2 profiling show?
- Explain your SLE-3 Container and Component design briefly.
- What did AI help with and what did you do yourself?

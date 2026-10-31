# GNN-Based Traffic Engineering for Software-Defined Networks

Research project exploring how graph neural network (GNN) traffic-engineering policies could improve routing in a software-defined network (SDN). The work combines a small Mininet/Ryu routing baseline with an initial, separate MAGNNETO-TE training pilot.

> **Research status:** Work in progress. The current controller uses shortest-hop routing. MAGNNETO-TE is not integrated with the Mininet network, and no performance improvement has yet been established.

## Research direction

The provisional research question is:

> On a controlled SDN testbed, how does a GNN-based traffic-engineering policy compare with shortest-hop routing in congestion, network performance, and decision overhead under changing traffic demands?

This question is subject to literature review and feasibility testing. The immediate goal is a fair, reproducible comparison, not a claim that a GNN is already better.

## Current system

| Component | Current state |
| --- | --- |
| **Mininet topology** | Six switches, six hosts, and eight inter-switch links with configured bandwidth and delay, providing multiple routes. |
| **Ryu controller** | Discovers links, learns host locations, uses a spanning tree for loop-free broadcast forwarding, and installs destination-based OpenFlow 1.3 rules. |
| **Routing baseline** | Breadth-first search selects an unweighted shortest-hop path. The configured link bandwidth and delay are not yet used in route selection. |
| **GNN training pilot** | A MAGNNETO-TE pilot completed separately from the Mininet/Ryu testbed and saved actor and critic checkpoints. |
| **Model integration and evaluation** | Not yet completed. There is no verified held-out comparison against the shortest-hop baseline. |

The training pilot confirms that the training workflow can run; it does not demonstrate better routing. The pilot used a different network/data setup from the six-switch Mininet mesh, so compatibility and transfer must be established before comparing results.

## Planned research workflow

1. **Reproduce the baseline.** Run the six-switch topology and record connectivity, routes, flow rules, and baseline network measurements.
2. **Fix the experiment design.** Define traffic scenarios, data provenance, training/validation/test splits, and a primary objective. Keep training and held-out traffic separate.
3. **Evaluate offline.** Compare the selected policy with shortest-hop routing on the same topology and traffic. Use maximum link utilization as a candidate congestion metric; measure throughput, delay, packet loss, and decision time separately.
4. **Check compatibility.** Map the model's graph, traffic inputs, and actions to the Mininet topology before attempting controller integration.
5. **Integrate and validate.** If the offline comparison is sound, adapt the policy for Ryu and verify the resulting OpenFlow paths in Mininet.
6. **Write up the evidence.** Report the method, baselines, data, limitations, and results, including negative or inconclusive results. Refine the research question and any novelty claim against the literature.

## Repository contents

This initial repository version contains **only this README**. The local project also includes topology/controller drafts, demonstration notes, reference material, and a third-party model checkout; those files are not part of this upload. Code, datasets, checkpoints, and experiment results will be added only after they are reviewed for reproducibility, provenance, and redistribution rights.

## Related work

- [MAGNNETO](https://arxiv.org/abs/2303.18157) — a multi-agent reinforcement-learning and GNN approach for traffic engineering that optimizes OSPF link weights. This is the model used for the initial training pilot; adapting its inputs and actions to an OpenFlow/Ryu mesh remains future work. See also the [authors' implementation](https://github.com/BNN-UPC/MAGNNETO-TE).
- [RouteNet-Fermi](https://doi.org/10.1109/TNET.2023.3269983) — a GNN-based network-performance model for estimating metrics such as delay, jitter, and packet loss. It addresses performance prediction, a different task from selecting traffic-engineering actions.

These works are starting points for the literature review, not evidence of this project's novelty.

## Acknowledgements

The MAGNNETO-TE codebase and associated research are third-party work by their respective authors. This project does not claim authorship of that model. Any future redistribution of third-party code or data will follow the original licenses and terms.

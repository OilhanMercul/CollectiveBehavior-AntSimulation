# Pheromone-driven trail formation in a physics-based 3D ant simulator

We extend the Position-Based Dynamics (PBD) ant swarm simulation of Loges & Weiss (2025) by introducing a pheromone field and the experimentally measured steering behavior of Argentine ants described by Perna et al. (2012). Our goal is to investigate how pheromone-based communication produces collective trails and how physical interactions, such as collisions and crowding, influence their formation.

## Authors :
| Name | GitHub |
|------|--------|
| Moira Grozdanić | [@moiragrozdanicc](https://github.com/moiragrozdanicc) |
| Raphaël Letourneur | [@raphltr](https://github.com/raphltr) |
| Oïlhan Mercul | [@OilhanMercul](https://github.com/OilhanMercul) |
| Ljubiša Milovanović | [@Ljubisa-Milovanovic](https://github.com/Ljubisa-Milovanovic) |

## Starting Point :

Our starting point is the following article on ant swarm aggregation dynamics:

> Loges, M., & Weiss, T. (2025). *Simulating Ant Swarm Aggregations Dynamics*. Proceedings of the ACM on Computer Graphics and Interactive Techniques, 8(4), Article 55, 1–16. https://doi.org/10.1145/3747868

This article includes a C++/Raylib codebase designed to simulate 3D ant aggregations using Position-Based Dynamics (PBD). The work focuses on a fluid dynamics approach, reproducing collective behaviors in specific physical contexts to allow direct comparison between high-density ant swarms and real viscoelastic fluids.
To extend the simulation, we use the research of Perna et al. (2012), which experimentally describes how Argentine ants respond to pheromone concentrations. Ants compare pheromone levels on their left and right and adjust their direction accordingly.

## Plan :

Our main objectives are:

- Implement a pheromone field with deposition and evaporation.
- Integrate the pheromone-based steering behavior described by Perna et al. (2012).
- Simulate trail formation in an open arena.
- Validate the simulated behavior against the experimental results of Perna et al.
- Investigate how ant density and physical collisions influence trail formation and stability.
- Experiments and evaluation

We plan to conduct open-arena experiments to observe trail formation and crowding experiments to investigate how ant density and physical interactions affect trail stability.

If time allows, we will also reproduce a binary-bridge experiment to study path selection between two branches.

Results will be evaluated using ant turning angles, trail formation over time, trail stability, tortuosity, loop formation and the effects of crowding. Experiments will use fixed random seeds to ensure reproducibility.

## Milestone :

[First Report – 13/11/2026]([📄 Read PDF](CollectiveBehavior-AntSimulation-main\reports\report_1\Pheromone_Driven_Trail_Formation_in_a_Physics_Based_3D_Ant_Simulator__Literature_Review_and_Implementation_Strategy.pdf) | [📂 LaTeX Source](reports/report_1/report_1.tex))
- Understand and reproduce the original simulator.
- Review relevant literature on pheromone-based behavior and trail formation.
- Finalize the implementation approach and experimental plan.

[Second Report – 11/12/2026](https://github.com/OilhanMercul/CollectiveBehavior-AntSimulation/milestone/2)
- Implement a pheromone field with deposition and evaporation.
- Integrate the pheromone-based steering behavior.
- Demonstrate initial trail formation in an open arena.

[Final Report – 08/01/2027](https://github.com/OilhanMercul/CollectiveBehavior-AntSimulation/milestone/3)
- Complete trail formation experiments.
- Validate simulated ant behavior against Perna et al.
- Investigate the effects of ant density and physical collisions on trail formation.
Analyze and present the results.

## 🧭 Documentation

- 🚀 **[SETUP.md](SETUP.md)** — **Complete Setup & Launch Guide** (Compiling on Windows/macOS, simulation controls, scene catalogue, parameter tuning guide, recording data, troubleshooting).
- 
## 📚 References

### Core References
- **Loges, M., & Weiss, T. (2025).** *Simulating Ant Swarm Aggregations Dynamics*. Proceedings of the ACM on Computer Graphics and Interactive Techniques, 8(4), Article 55, 1–16.  
  [https://doi.org/10.1145/3747868](https://doi.org/10.1145/3747868)
- **Perna, A. et al. (2012).** *Individual rules for trail pattern formation in Argentine ants*. *PLOS Computational Biology*, 8(7), e1002592.  
  [https://doi.org/10.1371/journal.pcbi.1002592](https://doi.org/10.1371/journal.pcbi.1002592)

---

### Related Work & Analysis

#### Pheromone-Based Behavior and Trail Formation

- **Hartman, S., Ryan, S. D., & Karamched, B. R. (2024).**  
  *Walk this way: modeling foraging ant dynamics in multiple food source environments*. *Journal of Mathematical Biology*, 89(3), Article 41.  
  [https://doi.org/10.1007/s00285-024-02136-2](https://doi.org/10.1007/s00285-024-02136-2)  
  > *Analysis:* This model relies on a discrete lattice domain with probabilistic position-jump processes, making it spatially incompatible with a continuous 3D PBD framework. Furthermore, it focuses on macro-level multi-source resource allocation (winner-take-all dynamics) rather than low-level, antenna-guided turning kinematics.

- **Boissard, E., Degond, P., & Motsch, S. (2013).**  
  *Trail formation based on directed pheromone deposition*. *Journal of Mathematical Biology*, 66(6), 1267–1301.  
  [https://doi.org/10.1007/s00285-012-0529-y](https://doi.org/10.1007/s00285-012-0529-y) | [arXiv:1108.3495](https://arxiv.org/abs/1108.3495)  
  > *Analysis:* Pheromones are represented as discrete directed vector particles $(\mathbf{x}_p, \boldsymbol{\omega}_p)$, creating a memory-heavy data structure to track and evaporate in 3D. Additionally, its interaction mechanism via stochastic Poisson alignment jumps interfaces less naturally with a continuous PBD velocity planner than a scalar field.

#### Traffic Flow and Crowding in Ant Swarms

- **Dobramysl, U., Garnier, S., Poissonnier, L.-A., Dussutour, A., & Bruna, M. (2025).**  
  *Argentine ants regulate traffic flow with stopped individuals*.  
  [HAL Id: hal-05346293](https://hal.science/hal-05346293)  
  > *Analysis:* Relevant to our investigation of physical crowding and collision dynamics, highlighting how stopped or slower ants regulate overall traffic and affect trail throughput.

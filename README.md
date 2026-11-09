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

[First Report – 13/11/2026](https://github.com/OilhanMercul/CollectiveBehavior-AntSimulation/milestone/1)
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

## Links and references : 
- [Loges, M., & Weiss, T. (2025). *Simulating Ant Swarm Aggregations Dynamics*](https://doi.org/10.1145/3747868)
- [Perna, A. et al. (2012). Individual rules for trail pattern formation in Argentine ants](https://doi.org/10.1371/journal.pcbi.1002592)


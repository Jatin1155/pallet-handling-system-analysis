# Pallet Handling System – Capacity Analysis and DOSIMIS-3 Simulation

**Master’s programme:** Logistics and Supply Chain Management  
**Institution:** Technische Hochschule Wildau (TH Wildau), Germany  
**Course case study:** *Simulation-based Analysis and Design of Materials Handling Systems*  
**Project:** Pallet Handling System – Part 1  
**Team:** Team 3

---

## Project overview

This project analyses the capacity and operating behaviour of an automated pallet-handling system connecting a warehouse, packaging, manufacturing and depalletising area.

The system contains multiple pallet flows that share conveyors, roller conveyors, turntables and two shuttle systems. Full pallets are transported to a depalletising workstation. Empty pallets are then collected, combined into stacks of nine and returned to the warehouse.

The central question is:

> **How much demand can the pallet-handling system process before shared resources become bottlenecks and queues begin to grow?**

The project combines manual capacity calculations with a DOSIMIS-3 simulation model. The manual analysis provides transparent theoretical estimates, while the simulation represents interactions such as shuttle priorities, FIFO call selection, empty movements, blocking and queue formation.

## Project status and next phase

**Overall project status: Ongoing**

### Part 1 – System analysis and capacity evaluation
The Part 1 work documented in this repository covers the system and material-flow analysis, manual capacity calculations, DOSIMIS-3 modelling, the mixed-load simulation experiments, bottleneck identification and interpretation of the results. The analysis indicates that SH1 is the most heavily utilised shared resource in the tested scenarios and that queues begin to grow as offered demand exceeds the system's handled throughput.

### Part 2 – Model optimisation
**Status: Planned / in progress – results not yet completed.**

The project will continue with Part 2, which will use the Part 1 model and findings as the baseline for optimisation. The aim is to investigate how the existing system can perform better without changing the system design or replacing its elements, in line with the case-study objective. The optimisation work may examine operating logic and control settings, shuttle task allocation and priorities, flow balancing, and avoidable waiting or empty movements where these can be tested in the model.

The optimised model will be evaluated against the Part 1 baseline using comparable demand scenarios and performance measures such as handled throughput, resource utilisation, queue lengths and lead times. The optimisation results and conclusions will be added to this repository after the Part 2 experiments have been completed and evaluated.

**Important:** The bottlenecks identified in Part 1 are findings from the current model and tested conditions. They are not presented as already solved. Part 2 is the follow-up work intended to test and assess possible improvements.

## Project origin and scope

This work is based on a case study provided as part of the TH Wildau Master’s course. The original case-study material defines the system layout, technical parameters, material flows, control rules and five project tasks.

The project work follows these main tasks:

1. **System analysis:** describe the system structure, material flows and control rules.
2. **Performance analysis:** calculate component and flow capacities, identify bottlenecks and estimate the system load limit.
3. **Simulation modelling:** develop and check a DOSIMIS-3 representation of the material-handling system.
4. **Simulation experiments:** run the mixed-flow system at different nominal load levels.
5. **Evaluation:** compare manual calculations with simulation results and draw conclusions about system performance.

The original assignment and a concise project brief with the system layout are included in the repository.

## System and material flows

The case study defines eight pallet flows:

| Flow | Route | Description |
|---|---|---|
| F1 | Warehouse → Packaging | Pallet supply to packaging |
| F2 | Warehouse → DEPAL | Warehouse pallet to depalletising |
| F3 | Packaging → DEPAL | Packaging pallet to depalletising |
| F4 | Packaging → Warehouse | Pallet return to warehouse |
| F5 | Empty-pallet stacks → Warehouse | Return of stacks containing nine empty pallets |
| F6 | Warehouse → Manufacturing | Pallet supply to manufacturing |
| F7 | Manufacturing → Warehouse | Pallet return to warehouse |
| F8 | Manufacturing → DEPAL | Manufacturing pallet to depalletising |

The model includes conveyors, roller conveyors, four turntables, two shuttles (SH1 and SH2), the DEPAL workstation and the empty-pallet stacking process.

## Methodology

### 1. Manual capacity analysis

The manual calculations use the technical data in the case study, including conveyor and shuttle speeds, equipment dimensions, turntable rotation time, manual handling times and the DEPAL process time.

The revised DEPAL cycle used in the manual analysis is:

- Depalletising process: **140 seconds**
- Transfer of the empty pallet to B_EPAL: **8.235 seconds**
- Total cycle: **148.235 seconds per pallet**
- Theoretical DEPAL capacity: **approximately 24.28 pallets/hour**

The manual analysis then evaluates individual flow capacities and the workload placed on shared resources, particularly SH1 and SH2.

### 2. DOSIMIS-3 simulation

A DOSIMIS-3 model was developed to represent the system layout, equipment, pallet routes and relevant control logic. The mixed-flow experiments considered four nominal load levels:

**55%, 60%, 65% and 100%.**

The experiments were evaluated using handled throughput, equipment utilisation, queue development and lead times.

### 3. Comparison and interpretation

Manual calculations and simulation results are compared to identify the main capacity constraints and explain differences between theoretical estimates and dynamic system behaviour.

The comparison is interpreted with care because the DOSIMIS experiments and the revised manual calculation do not use exactly the same internal DEPAL flow distribution. The model-version difference between some simulation runs is also documented in the technical report.

## Main simulation findings

The reported mixed-flow results are summarised below.

| Nominal load | Offered demand (pallets/h) | Handled throughput (pallets/h) | SH1 busy | SH2 busy | DEPAL busy |
|---:|---:|---:|---:|---:|---:|
| 55% | 69.9 | 70.3 | 85.1% | 55.4% | 54.0% |
| 60% | 76.3 | 76.6 | 93.0% | 60.8% | 57.1% |
| 65% | 82.6 | 78.4 | 96.1% | 62.5% | 58.7% |
| 100% | 127.2 | 76.9 | 95.1% | 63.8% | 63.3% |

**Key observations**

- Handled throughput increases from approximately 70.3 pallets/hour at 55% load to 76.6 pallets/hour at 60%.
- At 65% load, handled throughput increases only slightly to 78.4 pallets/hour, while the warehouse input queue begins to grow.
- At 100% load, offered demand is much higher than handled throughput and queues develop at the warehouse, packaging and manufacturing inputs.
- SH1 is the most heavily utilised shared resource in the reported mixed-load experiments.
- The simulation results indicate a throughput ceiling in the region of **76–78 pallets/hour** for the tested model and conditions.
- The simulation report identifies approximately **70 pallets/hour** as a more cautious operating level with some capacity reserve.

The figures describe the tested model and scenarios; they should not be interpreted as a universal capacity value for other system configurations.

## Manual calculation and simulation: interpretation

The revised manual calculation estimates the full-reference-load utilisation of SH1 at 112.1%, SH2 at 74.7% and DEPAL at approximately 100%. Partial-load manual estimates are obtained by proportional scaling.

The simulation represents dynamic effects that a static manual calculation cannot reproduce in full, including actual shuttle call sequences, priority rules, empty travel, blocking and queue formation.

**Important comparison limitation:** the four DOSIMIS mixed-load experiments were configured with the earlier Scenario D flow distribution based on a DEPAL rate of 21.5 pallets/hour. The revised manual calculation uses a DEPAL capacity of 24.28 pallets/hour and a revised internal flow distribution. Therefore, the utilisation comparison is indicative rather than a strict like-for-like validation. The technical report explains this difference and the related model-version limitation.

## Project files

| Folder / file | Contents |
|---|---|
| `01_Project_Brief/` | TH Wildau case-study brief, task summary and original system-layout drawings |
| `02_DOSIMIS_Model/` | ZIP package containing the DOSIMIS model and supporting files |
| `03_Simulation_Results/` | DOSIMIS-3 result/statistics files included with the project; filenames and scenario mapping should be checked against the corresponding run records |
| `04_Technical_Report/` | Detailed report covering manual calculations, model setup, simulation results, comparisons and conclusions |
| `05_Results_Graphs/` | Throughput and resource-utilisation comparison figures |

### DOSIMIS model package

The model package is supplied as a ZIP archive so that the model configuration and its supporting files remain together. The archive includes the DOSIMIS model (`.mfs`), backup and supporting drawing, picture, trace and result-related files.

The `.slg` files are also supplied separately to make the simulation statistics easier to locate. Their scenario mapping should only be stated where it has been verified against the corresponding run records.

To inspect or run the model, DOSIMIS-3 is required. The ability to open the model may depend on the installed software version and local configuration.

## Limitations and assumptions

The results should be read in the context of the following documented limitations:

- The manual partial-load utilisation values are proportional estimates based on the full-load manual workload calculation.
- The four mixed-load DOSIMIS experiments use an earlier DEPAL flow distribution than the revised manual calculation.
- The 55% and 100% experiments were run with an earlier chain-conveyor configuration; the 60% and 65% experiments used the later configuration.
- The explicit DEPAL sequencing condition described in the case study was not fully implemented in the model, as documented in the simulation report.
- The STRETCH process time was not specified in the case study and was modelled with zero additional process time.
- The results represent the tested model and run conditions. Further runs with identical revised input distributions and repeated random seeds would strengthen a like-for-like comparison.

These limitations are stated to make the modelling assumptions and scope of the conclusions transparent.

## Project documentation

- **Project brief:** summarises the original case-study objectives, five tasks, system boundaries, technical parameters and layout.
- **Technical report:** provides the detailed calculations, modelling approach, simulation results, comparison and conclusions.
- **Simulation result files:** provide the DOSIMIS statistics for the individual experiment runs.
- **DOSIMIS model archive:** provides the model and supporting files for inspection in DOSIMIS-3.

## Acknowledgement

The case-study scenario, system layout, technical parameters, material-flow definitions and task structure originate from the TH Wildau course material *Simulation-based Analysis and Design of Materials Handling Systems – Case Study: Pallet Handling System* (Autumn/Winter 2026/27).

The accompanying calculations, DOSIMIS-3 model work, experiments, analysis and report were developed as part of the student project. The repository should distinguish the work completed individually from work completed jointly by the project team.

---

**Keywords:** Intralogistics · Material Handling · Pallet Handling · Capacity Analysis · Bottleneck Analysis · Discrete-Event Simulation · DOSIMIS-3 · Throughput · Resource Utilisation · Warehouse Operations


## Planned Part 2 repository structure

When the optimisation work is carried out, its evidence can be added in a separate folder so that the original analysis remains traceable:

```text
06_Optimisation_Part_2/
├── Optimisation_Approach.md
├── Updated_DOSIMIS_Model/
├── Experiment_Settings/
├── Baseline_vs_Optimised_Results/
└── Conclusions_and_Recommendations.md
```

This folder is a proposed structure for future work; it does not indicate that the optimisation experiments or results are already complete.

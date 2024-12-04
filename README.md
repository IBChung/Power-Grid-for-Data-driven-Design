# Synthetic Power Grid Dataset for Data-driven Design
This repository contains datasets for power transmission network.
The datasets were created for the purpose of providing design engineers with realistic synthesize power grid for data-driven design of networks.
The size of the datasets were determined so that they are enough for deep-learning applications. However, it is not strictly limited to this purpose.

The publication corresponding to this repository contains an example case study on using a part of the datasets for generative design of transmission networks.

### Abstract of the paper
<Sub>Interdependent critical infrastructures are prone to be a target of disruptions from either natural disasters or deliberate attacks that can cause a great magnitude of negative consequences on the system. To
withstand and reduce the impacts of disruptive events, it is beneficial to consider them in the early stage of design to create a configuration that can maintain its performance as much as possible. However, due to the complexity of modern systems, it is difficult to optimize the large-scale system design with complicated constraints directly. To overcome this issue, it is advantageous to tackle the problem with a state-of-the-art data-driven approach. However, the problem arises due to the limited amount of data for power systems available to the public. Hence, synthesized power systems that resemble existing networks are collected and processed,
which can be utilized for implementing machine-learning models. The power system networks are represented as graphs with features holding information on the nodes and edges that relate to electrical components. Using the generated dataset, this research implements a generative approach based on Wasserstein GAN to create intelligent designs. Afterwards, performance measures are employed to induce the generation of a population with more appealing characteristics. To demonstrate the practicality of the dataset on data-driven design, it was applied to train the generative model for the 57-bus system. The results have shown that the model could generate feasible designs of higher resilience.<Sub>

## Datasets 
#### Summary of datasets and their sizes
| Analysis \ Network Size | 57 Bus | 118 Bus | 300 Bus |
| :-------- | :------- | :------------- | :---------------------- |
| AC PF    | 10,000 | 10,000 | 10,000 |
| DC OPF   | 100,000 | 100,000 | 100,000 |
| AC OPF   | 10,000 | 10,000 | 10,000 |

<sub>*PF: Power Flow / OPF: Optimal Power Flow*<sub>

Each folder contains 3 different folders of network size. Under the folder named with the network size are the datasets in CSV format. 
The network sizes were determined based on some of the most freqently used benchmarks: IEEE 57-, 118-, and 300-bus systems.

### Data Repository Structure
```bash
Repository
├── ACPF
│   ├── dataset_57_bus
│   │   └── 10,000 dataset
│   ├── dataset_118_bus
│   │   └── 10,000 dataset
│   └── dataset_300_bus
│       └── 10,000 dataset
├── DCOPF
│   ├── dataset_57_bus
│   │   └── 100,000 dataset
│   ├── dataset_118_bus
│   │   └── 100,000 dataset
│   └── dataset_300_bus
│       └── 100,000 dataset
├── ACOPF
│   ├── dataset_57_bus
│   │   └── 10,000 dataset
│   ├── dataset_118_bus
│   │   └── 10,000 dataset
│   └── dataset_300_bus
│       └── 10,000 dataset
├── LICENSE
└── README.md
```

## Data Structure
Each data sample consists of three or four files depending on the problem analysis: PF has three and OPF have four files.
- Branch contains the connection information and properties of the transmission lines
- Bus contains the type and power demand information for the buses and the results of the PF/OPF problem
- Gen contains information specific to generator buses within the network
- Gen Cost contains the operation cost model for each generator

<sub>*Generator operating costs are only considered for the optimal power flow problem. Hence, ACPF does not have gencost.csv files.*<sub>

A network data is represented as n(NS)_(SN), where NS is the Network Size and SN is the sample number starting from 1 and ending at 10,000 or 100,000 depending on the dataset.
Below are the details of the data structure, where the number indicates the column number of each data file.
```bash
├── n(NS)_(SN)_branch.csv
│   ├── connection information: 1) from bus and 2) to bus
│   ├── line properties: 3) resistance, 4) reactance, 5) susceptance, 6) line rating, and 7) line status
│   └── power flow results: 8) P injected at the from bus, 9) Q injected at the from bus, 10) P injected at the to bus, and 11) Q injected at the to bus
├── n(NS)_(SN)_bus.csv
│   ├── general information: 1) bus number and 2) bus type
│   └── power flow results: 3) P demand, 4) Q demand, 5) V magnitude, and 6) V phase angle
├── n(NS)_(SN)_gen.csv
│   ├── general information: 1) bus number
│   └── power flow results: 2) P output, 3) Q output, 4) V magnitude, 5) status, 6) capacity, and 7) minimum power output
└── n(NS)_(SN)_gencost.csv
    ├── general information: 1) cost model type
    ├── operation costs: 2) startup cost and 3) shutdown cost
    └── cost model: 4) number of coefficients and 5-end) coefficients
```

## MATPOWER and SynGrid
The datasets are generated using SynGrid:
- SynGrid is a matlab application that is integrated in MATPOWER
- MATPOWER is a MATLAB toolbox used for various applications on electrical engineering including power flow analysis

Refer to the repository for more details: [MATPOWER/SynGrid](https://github.com/MATPOWER/mx-syngrid)

## Additional Reference
Example case similar to this publication (GitHub repository): [Generative Graph for Transmission Grid](https://github.com/IBChung/generative_graph.git)

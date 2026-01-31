# Thesis Terminology Reference

**Thesis Title**: Privacy Protection Framework for Safety Beacon Message Management in the Internet of Vehicles
**Author**: Jiang Zheng
**Degree**: Doctor of Philosophy (Ph.D.) in Information Technology
**Institution**: Multimedia University, Malaysia
**Last Updated**: 2026-01-31

---

## Abbreviations

### Core Framework Components

| Full Form                                | Abbreviation | First Use                | Description                                      |
| ---------------------------------------- | ------------ | ------------------------ | ------------------------------------------------ |
| Privacy Protection Framework             | PPF          | Chapter 1, Section 1.5   | The integrated framework proposed in this thesis |
| SBM Separation Algorithm                 | SBM-SA       | Chapter 1, Section 1.5   | Module 1: Source-level privacy protection        |
| Privacy-Preserving Data Uploading Scheme | PriDUS       | Chapter 1, Section 1.5   | Module 2: Transmission layer protection          |
| Master-Slave Multi-Chain                 | MSMC         | Chapter 1, Section 1.5   | Module 3: Blockchain architecture                |
| Adaptive Grouping PBFT                   | AG-PBFT      | Chapter 1, Section 1.5   | Consensus algorithm for MSMC                     |
| Threshold Secret Sharing Algorithm       | TSSA         | Chapter 3, Section 3.3.2 | Cryptographic mechanism in PriDUS                |

### Vehicular Networking

| Full Form                          | Abbreviation | First Use                | Description                                  |
| ---------------------------------- | ------------ | ------------------------ | -------------------------------------------- |
| Internet of Vehicles               | IoV          | Chapter 1, Section 1.1   | Contemporary vehicular network ecosystem     |
| Intelligent Transportation Systems | ITS          | Chapter 1, Section 1.1   | Transportation system infrastructure         |
| Vehicular Ad-Hoc Networks          | VANETs       | Chapter 1, Section 1.1   | Legacy vehicular network architecture        |
| Safety Beacon Messages             | SBM          | Chapter 1, Section 1.1.1 | Vehicle status broadcast messages            |
| Vehicle-to-Everything              | V2X          | Chapter 1, Section 1.1   | Umbrella term for vehicle communication      |
| Vehicle-to-Vehicle                 | V2V          | Chapter 1, Section 1.1   | Inter-vehicle communication                  |
| Vehicle-to-Infrastructure          | V2I          | Chapter 1, Section 1.1   | Vehicle to roadside communication            |
| Vehicle-to-Network                 | V2N          | Chapter 1, Section 1.1   | Vehicle to cellular network communication    |
| Vehicle-to-Cloud                   | V2C          | Chapter 1, Section 1.1   | Vehicle to cloud platform communication      |
| Vehicle-to-Pedestrian              | V2P          | Chapter 1, Section 1.1   | Vehicle to pedestrian communication          |
| Vehicle to Edge                    | V2Edge       | Chapter 2, Section 2.4   | Vehicle to edge infrastructure communication |

### Infrastructure Components

| Full Form                 | Abbreviation | First Use                | Description                          |
| ------------------------- | ------------ | ------------------------ | ------------------------------------ |
| Roadside Unit             | RSU          | Chapter 1, Section 1.1   | Edge infrastructure node             |
| Roadside Units            | RSUs         | Chapter 1, Section 1.1   | Plural form                          |
| Onboard Unit              | OBU          | Chapter 1, Section 1.1.2 | Vehicle-mounted communication device |
| Certification Authority   | CA           | Chapter 1, Section 1.1   | Identity credential issuer           |
| Public Key Infrastructure | PKI          | Chapter 2, Section 2.3   | Cryptographic trust framework        |

### Communication Technologies

| Full Form                           | Abbreviation | First Use                | Description                       |
| ----------------------------------- | ------------ | ------------------------ | --------------------------------- |
| Dedicated Short-Range Communication | DSRC         | Chapter 1, Section 1.1.1 | IEEE 802.11p wireless protocol    |
| Cellular Vehicle-to-Everything      | C-V2X        | Chapter 1, Section 1.1.1 | LTE/5G-based communication        |
| Long-Term Evolution                 | LTE          | Chapter 1, Section 1.1.1 | 4G cellular standard              |
| Fifth Generation                    | 5G           | Chapter 1, Section 1.1   | Next-generation cellular standard |

### Blockchain Terms

| Full Form                           | Abbreviation | First Use                | Description                       |
| ----------------------------------- | ------------ | ------------------------ | --------------------------------- |
| Practical Byzantine Fault Tolerance | PBFT         | Chapter 1, Section 1.1.2 | Consensus algorithm               |
| Slave Chain                         | S-Chain      | Chapter 3, Section 3.3.3 | Regional blockchain in MSMC       |
| Master Chain                        | M-Chain      | Chapter 3, Section 3.3.3 | Global coordination chain in MSMC |
| Transactions Per Second             | TPS          | Chapter 1, Section 1.1.2 | Throughput metric                 |
| Block Header                        | BH           | Chapter 3, Section 3.3.3 | Block metadata section            |
| Block Body                          | BB           | Chapter 3, Section 3.3.3 | Block data section                |

### Identifiers and Data Elements

| Full Form           | Abbreviation | First Use                | Description                        |
| ------------------- | ------------ | ------------------------ | ---------------------------------- |
| Vehicle Identifier  | V-ID         | Chapter 3, Section 3.3.1 | Unique vehicle identity            |
| Sub-Identifiers     | sub-IDs      | Chapter 3, Section 3.3.2 | Split identity fragments in PriDUS |
| Group ID            | GID          | Chapter 3, Section 3.3.1 | Vehicle group identifier           |
| Location of Vehicle | LV           | Chapter 1, Section 1.1.1 | GPS coordinates in SBM             |
| Location of Scene   | LS           | Chapter 1, Section 1.1.1 | Incident location in SBM           |

### Research Methodology

| Full Form             | Abbreviation | First Use              | Description                  |
| --------------------- | ------------ | ---------------------- | ---------------------------- |
| Research Objective    | RO           | Chapter 1, Section 1.5 | Thesis research goals        |
| Problem Statement     | PS           | Chapter 1, Section 1.3 | Identified research problems |
| Research Question     | RQ           | Chapter 1, Section 1.4 | Guiding research questions   |
| Research Contribution | RC           | Chapter 1, Section 1.6 | Thesis contributions         |

### Security Terms

| Full Form                     | Abbreviation | First Use              | Description            |
| ----------------------------- | ------------ | ---------------------- | ---------------------- |
| Distributed Denial of Service | DDoS         | Chapter 6, Section 6.5 | Network attack type    |
| Central Processing Unit       | CPU          | Chapter 4, Section 4.3 | Computational resource |

### Simulation and Platforms

| Full Form                          | Abbreviation | First Use                | Description                 |
| ---------------------------------- | ------------ | ------------------------ | --------------------------- |
| Optimized Network Engineering Tool | OPNET        | Chapter 3, Section 3.7.2 | Network simulation platform |

### Related Works

| Full Form                                 | Abbreviation | First Use              | Description                |
| ----------------------------------------- | ------------ | ---------------------- | -------------------------- |
| Privacy-Preserving Spatial Crowdsourcing  | PriSC        | Chapter 2              | Related privacy scheme     |
| Data Aggregation and Batch Authentication | DABAB        | Chapter 2              | Related privacy solution   |
| Paid Information Collection               | PIC          | Chapter 1, Section 1.1 | Mobility data monetisation |

---

## Key Terms

### Technical Terms - Capitalisation Rules

- **Internet of Vehicles** - capitalised as proper noun (IoV)
- **blockchain** - lowercase in prose, unless starting a sentence
- **smart contract** - two words, lowercase
- **consensus algorithm** - lowercase
- **privacy protection** - lowercase
- **data lifecycle** - one word "lifecycle"
- **real-time** - hyphenated as adjective ("real-time processing")
- **state-of-the-art** - hyphenated when used as adjective
- **multi-chain** - hyphenated ("multi-chain architecture")
- **end-to-end** - hyphenated as adjective ("end-to-end protection")
- **re-identification** - hyphenated
- **pseudonym** - not "pseudo-nym"

### Framework and Algorithm Names

- **SBM-SA** - all caps with hyphen (SBM Separation Algorithm)
- **PriDUS** - capital P, D, U, S (Privacy-Preserving Data Uploading Scheme)
- **MSMC** - all caps (Master-Slave Multi-Chain)
- **AG-PBFT** - all caps with hyphen (Adaptive Grouping PBFT)
- **TSSA** - all caps (Threshold Secret Sharing Algorithm)

### Dataset Names

- **HighD** - capital H and D (German highway dataset)
- **NGSIM** - all caps (Next Generation Simulation)

### Platform Names

- **Hyperledger Fabric** - capital H and F
- **OPNET** - all caps
- **SUMO** - all caps (Simulation of Urban Mobility)

### Privacy Concepts

- **k-anonymity** - lowercase k with hyphen
- **l-diversity** - lowercase l with hyphen
- **t-closeness** - lowercase t with hyphen
- **mix-zone** - hyphenated
- **pseudonym rotation** - two words, lowercase
- **location cloaking** - two words, lowercase
- **trajectory tracking** - two words, lowercase
- **spatiotemporal correlation** - one word "spatiotemporal"

### Attack Types

- **Sybil attack** - capital S ("Sybil" is a proper noun)
- **Byzantine attack** - capital B
- **inference attack** - lowercase
- **linkage attack** - lowercase
- **replay attack** - lowercase
- **man-in-the-middle** - hyphenated (MITM)

---

## Consistency Rules

### Numbers

- Spell out one through nine in prose
- Use numerals for 10 and above
- Always use numerals with units: 5 ms, 100 MB, 32 GB, 10 Hz
- Use numerals for percentages: 5%, 35%, 96%
- Use numerals for technical specifications: k=8, n=5, t=3

### Units and Measurements

- **milliseconds** - abbreviated as "ms" (not "msec")
- **transactions per second** - "TPS" or spell out on first use
- **kilometres per hour** - "km/h" (not "kph")
- **metres per second squared** - "m/s\\textsuperscript{2}" for acceleration
- **gigabytes** - "GB" (not "gb" or "Gb")
- **terabytes** - "TB"
- **hertz** - "Hz" for frequency (10 Hz = 10 times per second)

### British English (Malaysian University Standard)

- behaviour (not behavior)
- analyse (not analyze)
- organisation (not organization)
- colour (not color)
- optimisation (not optimization)
- centralised (not centralized)
- decentralised (not decentralized)
- randomisation (not randomization)
- characterisation (not characterization)
- synchronisation (not synchronization)
- utilisation (not utilization)
- generalisation (not generalization)
- anonymisation (not anonymization)

### Thesis-Specific Terminology

| Avoid           | Use Instead                                    |
| --------------- | ---------------------------------------------- |
| car, automobile | vehicle                                        |
| server          | node, RSU, edge server (be specific)           |
| send            | transmit, broadcast, upload (context-specific) |
| get             | obtain, retrieve, acquire                      |
| use             | employ, utilise, apply                         |
| show            | demonstrate, indicate, illustrate              |
| good            | effective, efficient, optimal                  |
| bad             | ineffective, suboptimal, inadequate            |
| big             | large-scale, significant, substantial          |
| fast            | low-latency, high-throughput, efficient        |

---

## Chapter Notes

### Chapter 1: Introduction

- Define IoV, SBM, V2X on first use
- Introduce PPF, SBM-SA, PriDUS, MSMC, AG-PBFT
- Establish PS1, PS2, PS3 -> RQ1, RQ2, RQ3 -> RO1, RO2, RO3, RO4 mapping
- Reference SBM components: vehicle identity, LV (location of vehicle), LS (location of scene)

### Chapter 2: Literature Review

- Define VANETs, DSRC, C-V2X, PKI on first use
- Explain k-anonymity, l-diversity, t-closeness
- Introduce three-tier architecture: Access Layer, Edge Layer, Core Layer
- Summarise related works: DABAB, PriSC, BAVPM, PPAS

### Chapter 3: Research Methodology

- Detail PPF conceptual architecture
- Explain SBM-SA data types: Type I (identity), Type II (location), Type III (safety data)
- Define TSSA parameters: threshold t, total shares n
- Describe MSMC components: S-Chain, M-Chain, BH, BB
- Specify simulation platforms: OPNET, Hyperledger Fabric, HighD dataset

### Chapter 4: SBM-SA Module

- k-anonymity group size typically k=8-12
- Privacy leakage rates: 8-12% (proposed) vs 35-60% (baseline)
- Data utility preservation: >95%

### Chapter 5: PriDUS Module

- TSSA parameters: typically t=3, n=5
- Re-identification rates: 5-12% (proposed) vs 60-80% (baseline)
- Upload latency: <100 ms

### Chapter 6: MSMC and AG-PBFT

- Throughput: 45,000-65,000 TPS (proposed) vs 200-300 TPS (baseline PBFT)
- Confirmation latency: <800 ms
- Fault tolerance: up to 33% malicious nodes

### Chapter 7: PPF Feasibility Analysis

- End-to-end walkthrough of integrated framework
- Component synergy analysis
- Theoretical completeness verification

### Chapter 8: Conclusion

- Mirror terminology from Introduction
- Summarise RC1, RC2, RC3, RC4
- Acknowledge limitations and future work

---

## Cross-Reference Guide

### Problem Statement -> Research Question -> Research Objective

| Problem Statement                         | Research Question                                 | Research Objective            |
| ----------------------------------------- | ------------------------------------------------- | ----------------------------- |
| PS1: Source-level privacy vulnerabilities | RQ1: How to mitigate SBM generation privacy risk? | RO1: Propose SBM-SA           |
| PS2: V2Edge transmission vulnerabilities  | RQ2: How to protect SBM upload to RSUs?           | RO2: Propose PriDUS           |
| PS3: Centralised architecture limitations | RQ3: How to design scalable blockchain framework? | RO3: Design MSMC with AG-PBFT |
| -                                         | -                                                 | RO4: Analyse integrated PPF   |

### Research Contribution Mapping

| Contribution | Module         | Key Metric              |
| ------------ | -------------- | ----------------------- |
| RC1          | SBM-SA         | 8-12% privacy leakage   |
| RC2          | PriDUS         | 5-12% re-identification |
| RC3          | MSMC + AG-PBFT | 45,000-65,000 TPS       |
| RC4          | Integrated PPF | End-to-end protection   |

---

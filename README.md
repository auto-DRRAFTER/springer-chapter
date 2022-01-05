# auto-DRRAFTER

## About

This repository is intended for use with the chapter **Auto-DRRAFTER: Automated RNA modeling based on cryo-EM density** from the SpringerNature Methods in Molecular Biology: Protocols for RNA Structure and Dynamics Studies.

In this example, we will use the  *F. nucleatum* glycine riboswitch (PDB 6wll) and apo SAM-IV Riboswitch (PDB 6ues) that were previously solved by [Kappel et al. 2020](https://www.nature.com/articles/s41592-020-0878-9).

## Recommended Computing Requirement

Typical use of auto-DRRAFTER requires a high-performance computing cluster. While runs may be executed interactively, most auto-DRRAFTER runs benefit from using a job scheduler such as SLURM or Torque.

All jobs were executed on SKLB Duyu high performance computing center at Sichuan University and Sherlock 2.0 high performance computing cluster at Stanford University. Each auto-DRRAFTER round contains 150 jobs per helix placement of one end node (described below), with each job using one processor core available on either Duyu or Sherlock (Intel 6230, Intel E5-2640v4, Intel 5118 or AMD 7502). In the case of *F. nucleatum* glycine riboswitch, it took 144 computing hours (a total of 6 rounds with 24 hours per round) on 600 cores (a total of 4 end nodes with 150 jobs per end node).  

## Methods

The following are four python modules that will be used throughout the auto-DRRAFTER pipeline: 

1. auto-DRRAFTER_setup.py
2. submit_jobs.py
3. auto-DRRAFTER_setup_next_round.py
4. finalize_models.py

`auto-DRRAFTER_setup.py` is used to generate the low-pass density map to determine the `-map_thr` value and to place the initial probe helices. Both `submit_jobs.py` and `auto-DRRAFTER_setup_next_round.py` will then be used iteratively in each round; for example, there are six rounds in this example so both module will be ran six times. After reaching convergence, `finalize_models.py` is used to complete modeling.

## Organization

Input and output files of each auto-DRRAFTER round are available and organized in the following four subdirectories:

[`FNG_riboswitch_1/`](https://github.com/auto-DRRAFTER/springer-chapter/tree/main/FNG_riboswitch_1):  auto-DRRAFTER run for ***F. nucleatum* glycine riboswitch** executed on **Sherlock** computing cluster.

[`FNG_riboswitch_2/`](https://github.com/auto-DRRAFTER/springer-chapter/tree/main/FNG_riboswitch_2): auto-DRRAFTER run for ***F. nucleatum* glycine riboswitch** executed on **Duyu** computing cluster.

[`SAM-IV_riboswitch_1/`](https://github.com/auto-DRRAFTER/springer-chapter/tree/main/SAM-IV_riboswitch_1) :  auto-DRRAFTER run for **SAM-IV Riboswitch** executed on **Sherlock** computing cluster.

[`SAM-IV_riboswitch_2`](https://github.com/auto-DRRAFTER/springer-chapter/tree/main/SAM-IV_riboswitch_2)/ : auto-DRRAFTER run for **SAM-IV Riboswitch** executed on **Duyu** computing cluster.

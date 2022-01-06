# SAM_2

## Methods

Methods detailing the auto-DRRAFTER run for **SAM-IV Riboswitch** executed on **Duyu** computing cluster.

### Selecting end nodes for probe helix placement

```shell
# Step 2.1 from the auto-DRRAFTER chapter.
python $ROSETTA/main/source/src/apps/public/DRRAFTER/auto-DRRAFTER_setup.py -map_thr 20 -full_dens_map input_files/SAM.mrc -full_dens_map_reso 10.0 -fasta input_files/SAM.fasta -secstruct input_files/SAM.txt -out_pref SAM -rosetta_directory $ROSETTA/main/source/bin/ -nstruct_per_job 200 -cycles 30000 -fit_only_one_helix -rosetta_extension .static.linuxgccrelease -just_low_pass`

```shell
# Step 3.1 from the auto-DRRAFTER chapter.
python $ROSETTA/main/source/src/apps/public/DRRAFTER/auto-DRRAFTER_setup.py -map_thr 0.274 -full_dens_map input_files/SAM.mrc -full_dens_map_reso 10.0 -fasta input_files/SAM.fasta -secstruct input_files/SAM.txt -out_pref SAM -rosetta_directory $ROSETTA/main/source/bin/ -nstruct_per_job 200 -cycles 30000 -fit_only_one_helix -rosetta_extension .static.linuxgccrelease```
>		###### Output of Step 3.1
		Low-pass filtering the map to 20A.
		Converting density map to graph.
		Possible end nodes in the map: 
		1 11 
		You can visualize the end nodes in SAM_init_points.pdb
		You can specify which of these end nodes you'd like to use with -use_end_node
		Converting secondary structure to graph.
		Mapping secondary structure to density map.
		Setting up DRRAFTER runs.
		Making full helix H11

### Build initial models with different end nodes


#### R1 (Round 1)

```shell
# Step 4.2, first iteration from the auto-DRRAFTER chapter.
python $ROSETTA/main/source/src/apps/public/DRRAFTER/submit_jobs.py -out_pref SAM -curr_round R1 -njobs 150 -template_submission_script input_files/job_submission_template.sh -queue_command sbatch```

```shell
# Step 5.1, first iteration from the auto-DRRAFTER chapter.
python $ROSETTA/main/source/src/apps/public/DRRAFTER/auto-DRRAFTER_setup_next_round.py -out_pref SAM -curr_round R1 -nmodels 10 -rosetta_directory $ROSETTA/main/source/bin/ -convergence_threshold 10 -rosetta_extension .static.linuxgccrelease```
>###### Output of Step 5.1, first iteration
>	Setting up next round\
>	Overall convergence 27.383\
>	Density threshold: 0.653

### Iterative refinement of RNA models


#### R2 (Round 2)

```shell
# Step 4.2, second iteration from the auto-DRRAFTER chapter.
python $ROSETTA/main/source/src/apps/public/DRRAFTER/submit_jobs.py -out_pref SAM -curr_round R2 -njobs 150 -template_submission_script input_files/job_submission_template.sh -queue_command sbatch

```shell
# Step 5.1, second iteration from the auto-DRRAFTER chapter.
python $ROSETTA/main/source/src/apps/public/DRRAFTER/auto-DRRAFTER_setup_next_round.py -out_pref SAM -curr_round R2 -rosetta_directory $ROSETTA/main/source/bin/ -convergence_threshold 10 -rosetta_extension .static.linuxgccrelease
>###### Output of Step 5.1, first iteration
>	Setting up next round\
>	Overall convergence 6.435\
>	Density threshold: 0.653

As the overall convergence of `6.435`: is under the `-convergence_threshold 10`, we can now proceed directly to the final two rounds of modeling.

### Final two rounds of modeling

#### FINAL_R3 (Final Round 3)

```shell
# Step 6.2 from the auto-DRRAFTER chapter.
python $ROSETTA/main/source/src/apps/public/DRRAFTER/submit_jobs.py -out_pref SAM -curr_round FINAL_R3 -njobs 150 -template_submission_script input_files/job_submission_template.sh -queue_command sbatch
```

```shell
# Step 6.3 from the auto-DRRAFTER chapter.
python $ROSETTA/main/source/src/apps/public/DRRAFTER/auto-DRRAFTER_setup_next_round.py -out_pref SAM -curr_round FINAL_R3 -rosetta_directory $ROSETTA/main/source/bin/ -rosetta_extension .static.linuxgccrelease
```
>###### Output of Step 6.3
>	Setting up next round\
>	Overall convergence 5.428\
>	Density threshold: 0.653

#### FINAL_R4 (Final Round 4)

```shell
# Step 6.4 from the auto-DRRAFTER chapter.
python $ROSETTA/main/source/src/apps/public/DRRAFTER/submit_jobs.py -out_pref SAM -curr_round FINAL_R4 -njobs 150 -template_submission_script input_files/job_submission_template.sh -queue_command sbatch
```

```shell
# Step 6.5 from the auto-DRRAFTER chapter.
python $ROSETTA/main/source/src/apps/public/DRRAFTER/auto-DRRAFTER_setup_next_round.py -out_pref SAM -curr_round FINAL_R4 -rosetta_directory $ROSETTA/main/source/bin/ -rosetta_extension .static.linuxgccrelease
```
>###### Output of Step 6.5
>	DONE building models for SAM

### Finalizing Models

```shell
# Step 7.1 from the auto-DRRAFTER chapter.
python $ROSETTA/main/source/src/apps/public/DRRAFTER/finalize_models.py -fasta input_files/SAM.fasta -out_pref SAM -final_round FINAL_R4
```
>###### Output of Step 7.1
>	Done finalizing models

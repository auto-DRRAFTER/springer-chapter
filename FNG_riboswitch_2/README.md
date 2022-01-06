# FNG_riboswitch_2

## Methods

Methods detailing the auto-DRRAFTER run for ***F. nucleatum* glycine riboswitch** executed on **Duyu** computing cluster.

### Selecting end nodes for probe helix placement
```shell
# Step 2.1 from the auto-DRRAFTER chapter.
python $ROSETTA/main/source/src/apps/public/DRRAFTER/auto-DRRAFTER_setup.py -map_thr 20 -full_dens_map input_files/FNG_riboswitch.mrc -full_dens_map_reso 10.0 -fasta input_files/FNG_riboswitch.fasta -secstruct input_files/FNG_riboswitch.txt -out_pref FNG_riboswitch -rosetta_directory $ROSETTA/main/source/bin/ -nstruct_per_job 200 -cycles 30000 -fit_only_one_helix -rosetta_extension .static.linuxgccrelease -just_low_pass
```

```shell
# Step 3.1 from the auto-DRRAFTER chapter.
python $ROSETTA/main/source/src/apps/public/DRRAFTER/auto-DRRAFTER_setup.py -map_thr 0.0499 -full_dens_map input_files/FNG_riboswitch.mrc -full_dens_map_reso 10.0 -fasta input_files/FNG_riboswitch.fasta -secstruct input_files/FNG_riboswitch.txt -out_pref FNG_riboswitch -rosetta_directory $ROSETTA/main/source/bin/ -nstruct_per_job 200 -cycles 30000 -fit_only_one_helix -rosetta_extension .static.linuxgccrelease
```
>		###### Output of Step 3.1
>		Using only one end node!\
>		Low-pass filtering the map to 20A.\
>		Converting density map to graph.\
>		Possible end nodes in the map:\
>		1 5 11\
>		You can visualize the end nodes in FNG_riboswitch_init_points.pdb\
>		You can specify which of these end nodes you'd like to use with ->use_end_node\
>		Converting secondary structure to graph.\
>		Mapping secondary structure to density map.\
>		Setting up DRRAFTER runs.\
>		Making full helix H7\
>		Making full helix H4\
>		Making full helix H10\
>		Making full helix H15

### Build initial models with different end nodes

#### R1 (Round 1)
```shell
# Step 4.2, first iteration from the auto-DRRAFTER chapter.
python $ROSETTA/main/source/src/apps/public/DRRAFTER/submit_jobs.py -out_pref FNG_riboswitch -curr_round R1 -njobs 150 -template_submission_script input_files/job_submission_template.sh -queue_command sbatch
```

```shell
# Step 5.1, first iteration from the auto-DRRAFTER chapter.
python $ROSETTA/main/source/src/apps/public/DRRAFTER/auto-DRRAFTER_setup_next_round.py -out_pref FNG_riboswitch -curr_round R1 -nmodels 10 -rosetta_directory $ROSETTA/main/source/bin/ -convergence_threshold 10 -rosetta_extension .static.linuxgccrelease```
>###### Output of Step 5.1, first iteration
>	Setting up next round\
>	Overall convergence 38.971\
>	Density threshold: 0.051\
>	Density threshold: 0.051\
>	Density threshold: 0.051\
>	Density threshold: 0.051

### Iterative refinement of RNA models
#### R2 (Round 2)

```shell
# Step 4.2, second iteration from the auto-DRRAFTER chapter.
python $ROSETTA/main/source/src/apps/public/DRRAFTER/submit_jobs.py -out_pref FNG_riboswitch -curr_round R2 -njobs 150 -template_submission_script input_files/job_submission_template.sh -queue_command sbatch
```

```shell
# Step 5.1, second iteration from the auto-DRRAFTER chapter.
python $ROSETTA/main/source/src/apps/public/DRRAFTER/auto-DRRAFTER_setup_next_round.py -out_pref FNG_riboswitch -curr_round R2 -nmodels 10 -rosetta_directory $ROSETTA/main/source/bin/ -convergence_threshold 10 -rosetta_extension .static.linuxgccrelease
```
>###### Output of Step 5.1, second iteration
>	Setting up next round\
>	Overall convergence 37.804\
>	Density threshold: 0.051\
>	Density threshold: 0.051\
>	Density threshold: 0.051\
>	Density threshold: 0.051

#### R3 (Round 3)

```shell
# Step 4.2, third iteration from the auto-DRRAFTER chapter.
python $ROSETTA/main/source/src/apps/public/DRRAFTER/submit_jobs.py -out_pref FNG_riboswitch -curr_round R3 -njobs 150 -template_submission_script input_files/job_submission_template.sh -queue_command sbatch
```

```shell
# Step 5.1, third iteration from the auto-DRRAFTER chapter.
python $ROSETTA/main/source/src/apps/public/DRRAFTER/auto-DRRAFTER_setup_next_round.py -out_pref FNG_riboswitch -curr_round R3 -rosetta_directory $ROSETTA/main/source/bin/ -convergence_threshold 10 -rosetta_extension .static.linuxgccrelease
```
>###### Output of Step 5.1, third iteration
>	Overall convergence 25.482\
>	Density threshold: 0.051\
>	Density threshold: 0.051\
>	Density threshold: 0.051\
>	Density threshold: 0.051


#### R4 (Round 4)

```shell
# Step 4.2, third iteration from the auto-DRRAFTER chapter.
python $ROSETTA/main/source/src/apps/public/DRRAFTER/submit_jobs.py -out_pref FNG_riboswitch -curr_round R4 -njobs 150 -template_submission_script input_files/job_submission_template.sh -queue_command sbatch
```

```shell
# Step 5.1, third iteration from the auto-DRRAFTER chapter.
python $ROSETTA/main/source/src/apps/public/DRRAFTER/auto-DRRAFTER_setup_next_round.py -out_pref FNG_riboswitch -curr_round R4 -rosetta_directory $ROSETTA/main/source/bin/ -convergence_threshold 10 -rosetta_extension .static.linuxgccrelease
```
>###### Output of Step 5.1, third iteration
>	Overall convergence 14.875\
>	Density threshold: 0.051\
>	Density threshold: 0.051\
>	Density threshold: 0.051\
>	Density threshold: 0.051


#### R5 (Round 5)

```shell
# Step 4.2, third iteration from the auto-DRRAFTER chapter.
python $ROSETTA/main/source/src/apps/public/DRRAFTER/submit_jobs.py -out_pref FNG_riboswitch -curr_round R5 -njobs 150 -template_submission_script input_files/job_submission_template.sh -queue_command sbatch
```

```shell
# Step 5.1, third iteration from the auto-DRRAFTER chapter.
python $ROSETTA/main/source/src/apps/public/DRRAFTER/auto-DRRAFTER_setup_next_round.py -out_pref FNG_riboswitch -curr_round R5 -rosetta_directory $ROSETTA/main/source/bin/ -convergence_threshold 10 -rosetta_extension .static.linuxgccrelease
```
>###### Output of Step 5.1, third iteration
>	Overall convergence 14.055\
>	Density threshold: 0.051\
>	Density threshold: 0.051\
>	Density threshold: 0.051\
>	Density threshold: 0.051


#### R6 (Round 6)

```shell
# Step 4.2, third iteration from the auto-DRRAFTER chapter.
python $ROSETTA/main/source/src/apps/public/DRRAFTER/submit_jobs.py -out_pref FNG_riboswitch -curr_round R6 -njobs 150 -template_submission_script input_files/job_submission_template.sh -queue_command sbatch
```

```shell
# Step 5.1, third iteration from the auto-DRRAFTER chapter.
python $ROSETTA/main/source/src/apps/public/DRRAFTER/auto-DRRAFTER_setup_next_round.py -out_pref FNG_riboswitch -curr_round R6 -rosetta_directory $ROSETTA/main/source/bin/ -convergence_threshold 10 -rosetta_extension .static.linuxgccrelease
```
>###### Output of Step 5.1, third iteration
>	Overall convergence 14.068\
>	Density threshold: 0.051\
>	Density threshold: 0.051\
>	Density threshold: 0.051\
>	Density threshold: 0.051

#### R7 (Round 7)

```shell
# Step 4.2, fourth iteration from the auto-DRRAFTER chapter.
python $ROSETTA/main/source/src/apps/public/DRRAFTER/submit_jobs.py -out_pref FNG_riboswitch -curr_round R7 -njobs 150 -template_submission_script input_files/job_submission_template.sh -queue_command sbatch
```

```shell
# Step 5.1, fourth iteration from the auto-DRRAFTER chapter.
python $ROSETTA/main/source/src/apps/public/DRRAFTER/auto-DRRAFTER_setup_next_round.py -out_pref FNG_riboswitch -curr_round R7 -rosetta_directory $ROSETTA/main/source/bin/ -convergence_threshold 10 -rosetta_extension .static.linuxgccrelease
```
>###### Output of Step 5.1, fourth iteration
>	Setting up next round\
>	Overall convergence 13.967\
	Convergence doesn't seem to be getting better, skipping to final round
>	Density threshold: 0.051

### Final two rounds of modeling

#### FINAL_R8 (Final Round 8)

```shell
# Step 6.2 from the auto-DRRAFTER chapter.
python $ROSETTA/main/source/src/apps/public/DRRAFTER/submit_jobs.py -out_pref FNG_riboswitch -curr_round FINAL_R8 -njobs 150 -template_submission_script input_files/job_submission_template.sh -queue_command sbatch
```

```shell
# Step 6.3 from the auto-DRRAFTER chapter.
python $ROSETTA/main/source/src/apps/public/DRRAFTER/auto-DRRAFTER_setup_next_round.py -out_pref FNG_riboswitch -curr_round FINAL_R8 -rosetta_directory $ROSETTA/main/source/bin/ -rosetta_extension .static.linuxgccrelease
```
>###### Output of Step 6.3
>	Setting up next round\
>	Overall convergence 8.562\
>	Density threshold: 0.051

#### FINAL_R9 (Final Round 9)

```shell
# Step 6.4 from the auto-DRRAFTER chapter.
python $ROSETTA/main/source/src/apps/public/DRRAFTER/submit_jobs.py -out_pref FNG_riboswitch -curr_round FINAL_R9 -njobs 150 -template_submission_script input_files/job_submission_template.sh -queue_command sbatch
```

```shell
# Step 6.5 from the auto-DRRAFTER chapter.
python $ROSETTA/main/source/src/apps/public/DRRAFTER/auto-DRRAFTER_setup_next_round.py -out_pref FNG_riboswitch -curr_round FINAL_R9 -rosetta_directory $ROSETTA/main/source/bin/ -rosetta_extension .static.linuxgccrelease
```
>###### Output of Step 6.5
>	DONE building models for FNG_riboswitch

### Finalizing Models

```shell
# Step 7.1 from the auto-DRRAFTER chapter.
python $ROSETTA/main/source/src/apps/public/DRRAFTER/finalize_models.py -fasta input_files/FNG_riboswitch.fasta -out_pref FNG_riboswitch -final_round FINAL_R9
```
>###### Output of Step 7.1
>	Done finalizing models
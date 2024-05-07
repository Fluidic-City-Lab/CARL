## CARL: Congestion-Aware Reinforcement Learning for Imitation-based Perturbations in Mixed Traffic Contro

<p align="center">
  <img src="https://github.com/poudel-bibek/EnduRL/blob/5241e6f905b16dcb43df86fbb328b52c64050550/ring/ring_banner.gif" alt="Alt Text">
  <br>
  <i>Our RVs in the Ring</i>
</p>

Paper in: [arXiv](https://arxiv.org/abs/2404.00796v1)

------
This work was done on top of [FLOW](https://github.com/flow-project/flow) framework obtained on Jan 3, 2023.

### Installation instructions 

Developed and tested on Ubuntu 18.04, Python 3.7.3

- Install [Anaconda](https://www.anaconda.com/)
- Setup [SUMO versio 1.15.0](https://github.com/eclipse-sumo/sumo/releases/tag/v1_15_0)
- Clone this repository
- Use the following commands

```
conda env create -f environment.yml
conda activate flow
python setup.py develop
pip install -U pip setuptools
pip install -r requirements.txt
```

### Part 1: Training the Congestion Stage Classifier
- Follow the Notebooks: [Ring](https://github.com/poudel-bibek/Imitation_Congestion/blob/master/ring/Ours/CSC_training_ring.ipynb)

If you want to use the trained CSCs, see `Data` section below. 

### Part 2: Training RL based RVs
Go to the folder for the environment `ring/Ours` and enter the command:

```
# Train our policy in Ring (at 5% penetration) 
python train.py singleagent_ring

# Train our policy in Ring (at penetrations >5%)
python train.py multiagent_ring


### Part 3: Generate rollouts for RL based RVs or Heuristic and Model based RVs and save as csv files.
All scripts related to this part are consolidated [Evaluate Ring](https://github.com/poudel-bibek/Imitation_Congestion/blob/master/ring/Evaluate%20Ring.ipynb) Jupyter Notebook. 

#### I. RL based RVs:

Replace the method name to be one of: ours, wu

```
python test_rllib.py [Location of trained policy] [checkpoint number] --method wu --gen_emission --num_rollouts [no_of_rollouts] --shock --render --length 260
```

#### II. Heuristic and Model based RVs:
For all (replace the method_name to be one of: bcm, lacc, piws, fs, idm)

```
python classic.py --method [method_name] --render --length 260 --num_rollouts [no_of_rollouts] --shock --gen_emission
```
For stability tests where a standard perturbation is applied by a leading HV, include --stability to the line above

### Part 4: Evaluate the generated rollouts

To evaluate the generated rollouts into Safety, Efficiency and Stability metrics:
Replace the method name to be one of: bcm, idm, fs, piws, lacc, wu, ours

```
python eval_metrics.py --method [method_name] --num_rollouts [no_of_rollouts]
```

To add plots to the metrics, include --save_plots

For Stability plots

```
python eval_plots.py --method [method_name]
```


### Data

- Data (including experiments rollouts and full policies): [HuggingFace](https://huggingface.co/datasets/matrix-multiply/EnduRL_data/tree/main)

- Trained CSC Models: [HuggingFace](https://huggingface.co/matrix-multiply/Congestion_Stage_Classifier/tree/main)


### Cite


```

@article{poudel2024endurl,
  title={},
  author={Poudel, Bibek and Li, Weizi and Li, Suhai},
  journal={arXiv preprint arXiv:2311.12261},
  year={2024}
}

```

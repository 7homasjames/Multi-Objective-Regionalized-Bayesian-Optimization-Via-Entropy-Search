# Multi-Objective-Regionalized-Bayesian-Optimization-Via-Entropy-Search(MORBES)
## A new methodology to explore the Pareto front more effectively. The proposed approach uses a Maximum Value Entropy selection procedure to search the entire Pareto front. 
Finding the best trade-offs between several complex objective functions is a problem that is frequently encountered in a variety of disciplines, such as science, engineering, and machine learning. Computationally expensive simulations are frequently required in these domains to balance trade-offs, e.g., between optical device efficiency and image quality. It can be necessary to build and test prototypes or run complex computer simulations in order to assess a design. Sample-efficient optimization is therefore essential. 

This report introduces a fresh way to solve this obstacle, allowing Bayesian Optimization to be used to high-dimensional multi-objective situations. Through the use of a coordinated collection of local trust regions (TRs), the method known as MORBES ("Multi-Objective Regionalized Bayesian Optimization Using Entropy Search") optimizes various areas of the global Pareto frontier in concurrently by computing their entropies.

### MORBES Architecture
#### Center Selection Of a Hypercube via Maximum Value Entropy Search

MORBES needs to identify a point on the pareto front with maximum entropy relative to the point being referred. This selected point should have the highest variance to ensure broad range across the Pareto front, as points in highly crowded regions contribute less.
<div align="center">
  <img src="https://github.com/7homasjames/Multi-Objective-Regionalized-Bayesian-Optimization-Via-Entropy-Search/assets/118433299/24346484-1f8d-44c3-af5f-a689b961e697" alt="MORBES" width="500" height="400">
</div>

#### Tchebycheff's Scalarization for Reintializing Trusted Regions

MORBES carries out local optimization inside a trust region (TR), a principled method based on hypervolume scalarization is used to re-initialize the TRs to guarantee global optimization. By aggregating the weights of each objective, as defined by the \(\lambda\) weights, and combining them into a single scalar value, this method combines numerous objectives. A multi-objective optimization problem can be successfully reduced to a single-objective problem using this technique. As a result, maximizing the hypervolume is the same as maximizing the randomized single-objective scalarization \cite{zhang2020random}, guaranteeing that the solution set respects the assigned importance of each objective while fully covering the objective space
<div align="center">
  <img src="https://github.com/7homasjames/Multi-Objective-Regionalized-Bayesian-Optimization-Via-Entropy-Search/assets/118433299/fdfa6cc3-edea-4150-8c9c-0c4bf4321afe" alt="RE" width="500" height="100">
</div>


### Getting Into the Code

The project is structured into four main parts:

1. **Utilities**     : The utilities for constructing the acquisition functions and other helper methods are defined in the `morbes/` directory.
2. **Experiments**   : MORBES has been tested on various experiments  and they are defined in `experiments/` directory
3. **Configuration** : The experiment configurations are found in the `config.json` file of each sub-directory.
4. **Main function** : `main.py/` is used to run the experiments


Center Selection Of a Hypercube via Maximum Value Entropy Search is implemented in the `morbes/trust_region.py` file and Tchebycheff's Scalarization for Reintializing Trusted Regions is implemented in the  `morbes/state.py` file.

### Running the code

To run a basic benchmark based on the config.json file in experiments/<experiment_name> using <algorithm>, follow these steps:

1. Navigate to the experiments directory.
2. Run the main.py script with the specified experiment name, algorithm, and seed

```bash
cd experiments 
python main.py <experiment_name> morbes <seed>

Where

experiments = {
    "dtlz2_10d": "DTLZ2 (d=10)",
    "dtlz2_30d": "DTLZ2 (d=30)",
    "dtlz2_100d": "DTLZ2 (d=100)",
    "dtlz5_m2": "DTLZ5 (M=2)",
    "dtlz7_m2": "DTLZ7 (M=2)",
    "rover": "Rover",
    "welded_beam": "Welded Beam",
}








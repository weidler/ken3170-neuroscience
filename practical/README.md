# Computer Practical 5: Modeling in Neuroscience (KEN3170)

In this practical you will learn how we measure the alignment between to systems without relying on them to be of equal scale or
dimensionality. Instead of directly comparing the internal representations of two systems, we can use RSA to evaluate how well the _representational geometries_ of the systems align. That is, instead of measuring the distance between concept representations across systems, we measure the similarity between the ways in which the systems differentiate between concepts.

### Part I: Diving deeper into RSA

In the table below you are given **two computational models** that produce internal representations of the same set of stimuli, alongside **reference data from the brain**. Your goal is to use **Representational Similarity Analysis (RSA)** to evaluate which model better matches the geometry of the brain data.

| Class | Model1 (len=5) | Model2 (len=7) | Brain (len=9) |
| --- | --- | --- | --- |
| A   | \[0.971, 0.04, -0.046, 0.141, -0.159\] | \[-0.267, -0.215, -0.032, -0.088, -0.189, -0.895, -0.175\] | \[0.981, -0.066, -0.045, -0.14, 0.058, 0.005, 0.06, -0.016, -0.095\] |
| B   | \[0.988, 0.017, -0.068, 0.073, -0.131\] | \[0.113, 0.293, 0.401, 0.783, -0.137, -0.26, -0.097\] | \[0.974, -0.042, -0.055, -0.179, 0.05, 0.049, 0.014, 0.035, -0.087\] |
| C   | \[0.102, 0.155, 0.973, -0.084, 0.09\] | \[0.932, -0.072, -0.073, -0.188, 0.236, 0.079, 0.089\] | \[0.1, 0.138, 0.96, -0.084, 0.089, -0.022, -0.096, -0.079, -0.145\] |
| D   | \[0.089, 0.992, -0.031, -0.067, -0.072\] | \[0.067, -0.087, 0.185, -0.157, -0.179, 0.122, 0.955\] | \[0.051, 0.99, -0.099, -0.016, 0.003, -0.067, -0.032, -0.003, -0.086\] |
| E   | \[0.144, 0.975, -0.027, -0.061, -0.142\] | \[-0.13, -0.115, -0.076, -0.042, -0.094, -0.083, -0.979\] | \[0.077, 0.986, -0.094, -0.042, 0.013, -0.067, -0.036, -0.037, -0.097\] |

To this end, go step by step through the process of RSA.

1. For each system (i.e., model or brain) calculate the pairwise dissimilarities between classes within the system's representational space. Use the Euclidean distance to do that:

   $$d(\mathbf{x}_i, \mathbf{x}_j) = \lVert \mathbf{x}_i - \mathbf{x}_j \rVert_2 = \sqrt{\sum_{k=1}^{n} (x_{i,k} - x_{j,k})^2}$$

   where $\mathbf{x}_i$ and $\mathbf{x}_j$ are the representational vectors (activation patterns of brain or model) for classes $i$ and $j$ within one system, and $n$ is the dimensionality of that system's representational space. For every pair of classes this gives you the **Representational Dissimilarity Matrix (RDM)** of that system, $RDM \in \mathbb{R}^{5 \times 5}$, with entries $RDM_{ij} = d(\mathbf{x}_i, \mathbf{x}_j)$. Construct one RDM per system (Model1, Model2, and Brain), per hand.

2. Calculate the similarity between the model RDMs and the brain RDM using the Pearson correlation coefficient. Since RDMs are symmetric with a zero diagonal, only compare the **upper (or lower) triangle, off-diagonal entries**. Let's call this vector of unique dissimilarities $\mathbf{v}$:

   $$r(RDM_A, RDM_B) = \frac{\sum_{k=1}^{m} (v_{A,k} - \bar{v}_A)(v_{B,k} - \bar{v}_B)}{\sqrt{\sum_{k=1}^{m} (v_{A,k} - \bar{v}_A)^2} \sqrt{\sum_{k=1}^{m} (v_{B,k} - \bar{v}_B)^2}}$$

   where $v_{A,k}$ and $v_{B,k}$ are the $k$-th entries of the vectorized upper triangles of $RDM_A$ and $RDM_B$, $\bar{v}_A$ and $\bar{v}_B$ their means, and $m$ the number of unique off-diagonal entries. This gives you one correlation value per model (so you should have Model1 vs. Brain and Model2 vs. Brain).

3. Report which of the models is the better fit.

For now, do this by hand (obviously using a calculator or whatever) to get a better feel for the process.


### Part II: Programmatic RSA

Now that you should have a good understanding of the process of RSA by hand, you will implement the same pipeline in Python. Doing this yourself, from scratch, before you get to use a full-blown library (e.g., `rsatoolbox`) will help you understand what is actually happening under the hood. Work in Python and build a small toolbox step by step. Use only `numpy`, `scipy` or similar libraries (e.g., plotting), but no RSA-specific libraries. You can always sanity-check your code by comparing against the hand calculations you did in Part I. For the table above, your `compute_rdm()` output should reproduce the RDMs you computed by hand, and your `compare_rdms()` output should reproduce the correlation values you computed by hand.

#### Step 1: Represent the data

Store each system representation as a `(n_classes, n_features)` numpy array. 

```python
import numpy as np

model1 = np.array([
    [0.971, 0.04, -0.046, 0.141, -0.159],
    [0.988, 0.017, -0.068, 0.073, -0.131],
    [0.102, 0.155, 0.973, -0.084, 0.09],
    [0.089, 0.992, -0.031, -0.067, -0.072],
    [0.144, 0.975, -0.027, -0.061, -0.142],
])

model2 = np.array([
    [-0.267, -0.215, -0.032, -0.088, -0.189, -0.895, -0.175],
    [0.113, 0.293, 0.401, 0.783, -0.137, -0.26, -0.097],
    [0.932, -0.072, -0.073, -0.188, 0.236, 0.079, 0.089],
    [0.067, -0.087, 0.185, -0.157, -0.179, 0.122, 0.955],
    [-0.13, -0.115, -0.076, -0.042, -0.094, -0.083, -0.979],
])

brain = np.array([
    [0.981, -0.066, -0.045, -0.14, 0.058, 0.005, 0.06, -0.016, -0.095],
    [0.974, -0.042, -0.055, -0.179, 0.05, 0.049, 0.014, 0.035, -0.087],
    [0.1, 0.138, 0.96, -0.084, 0.089, -0.022, -0.096, -0.079, -0.145],
    [0.051, 0.99, -0.099, -0.016, 0.003, -0.067, -0.032, -0.003, -0.086],
    [0.077, 0.986, -0.094, -0.042, 0.013, -0.067, -0.036, -0.037, -0.097],
])
```

**Test dataset.** The table in Part I works for a first pass, but to actually test and benchmark your functions in Steps 2 and 6 use `data/rsa_individual_test_data.npz`, a larger synthetic dataset:

```python
data = np.load("data/rsa_individual_test_data.npz")
brain, model_good, model_bad = data["brain"], data["model_good"], data["model_bad"]
class_labels = data["class_labels"]
```

#### Step 2: Compute an RDM

Implement a function that takes a `(n_classes, n_features)` array of representations and returns the `(n_classes, n_classes)` RDM of pairwise Euclidean distances from Part I, Equation 1.

```python
def compute_rdm(patterns: np.ndarray) -> np.ndarray:
    """Compute the Euclidean-distance RDM for a set of representational patterns."""
    n_classes = patterns.shape[0]
    rdm = np.zeros((n_classes, n_classes))
    
    # TODO construct RDM
    
    return rdm
```

**Tip**: First write this with a double `for` loop over class pairs. When that works, and it will be slow, try to vectorize it and benchmark to feel good about the performance improvement.

#### Step 3: Compare two RDMs

Implement a function that takes two RDMs and returns their similarity as the Pearson correlation between their vectorized upper triangles (`np.triu_indices`) as in Part I, Equation 2. Feel free to use `scipy.stats.pearsonr` or `np.corrcoef`, this is not a math class.

```python
def upper_triangle(rdm: np.ndarray) -> np.ndarray:
    """Extract the off-diagonal upper-triangular entries of an RDM as a 1D vector."""
    pass
    

def compare_rdms(rdm_a: np.ndarray, rdm_b: np.ndarray) -> float:
    """Compare two RDMs via Pearson correlation of their upper-triangular entries."""
    pass
```

#### Step 4: Apply your amazing functions

Use `compute_rdm()` on `model1`, `model2`, and `brain` and then use `compare_rdms()` to compute the Model1-to-Brain and Model2-to-Brain similarities. Confirm you get more or less the same numbers as by hand, and the same conclusion about which model fits better.

#### Step 5: Visualize your RDMs

Write a small helper that plots an RDM (e.g., with `matplotlib.pyplot.imshow`). Plot all three RDMs side by side. Does the visual similarity between the Model1/Model2 RDM and the Brain RDM match what you expected from the correlation values?

#### Step 6: Generalize your toolbox

Turn your code into a minimal, reusable module (your cute little toolbox!) and extend it with some of the following:

- Support additional dissimilarity metrics in `compute_rdm()` (e.g., `1 - correlation` instead of Euclidean distance).
- Support Spearman's rank correlation as an alternative to Pearson in `compare_rdms()`.
- A `compare_to_many(reference_rdm, candidate_rdms)` function that compares one reference RDM against a list of candidate RDMs and returns a ranked list of similarities.
- Statistical tests for comparing multiple RDMs for one system (e.g., multiple independent runs of the same model, multiple participants, ...) with confidence intervals. Use `data/rsa_group_test_data.npz`, which holds `participants` (6 x classes x channels), `model_a` and `model_b` (10 runs x classes x units each) and score every participant against every model run, report the mean with a 95% CI, and test whether model A fits better than model B. Think about which sources of variability your CI should reflect: both participants and model runs are random samples.

Keep this toolbox around, you'll have the option to use it in the assignment.

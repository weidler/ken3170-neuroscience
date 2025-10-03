# Computer Practical 5: Modeling in Neuroscience (KEN3170)

### Part I: Diving deeper into RSA - By Hand

You are given **two computational models** that produce internal representations of the same set of stimuli, alongside **reference data from the brain**. Use **Representational Similarity Analysis (RSA)** to evaluate which model better matches the structure of the brain data.  

**Reflect on the following**:

1. How do we represent the responses of a model or the brain for each stimulus?
2. What kind of similarity or dissimilarity measure are there, and why should we use them?  
Consider this overview: [https://rsatoolbox.readthedocs.io/en/stable/distances.html](https://rsatoolbox.readthedocs.io/en/stable/distances.html)
3. How do we construct and interpret representational dissimilarity matrices (RDMs)?
4. How can you quantify the correspondence between a model’s RDM and the brain’s RDM?  
Consider this overview: [https://rsatoolbox.readthedocs.io/en/stable/comparing.html](https://rsatoolbox.readthedocs.io/en/stable/comparing.html)  
5. If one model correlates more strongly with the brain than the other, what does that imply?  

| Class | Model1 (len=5) | Model2 (len=7) | Brain (len=9) |
| --- | --- | --- | --- |
| A   | \[0.971, 0.04, -0.046, 0.141, -0.159\] | \[-0.267, -0.215, -0.032, -0.088, -0.189, -0.895, -0.175\] | \[0.981, -0.066, -0.045, -0.14, 0.058, 0.005, 0.06, -0.016, -0.095\] |
| B   | \[0.988, 0.017, -0.068, 0.073, -0.131\] | \[0.113, 0.293, 0.401, 0.783, -0.137, -0.26, -0.097\] | \[0.974, -0.042, -0.055, -0.179, 0.05, 0.049, 0.014, 0.035, -0.087\] |
| C   | \[0.102, 0.155, 0.973, -0.084, 0.09\] | \[0.932, -0.072, -0.073, -0.188, 0.236, 0.079, 0.089\] | \[0.1, 0.138, 0.96, -0.084, 0.089, -0.022, -0.096, -0.079, -0.145\] |
| D   | \[0.089, 0.992, -0.031, -0.067, -0.072\] | \[0.067, -0.087, 0.185, -0.157, -0.179, 0.122, 0.955\] | \[0.051, 0.99, -0.099, -0.016, 0.003, -0.067, -0.032, -0.003, -0.086\] |
| E   | \[0.144, 0.975, -0.027, -0.061, -0.142\] | \[-0.13, -0.115, -0.076, -0.042, -0.094, -0.083, -0.979\] | \[0.077, 0.986, -0.094, -0.042, 0.013, -0.067, -0.036, -0.037, -0.097\] |

### Part II and III: RSA for Real - Comparing Models and Data with the rsatoolbox

The repository contains data and two Jupyter notebooks. Clone the repository, create a virtual environment, install the requirements, and then run through the notebooks.

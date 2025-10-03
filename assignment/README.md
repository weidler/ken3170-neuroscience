# Assignment 5: Modeling in Neuroscience

In this assignment, you will be using neuroanatomical data from the EBRAINS Atlases to inspire two networks, compare them to each other using RSA and optionally other methods discussed in class, and analyse whether the functional connectivity in the model after training is closer to the functional connectivity before training.

1. Use [`siibra`](https://siibra-python.readthedocs.io/en/latest/) or the [interactive viewer](https://atlases.ebrains.eu/viewer/) to explore the human, monkey, and marmoset brain, and specifically the visual system.
2. From your own review of the literature, gather the regions involved in processing visual information along both the ventral and dorsal pathway (should end up being at least 6 regions, depending on the detail you want to do) for the three species.
3. Again using siibra (via Python or interactively), for the regions you selected (you may need to map them to areas within the specific parcellation you are using), extract information about the cell density and structural connectivity to constrain the architecture of one neural network model of the visual system for each of the three species.
   1. If information is lacking, report this in your submission, and discuss and implement workarounds.
   2. Should there be generally too little data to inform your nonhuman primate models, you may choose to only implement the human model but then compare different variants.
5. Using `pytorch` (or whatever autodifferentiation library you prefer), implement three network architectures to model the human, monkey, and marmoset visual system. If you are motivated, go fancy, but we do not expect you to go deeper than a simple feedforward RELU-activated CNN with two pathways. Depending on your analysis from 3.), you may need to build skip connections and connections between the pathways, however.
6. Train the networks on a simple dataset. We suggest Fashion MNIST.
7. After training, use RSA as done previously in the practical to investigate the representational similarity between the three models. Report on whether your constraints had an influence on the performance of the networks, and the representations.
8. Measure the functional connectivity (e.g. using correlation) between the layers in your networks before and after training. Did it change? If so, how?
9. (Optional, if you have time) Compare the functional connectivity in your models to empirical data in the atlases.
10. Use t-SNE as implemented in sklearn to visualize the topology of the representational space of your models.
11. (Optional, if you have time) Use other methods discussed in class to compare the models to each other, e.g. CEBRA. This might be time-intensive, don't get too caught uup here.
12. Report on your methods, results, and conclusions in the README on GitHub and briefly document the code.

Generally, we expect you to show that you understood the methods and concepts discussed in class, and can apply them to a novel situation. We do not expect you to be able to implement state-of-the-art models or methods from scratch. If you do not manage to train your models to a good level of performance, thats odd, but not catastrophic. Report on it, and still do any analysis asked for in the assignment. We also do not expect you to do a perfect review of the literature, or make the perfect 'neuroscientific' decisions when it comes to selecting and using neuroanatomical data to build your inductive biases. If you are unsure about anything, please reach out (t.weidler@maastrichtuniversity.nl).
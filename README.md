# Encode, Attend & Navigate

## Overview

<img align="left" img src="./GitImg/Brain.png" width="75">

Tensorflow implementation of "Learning Heuristics for the TSP by Policy Gradient". <br/>
[Michel Deudon, Pierre Cournut, Alexandre Lacoste, Yossiri Adulyasak, Louis-Martin Rousseau].

## Requirements

- [Python 3.5+](https://anaconda.org/anaconda/python)
- [TensorFlow 1.3.0+](https://www.tensorflow.org/install/)
- [Tqdm](https://pypi.python.org/pypi/tqdm)

## Usage

- To train a model from scratch (data is generated on the fly), run blocks 1.DataGenerator, 2.Config, 3.Model and 4.Train with the Jupyter Notebook (Neural_Reinforce.ipynb). You can change parameters in the Config block. Default parameters should replicate results reported in our paper (2D TSP50).

- If training is successful, the model will be saved in a "save" folder (filename depends on config) and training statistics will be reported in a "summary" folder. To visualize training on tensorboard, run:
```
> tensorboard --logdir=summary
```

- To test a trained model, run block 5.Test with the Jupyter Notebook (Neural_Reinforce.ipynb).

## What is Combinatorial Optimization ?

![comic](./GitImg/Comic.png)

* __Combinatorial Optimization__: A topic that consists of finding an optimal object from a finite set of objects.
* __Sequencing problems__: The best order for performing a set of tasks must be determined.
* __Applications__: Manufacturing, routing, astrology, genetics...

Can we learn data-driven heuristics, competitive with existing man-engineered heuristics ?

## What is Deep Reinforcement Learning ?


<img align="left" img src="./GitImg/MDP.png" height="210">

* __Reinforcement Learning__: A general purpose framework for Decision Making in a scenario where a learner actively interacts with an environment to achieve a certain goal.
* __Deep Learning__: A general purpose framework for Representation Learning
* __Successful applications__: Playing games, navigating worlds, controlling physical systems and interacting with users.

## Related Work

Our work draws inspiration from [Neural Combinatorial Optimization with Reinforcement Learning](http://arxiv.org/abs/1611.09940) to solve the Euclidean TSP. Our framework gets a 5x speedup compared to the original framework, while achieving similar results in terms of optimality.

## Architecture

Following [Bello & al., 2016], our Neural Network overall parameterizes a stochastic policy over city permutations. Our model is trained by Policy Gradient ([Reinforce](https://link.springer.com/article/10.1007/BF00992696), 1992) to learn to assign high probability to "good tours", and low probability to "undesirable tours".

<p> 
  ### Neural Encoder

  <img align="left" img src="./GitImg/Encoder.png" height="150">

  Our neural encoder takes inspiration from advances in Neural Machine Translation (cite self attentive...)
  The purpose of our encoder is to obtain a representation for each action (city) given its context.

  The output of our encoder is a set of reference vectors ref = (enc1, ..., encn), each representing a city interacting with other cities.
</p>

### Neural Decoder

<img align="left" img src="./GitImg/Decoder.png" height="150">

Similar to [Bello & al., 2016], our Neural Decoder uses a Pointer (cite paper) to effectively point to a city given a trajectory. Our model however explicity forgets after K steps, dispensing with LSTM networks.

### Local Search
We use a simple 2-OPT post-processing to clean best sampled tours during test time.
One contribution we would like to emphasize here is that simple heuristics can be used in conjunction with Deep Reinforcement Learning, shedding light on interesting hybridization between Artificial Intelligence (AI) & Operations Research (OR).

## Results

![results](./GitImg/Results.png)

![tsp100](./GitImg/TSP100.png)

We evaluate on TSP100 our model pre-trained on TSP50 and the results show that that it performs relatively well even though the model was not trained directly on the same instance size as in [Bello & al, 2016]. We believe that the Markov assumption (see Decoder) helps generalizing the model.

## Acknowledgments
[add links]

Ecole Polytechnique (l'X), Polytechnique Montreal and CIRRELT for financial & logistic support
Element AI for hosting weekly meetings
Compute Canada & Télécom Paris-Tech for computational resources.

Special thanks (sorted by name)
Pr. Alessandro Lazaric (SequeL Team, INRIA Lille)
Dr. Alexandre Lacoste (Element AI)
Pr. Claudia D'Ambrosio (CNRS, LIX)
Diane Bernier
Dr. Khalid Laaziri
Pr. Leo Liberti (CNRS, LIX)
Pr. Louis-Martin Rousseau (Polytechnique Montreal)
Magdalena Fuentes (Télécom Paris-Tech)
Mehdi Taobane
Pierre Cournut (Ecole Polytechnique)
Pr. Yossiri Adulyasak (HEC Montreal)


## Author
Michel Deudon / [@mdeudon](https://github.com/MichelDeudon)

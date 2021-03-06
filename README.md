<!-- Logo -->
<p align="center">
   <img src="assets/logo_wide.svg" width="50%">
</p>

<!-- Short description -->
<p align="center">
   A Reinforcement Learning Library for Research and Education
</p>

<!-- The badges -->
<p align="center">
   <a href="https://github.com/rlberry-py/rlberry/workflows/test/badge.svg">
      <img alt="pytest" src="https://github.com/rlberry-py/rlberry/workflows/test/badge.svg">
   </a>
   <a href='https://rlberry.readthedocs.io/en/latest/?badge=latest'>
      <img alt="Documentation Status" src="https://readthedocs.org/projects/rlberry/badge/?version=latest">
   </a>
   <a href="https://img.shields.io/github/contributors/rlberry-py/rlberry">
      <img alt="contributors" src="https://img.shields.io/github/contributors/rlberry-py/rlberry">
   </a>
   <a href="https://app.codacy.com/gh/rlberry-py/rlberry?utm_source=github.com&utm_medium=referral&utm_content=rlberry-py/rlberry&utm_campaign=Badge_Grade">
      <img alt="Codacy" src="https://api.codacy.com/project/badge/Grade/27e91674d18a4ac49edf91c339af1502">
   </a>
   <a href="https://codecov.io/gh/rlberry-py/rlberry">
      <img alt="codecov" src="https://codecov.io/gh/rlberry-py/rlberry/branch/main/graph/badge.svg?token=TIFP7RUD75">
   </a>
   <a href="https://pypi.org/project/rlberry/">
      <img alt="PyPI" src="https://img.shields.io/pypi/v/rlberry">
   </a>
</p>

<p align="center">
   <a href="https://colab.research.google.com/github/rlberry-py/rlberry/blob/main/notebooks/introduction_to_rlberry.ipynb">
      <b>Try it on Google Colab!</b>
      <img alt="Open In Colab" src="https://colab.research.google.com/assets/colab-badge.svg">
   </a>
</p>

<!-- Horizontal rule -->
<hr>

<!-- Table of content -->

| Section | Description |
|-|-|
| [Introduction](#introduction) | The philosophy of `rlberry` |
| [Getting started](#getting-started) | A quick usage guide of `rlberry` |
| [Installation](#installation) | How to install `rlberry` |
| [Documentation](#documentation) | A link to the documentation |
| [Contributing](#contributing) | A guide for contributing |
| [Citation](#citing-rlberry) | How to cite this work |

## Introduction

The goal of `rlberry`to make **Reinforcement Learning** (RL) research and teaching easier. For that purpose, `rlberry` provides several interfaces that allow users to create their own experimental pipeline in a fast, clear and reproducible way. `rlberry` comprises the following major components and main features:

*   An interface for agents, that
    *   puts minimal constraints on the agent code (=> making it easy to include new algorithms and modify existing ones);

    *   allows comparison between agents using a simple and unified evaluation interface (=> making it easy, for instance, to compare deep and "traditional" RL algorithms);

    *   includes detailed documentation and comprehensible tutorial/examples (Jupyter Notebook) for each implemented agents (=> making it easy for education).

*   An interface for environments, that
    *   allows to create novel environments easily (=> making it possible to add your own environments);

    *   totally adapts to [`OpenAI Gym`](https://gym.openai.com/) (=> making it easy to use any existing environments from `gym`).

*   An interface for rendering, that
    *   provides simple and clear visualization of your experiments.

*   Several important features include
    *   a unified seeding mechanism: define only one global seed, from which all other seeds will inherit, enforcing independence of the random number generators;

    *   an interface to [`Optuna`](https://optuna.org/) that allows automatic hyperparameter optimization;

    *   compatibility with [`Sacred`](https://sacred.readthedocs.io/en/stable/quickstart.html) that facilitates configuration, organization, logging and reproducing of computational experiments.

<p align="center">
   <img src="assets/rlberry.svg" width="70%">
</p>


## Getting started

We provide a handful of notebooks on [Google colab](https://colab.research.google.com/) as examples to show you how to use `rlberry`.

| Content | Description | Link |
|-|-|-|
| Introduction to `rlberry` | How to create an agent, optimize its hyperparameters and compare to a baseline. | <a href="https://colab.research.google.com/github/rlberry-py/rlberry/blob/main/notebooks/introduction_to_rlberry.ipynb"><img alt="Open In Colab" src="https://colab.research.google.com/assets/colab-badge.svg"></a> |
| RL Experimental Pipeline | How to define a configuration, run experiments in parallel and save a `config.json` for reproducibility. | <a href="https://colab.research.google.com/github/rlberry-py/rlberry/blob/main/notebooks/experimental_pipeline_with_rlberry.ipynb"><img alt="Open In Colab" src="https://colab.research.google.com/assets/colab-badge.svg"></a> |


### Compatibility with [OpenAI Gym](https://gym.openai.com/)

If you want to use `gym` environments with `rlberry`, simply do the following:

```python
from rlberry.envs import gym_make

# for example, let's take CartPole
env = gym_make('CartPole-v1')
```

This way, `env` behaves exactly the same as the `gym` environment, we simply replace the seeding function by `env.reseed()`, which ensures unified seeding and reproducibility when using `rlberry`.


### Seeding 

In `rlberry`, __only one global seed__ is defined, and all the random number generators used by the agents and environments inherit from this seed, ensuring __reproducibility__  and __independence between the generators__ (see [NumPy SeedSequence](https://numpy.org/doc/stable/reference/random/parallel.html)).

Example:

```python
import rlberry.seeding as seeding

seeding.set_global_seed(seed=123)

# From now on, no more seeds are defined by the user, and all the results are reproducible.
...

# If you need a random number generator (rng), call:
rng = seeding.get_rng()   

# which gives a numpy Generator (https://numpy.org/doc/stable/reference/random/generator.html) 
# that is independent of all the previous generators created by seeding.get_rng()
rng.integers(5)
rng.normal()
# etc

```

## Installation

### Cloning & creating virtual environment

It is suggested to create a virtual environment using Anaconda or [Miniconda](https://docs.conda.io/en/latest/miniconda.html):

```bash
git clone https://github.com/rlberry-py/rlberry.git
conda create -n rlberry python=3.7
```

### Basic installation

Install without heavy libraries (e.g. pytorch):

```bash
conda activate rlberry
pip install -e .
```

### Full installation

Install with all features:

```bash
conda activate rlberry
pip install -e .[full]
```

which includes:

*   [`Numba`](https://github.com/numba/numba) for just-in-time compilation of algorithms based on dynamic programming
*   [`PyTorch`](https://pytorch.org/) for Deep RL agents
*   [`Optuna`](https://optuna.org/#installation) for hyperparameter optimization
*   [`Sacred`](https://github.com/IDSIA/sacred) for handling experiment configurations
*   [`ffmpeg-python`](https://github.com/kkroening/ffmpeg-python) for saving videos
*   [`PyOpenGL`](https://pypi.org/project/PyOpenGL/) for more rendering options

### Tests

To run tests, install test dependencies with `pip install -e .[test]` and run `pytest`. To run tests with coverage, install test dependencies and run `bash run_testscov.sh`. See coverage report in `cov_html/index.html`.

## Documentation

The documentation is under construction and will be available [here](https://rlberry.readthedocs.io/en/latest/).

## Contributing

Want to contribute to `rlberry`? Please check [our contribution guidelines](CONTRIBUTING.md). A list of interesting TODO's will be available soon. **If you want to add any new agents or environments, do not hesitate to [open an issue](https://github.com/rlberry-py/rlberry/issues/new/choose)!**

### Implementation notes

*   When inheriting from the `Agent` class, make sure to call `Agent.__init__(self, env, **kwargs)` using `**kwargs` in case new features are added to the base class, and to make sure that `copy_env` and `reseed_env` are always an option to any agent. 

Infos, errors and warnings are printed using the `logging` library.

*   From `gym` to `rlberry`:
    *   `reseed` (rlberry) should be called instead of `seed` (gym). `seed` keeps compatilibity with gym, whereas `reseed` uses the unified seeding mechanism of `rlberry`.

## Citing rlberry

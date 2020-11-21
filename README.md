<img src="logo/logo_wide.svg" width="50%">

# A Reinforcement Learning Library for Research and Education 

![pytest](https://github.com/rlberry-py/rlberry/workflows/test/badge.svg)

# Goals

* Write detailed documentation and comprehensible tutorial/examples (Jupyter Notebook) for each implemented algorithm.
* Provide a general interface for agents, that
    * puts minimal constraints on the agent code (=> making it easy to include new algorithms and modify existing ones);
    * allows comparison between agents using a simple and unified evaluation interface (=> making it easy, for instance, to compare deep and "traditional" RL algorithms).
* Unified seeding mechanism: define only one global seed, from which all other seeds will inherit, enforcing independence of the random number generators.
* Simple interface for creating and rendering new environments. 


# Install

To install rlberry on your own device, first create a virtual environment using Anaconda or [Miniconda](https://docs.conda.io/en/latest/miniconda.html) (suggested):

```
conda create -n rlberry python=3.7
conda activate rlberry
git clone https://github.com/rlberry-py/rlberry.git
pip install -e .
```

Or you can also install directly (not suggested):

```
git clone https://github.com/rlberry-py/rlberry.git
python3 -m pip install -e .
```

# Optional dependencies

* For saving videos: [ffmpeg-python](https://github.com/kkroening/ffmpeg-python) 
```
pip install ffmpeg-python
```

* For hyperparameter optimization: [optuna](https://optuna.org/#installation)
```
pip install optuna
```


# Tests

To run tests, run `pytest`. To run tests with coverage, install and run `pytest-cov`:

```
pip install pytest-cov
bash run_tests.sh
```

See coverage report in `cov_html/index.html`.



# Implementation notes

* When inheriting from the `Agent` class, make sure to call `Agent.__init__(self, env, **kwargs)` using `**kwargs` in case new features are added to the base class, and to make sure that `copy_env` and `reseed_env` are always an option to any agent. 

* Convention for verbose in the agents:
    * `verbose=0`: nothing is printed
    * `verbose>1`: print progress messages

Errors and warnings are printed using the `logging` library.

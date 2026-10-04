# Hands-On Machine Learning with Scikit-Learn and PyTorch

The goal of this project is to teach you the fundamentals of Machine Learning in Python. It contains the example code and solutions to the exercises in the first edition of my new O'Reilly book [Hands-on Machine Learning with Scikit-Learn and PyTorch (1st edition)](https://homl.info/):

<a href="https://homl.info/er"><img src="https://www.oreilly.com/covers/urn:orm:book:9798341607972/400w/" title="book" width="150" border="0" /></a>

**Note**: If you are looking for the notebooks for the TensorFlow/Keras version of this book, check out [ageron/handson-ml3](https://github.com/ageron/handson-ml3).
**Note**: If you prefer [Polars](https://pola.rs/) over Pandas, check out [PGupta-Git/handson-mlp (polars branch)](https://github.com/PGupta-Git/handson-mlp/tree/polars_integration), a community-maintained Polars version of this project (see [#23](https://github.com/ageron/handson-mlp/issues/23)).

## Quick Start

### Want to play with these notebooks online without having to install anything?

- <a href="https://colab.research.google.com/github/ageron/handson-mlp/blob/main/" target="_parent"><img src="https://colab.research.google.com/assets/colab-badge.svg" alt="Open In Colab"/></a> (recommended)

⚠ _Colab provides a temporary environment: anything you do will be deleted after a while, so make sure you download any data you care about._

### Just want to quickly look at some notebooks, without executing any code?

- <a href="https://nbviewer.jupyter.org/github/ageron/handson-mlp/blob/main/index.ipynb"><img src="https://raw.githubusercontent.com/jupyter/design/master/logos/Badges/nbviewer_badge.svg" alt="Render nbviewer" /></a>

- [github.com's notebook viewer](https://github.com/ageron/handson-mlp/blob/main/index.ipynb) also works but it's not ideal: it's slower, the math equations are not always displayed correctly, and large notebooks often fail to open.

### Want to install this project on your own machine?

Check out the [installation instructions](INSTALL.md).


# FAQ

**Which Python version should I use?**

I recommend Python 3.12. If you follow the installation instructions above, that's the version you will get. Versions 3.10 and 3.11 should work as well, but some libraries are not yet available for 3.13.

**I'm getting an error when I call `load_housing_data()`**

If you're getting an HTTP error, make sure you're running the exact same code as in the notebook (copy/paste it if needed). If the problem persists, please check your network configuration. If it's an SSL error, see the next question.

**I'm getting an SSL error on MacOSX**

You probably need to install the SSL certificates (see this [StackOverflow question](https://stackoverflow.com/questions/27835619/urllib-and-ssl-certificate-verify-failed-error)). If you downloaded Python from the official website, then run `/Applications/Python\ 3.12/Install\ Certificates.command` in a terminal (change `3.12` to whatever version you installed). If you installed Python using MacPorts, run `sudo port install curl-ca-bundle` in a terminal.

**I've installed this project locally. How do I update it to the latest version?**

See [INSTALL.md](INSTALL.md)

**How do I update my Python libraries to the latest versions, when using Anaconda?**

See [INSTALL.md](INSTALL.md)

## Contributors

I would like to thank everyone [who contributed to this project](https://github.com/ageron/handson-mlp/graphs/contributors), either by providing useful feedback, filing issues or submitting Pull Requests.

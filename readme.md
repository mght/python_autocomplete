[![PyPI - Python Version](https://badge.fury.io/py/labml-python-autocomplete.svg)](https://badge.fury.io/py/labml-python-autocomplete)
[![PyPI Status](https://pepy.tech/badge/labml-python-autocomplete)](https://pepy.tech/project/labml-python-autocomplete)
[![Join Slack](https://img.shields.io/badge/slack-chat-green.svg?logo=slack)](https://join.slack.com/t/labforml/shared_invite/zt-egj9zvq9-Dl3hhZqobexgT7aVKnD14g/)
[![Twitter](https://img.shields.io/twitter/follow/labmlai?style=social)](https://twitter.com/labmlai?ref_src=twsrc%5Etfw)

# Python Autocomplete

[This](https://github.com/lab-ml/python_autocomplete) project try autocompleting python
source code using LSTM or Transformer models.

Training model: [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/lab-ml/python_autocomplete/blob/master/notebooks/train.ipynb)

Evaluating trained model: [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/lab-ml/python_autocomplete/blob/master/notebooks/evaluate.ipynb)

It gives quite decent results by saving above 30% key strokes in most files,
and close to 50% in some. We calculated key strokes saved by making a single (best)
prediction and selecting it with a single key.

The dataset we use is the python code found in repos linked in
[Awesome-pytorch-list](https://github.com/bharathgs/Awesome-pytorch-list).
We download all the repositories as zip files, extract them, remove non python files and split them
randomly to build training and validation datasets.

We train a character level model without any tokenization of the source code, since it's the simplest.

### Try it yourself

1. Clone this repo
2. Install requirements from `requirements.txt`
3. Run `python_autocomplete/create_dataset.py`. 
   * It collects repos mentioned in
 [PyTorch awesome list](https://github.com/bharathgs/Awesome-pytorch-list)
   * Downloads the zip files of the repos
   * Extract the zips
   * Remove non python files
   * Collect all python code to `data/train.py` and, `data/eval.py`
4. Run `python_autocomplete/train.py` to train the model.
 *Try changing hyper-parameters like model dimensions and number of layers*.
5. Run `evaluate.py` to evaluate the model.

You can also run the training notebook on Google Colab.

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/lab-ml/python_autocomplete/blob/master/notebooks/train.ipynb)
 
### Sample

Here's a sample evaluation of a trained transformer model.

Colors:
* <span style="color:yellow">yellow</span>: the token predicted is wrong and the user needs to type that character.
* <span style="color:blue">blue</span>: the token predicted is correct and the user selects it with a special key press, such as TAB or ENTER.
* <span style="color:green">green</span>: autocompleted characters based on the prediction

<p align="center">
  <img src="/images/python-autocomplete.png?raw=true" width="100%" title="Screenshot">
</p>

We are working on a simple extension for VSCode for demonstration.

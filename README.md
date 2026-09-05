Udacity _HMM Tagger_ project: a hidden Markov model for part-of-speech tagging with a universal tagset, trained on the Brown corpus and compared against a most-frequent-class baseline.

I also included an AI-generated cheat sheet on [Probabilistic Graphical Models](cheat-sheet-probalistic-graphical-models.md) in case you need a refresher on these topics.

Setup with [uv](https://docs.astral.sh/uv/): `uv venv --python 3.13 venv && source venv/bin/activate && uv pip install -r requirements.txt`. The notebooks use an older Pomegranate HMM API. That is why pomegranate is pinned to version 0.15.0. Otherwise it will error out.

Open the project notebook with `jupyter notebook "HMM Tagger.ipynb"`. Graph drawing in the helpers needs [GraphViz](https://graphviz.org/) installed separately.

Udacity also provided a small warmup notebook (`HMM warmup (optional).ipynb`); I left it as-is.

Starter code is from Udacity (MIT License).

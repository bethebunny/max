# TorchScript BERT Inference

This directory includes scripts used to run simple BERT inference via the MAX
Python API to predict the sentiment of the given text.

## Quickstart

```sh
python3 -m venv venv && source venv/bin/activate
python3 -m pip install --upgrade pip setuptools
python3 -m pip install -r requirements.txt
# Install the MAX Engine Python package
python3 -m pip install --find-links "$(modular config max.path)/wheels" max-engine
# Run the MAX Engine example
bash run.sh
# Run the MAX Serving example
bash deploy.sh
```

## Scripts Included

- `download-model.py`
    Downloads the model from HuggingFace, converts it to `TorchScript` format,
    and saves it to the current directory. The script also produces inputs for
    the model from the provided input sentence.

    For more information about the model, reference the [model card](https://huggingface.co/bert-base-uncased).

    Usage: `python3 download-model.py --text=<masked text>`.

- `simple-inference.py`
    Classifies example input text using the MAX Engine. The script prepares an
    example input, executes the model, and generates the classification
    result.

    You can use the `--text` CLI flag to specify an input sentence.
    For example, `python3 simple-inference.py --text "There are many exciting developments in the field of AI Infrastructure!"`

- `triton-inference.py`
    Classifies example input text using the MAX Serving. The script launches a Triton container, prepares an example input, executes the model by calling HTTP inference endpoint, and returns the classification result.

    You can use the `--input` CLI flag to specify an input example.
    For example, `python3 triton-inference.py --input="There are many exciting developments in the field of AI Infrastructure!"`.

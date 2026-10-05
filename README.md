# RNN Movie Sentiment Analysis

A deep learning project that uses a **Simple Recurrent Neural Network (SimpleRNN)** with TensorFlow/Keras to classify IMDB movie reviews as **Positive** or **Negative**. The trained model is exposed through an interactive **Streamlit** web application.

## Project Overview

This project uses the IMDB movie-review dataset provided by `tensorflow.keras.datasets.imdb`.

## Live App

[View the App](https://rnn-movies-sentimenment-analysis-ekwxewtchfeudymnfyrafh.streamlit.app/)


The workflow is:

1. Load the IMDB dataset.
2. Use a vocabulary size of 10,000 words.
3. Pad reviews to a maximum length of 500 tokens.
4. Convert token sequences through an Embedding layer.
5. Process the sequences using a SimpleRNN layer.
6. Use a sigmoid output layer for binary sentiment classification.
7. Train with Adam and binary cross-entropy.
8. Use EarlyStopping to restore the best validation weights.
9. Save the trained model as `simple_rnn_imdb.h5`.
10. Use Streamlit to accept a movie review and display its predicted sentiment and score.

## Model Architecture

The model is a SimpleRNN-based binary classifier:

```text
Input Review
     ↓
Embedding
(vocabulary: 10,000, embedding dimension: 128)
     ↓
SimpleRNN
(128 units, ReLU activation)
     ↓
Dense
(1 unit, Sigmoid activation)
     ↓
Positive / Negative
```

### Model Configuration

| Component | Configuration |
|---|---|
| Dataset | IMDB |
| Vocabulary size | 10,000 |
| Maximum sequence length | 500 |
| Embedding dimension | 128 |
| RNN units | 128 |
| RNN activation | ReLU |
| Output activation | Sigmoid |
| Optimizer | Adam |
| Loss | Binary Cross-Entropy |
| Batch size | 32 |
| Maximum epochs | 7 |
| Validation split | 20% |
| Early stopping | Patience = 5 |
| Saved model | `simple_rnn_imdb.h5` |

The model contains **1,313,025 trainable parameters**.

## Training Results

The model was trained for 7 epochs with early stopping configured to monitor validation loss and restore the best weights.

From the recorded training run:

| Epoch | Training Accuracy | Validation Accuracy |
|---:|---:|---:|
| 1 | 81.59% | 77.12% |
| 2 | 80.11% | 74.18% |
| 3 | 84.42% | 74.60% |
| 4 | 88.67% | 77.56% |
| 5 | 91.55% | 78.44% |
| 6 | 94.09% | **80.36%** |
| 7 | 95.99% | 79.18% |

The highest recorded validation accuracy was **80.36% at epoch 6**.

> Note: The project files contain training/validation results, but no separate test-set evaluation result is recorded.

## Prediction Pipeline

For a user-entered review:

1. Convert the text to lowercase.
2. Split the review into words.
3. Map words to the IMDB word-index values.
4. Assign unknown words the configured unknown-token index.
5. Pad the sequence to 500 tokens.
6. Pass the processed review to the trained model.
7. If the prediction score is greater than `0.5`, classify it as **Positive**; otherwise classify it as **Negative**.

## Streamlit Application

The Streamlit application provides:

- A movie-review text area.
- A **Classify** button.
- Predicted sentiment.
- Prediction score.

The application title is:

**IMDB Movie Review Sentiment Analysis**

## Project Structure

```text
RNN-Movies-Sentimement-Analysis/
│
├── main.py
├── simple_rnn_imdb.h5
├── requirements.txt
├── prediction.ipynb
└── simplernn.ipynb
```

### File Description

- **`main.py`** — Streamlit application and prediction logic.
- **`simple_rnn_imdb.h5`** — Trained SimpleRNN model.
- **`requirements.txt`** — Python dependencies required by the project.
- **`prediction.ipynb`** — Loads the trained model and demonstrates prediction on an example review.
- **`simplernn.ipynb`** — End-to-end model development and training notebook.

## Installation

Clone the repository:

```bash
git clone https://github.com/Altamash0078600/RNN-Movies-Sentimement-Analysis.git
cd RNN-Movies-Sentimement-Analysis
```

Create and activate a virtual environment:

### Windows

```powershell
python -m venv venv
.env\Scriptsctivate
```

Install the dependencies:

```bash
pip install -r requirements.txt
```

## Run the Streamlit App

Run:

```bash
streamlit run main.py
```

The application will open in your browser.

## Example

Input:

```text
This movie was fantastic! The acting was great and the plot was thrilling.
```

The application returns:

```text
Sentiment: Positive
Prediction Score: <model score>
```

## Technologies Used

- Python
- TensorFlow
- Keras
- NumPy
- Pandas
- Scikit-learn
- Matplotlib
- TensorBoard
- Streamlit
- Scikeras

## Future Improvements

- Evaluate the model on the IMDB test set and report test accuracy.
- Experiment with LSTM and GRU architectures.
- Compare SimpleRNN, LSTM, and GRU performance.
- Improve text preprocessing and tokenization.
- Add confidence/probability visualization to the Streamlit interface.
- Improve the UI with review examples and prediction history.

## Author

**Altamash Siddquie**

This project was developed as an end-to-end deep learning and NLP project using a SimpleRNN for movie-review sentiment classification.

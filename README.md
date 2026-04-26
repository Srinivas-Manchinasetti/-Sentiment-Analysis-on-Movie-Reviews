🎬 IMDB Sentiment Analysis — LSTM vs Fine-Tuned DistilBERT

A comparative sentiment analysis project on the IMDB movie reviews dataset, implementing two deep learning approaches: an improved Bidirectional LSTM and a fine-tuned DistilBERT transformer. Built and trained on Google Colab with a T4 GPU.

📌 Project Overview
This project classifies movie reviews as Positive or Negative using two models:

Part A — Bidirectional LSTM (TensorFlow/Keras): A classic deep learning approach with improved architecture — larger vocabulary, bidirectional layers, and training callbacks.
Part B — Fine-Tuned DistilBERT (PyTorch + HuggingFace Transformers): A pretrained transformer model fine-tuned on IMDB review data.
Part C — Comparison: A side-by-side evaluation of both models on the same 1,000 test samples, with a bar chart visualizing their accuracy.


📁 Repository Structure
├── Sentiment_Analysis_Fixed.ipynb   # Main Colab notebook (all steps)
└── README.md

🗃️ Dataset

Source: IMDB Dataset via HuggingFace datasets
Total samples: 50,000 movie reviews (25k train + 25k test)
Split used: 40,000 train / 10,000 test (via train_test_split with random_state=42)
Labels: Binary — 0 (Negative), 1 (Positive)


🧠 Models
Part A — Improved Bidirectional LSTM
ParameterValueVocabulary size20,000Max sequence length200 tokensEmbedding dim128ArchitectureBidirectional LSTM (128) → Dropout → Bidirectional LSTM (64) → Dropout → DenseOptimizerAdamLossBinary CrossentropyEpochsUp to 5 (EarlyStopping on val_loss)Batch size64CallbacksEarlyStopping, ReduceLROnPlateau
Key improvements over baseline:

Vocabulary size increased from 5,000 → 20,000
Max sequence length increased from 100 → 200
Upgraded from a single LSTM to stacked Bidirectional LSTMs
Added EarlyStopping and ReduceLROnPlateau for better convergence


Part B — Fine-Tuned DistilBERT
ParameterValueBase modeldistilbert-base-uncasedTraining samples10,000Eval samples1,000Max token length256OptimizerAdamW (lr=2e-5, weight_decay=0.01)SchedulerLinear warmup (10% of steps)Epochs3Batch size16Gradient clippingmax_norm=1.0

📊 Results
Both models are evaluated on the same 1,000 test samples for a fair comparison:
ModelAccuracyBidirectional LSTM~88–90%Fine-Tuned DistilBERT~92–93%

Exact values will vary slightly per run. DistilBERT consistently outperforms the LSTM due to its pretraining on large-scale text corpora and attention-based contextual understanding.


⚙️ Setup & Usage
Requirements
bashpip install transformers datasets tensorflow scikit-learn matplotlib torch accelerate
Running the Notebook

Open Sentiment_Analysis_Fixed.ipynb in Google Colab
Set runtime to T4 GPU: Runtime → Change runtime type → T4 GPU
Run all cells sequentially (Steps 1–17)


⚠️ Runtime warning: The full notebook takes approximately 2–3 hours on a T4 GPU. The DistilBERT fine-tuning loop (Step 14) is the most time-intensive — plan accordingly within Colab's session limits.


🧪 Custom Review Testing
Step 17 lets you test both models on custom reviews side by side:
=======================================================
Review                              LSTM         DistilBERT
=======================================================
This movie was fantastic and thr... Positive ✅  Positive ✅
Absolutely terrible. Waste of ti... Negative ❌  Negative ❌
One of the best films I have eve... Positive ✅  Positive ✅
=======================================================

🛠️ Tech Stack
ToolPurposePython 3Core languageTensorFlow / KerasLSTM modelPyTorchDistilBERT training loopHuggingFace TransformersDistilBERT model & tokenizerHuggingFace DatasetsIMDB dataset loadingscikit-learnTrain/test split, accuracy metricMatplotlibTraining curves & comparison chartGoogle Colab (T4 GPU)Training environment

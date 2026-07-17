This project is an English-to-Hindi Neural Machine Translation system. It accepts an English sentence and generates its corresponding Hindi translation using two different deep-learning approaches.

Main objective

The objective is to study and implement machine translation using:

A pretrained transformer model called mBART
A custom LSTM encoder–decoder model trained on English–Hindi sentence pairs

This makes the project both an implementation and a comparison of traditional sequence-to-sequence learning with modern transformer-based translation.

Dataset

The notebook uses:

Hindi_English_Truncated_Corpus.csv

Its main columns are:

english_sentence: source English sentence
hindi_sentence: corresponding Hindi translation

Each English sentence and Hindi sentence together form a parallel translation pair.

Project workflow
1. Exploratory data analysis

The notebook initially examines the dataset through:

First and last records
Dataset dimensions and column information
Missing-value analysis
Sentence-length analysis
Character and token counts
Most frequently occurring English and Hindi words
Statistical and graphical exploration

Missing sentence pairs are removed before training.

2. Text preprocessing

The English and Hindi sentences are cleaned by:

Converting text into a consistent format
Removing English and Hindi digits
Removing punctuation
Removing unnecessary spaces
Stripping leading and trailing spaces
Limiting sentences according to their length
Adding START_ and _END markers to Hindi sentences

The start and end markers help the decoder determine when translation generation should begin and stop.

3. Vocabulary preparation

Separate vocabularies are created for English and Hindi.

Each word is assigned a numerical index:

English word → input token index
Hindi word → target token index

Reverse dictionaries are also created to convert the model’s numeric output back into Hindi words.

4. Training and testing split

The processed English–Hindi sentence pairs are divided into training and testing datasets.

A batch generator prepares:

Encoder input sequences
Decoder input sequences
Expected decoder output sequences

This enables teacher-forcing-based training of the LSTM model.

Translation approach 1: mBART

The project loads:

facebook/mbart-large-50-one-to-many-mmt

mBART is a pretrained multilingual transformer developed for translation and text-generation tasks.

In the notebook:

English is configured using en_XX.
Hindi is selected using hi_IN.
English sentences are tokenized.
mBART generates Hindi token sequences.
Generated tokens are converted back into readable Hindi text.

The current notebook uses the pretrained mBART model for inference. It does not appear to fine-tune mBART on the project dataset.

Translation approach 2: LSTM encoder–decoder

The second approach builds a translation model from scratch.

Encoder

The encoder:

Receives the numerical English sentence.
Converts words into embeddings.
Processes the sequence through an LSTM layer.
Produces hidden and cell states representing the sentence.
Decoder

The decoder:

Receives the Hindi start token.
Uses the encoder’s hidden and cell states.
Predicts the next Hindi word.
Feeds the predicted word back into itself.
Continues until _END or the maximum length is reached.

A Softmax output layer calculates the probability of each possible Hindi word.

Project output

For sample records, the notebook displays:

Input English sentence
Actual Hindi translation
Predicted Hindi translation

This allows a direct comparison between the reference translation and the model-generated translation.

Technologies used
Python
TensorFlow and Keras
Hugging Face Transformers
mBART
LSTM
Pandas and NumPy
Scikit-learn
FastEDA
Plotly and Cufflinks
SentencePiece
Strengths
Includes both transformer and LSTM approaches
Covers the complete NLP pipeline
Performs dataset exploration and cleaning
Implements custom batch generation
Builds separate training and inference models
Demonstrates real English-to-Hindi translations
Provides a good academic introduction to neural machine translation
Current limitations
mBART is used as a pretrained model but is not fine-tuned.
The notebook does not provide a formal BLEU or chrF evaluation.
The LSTM model may have difficulty with long sentences.
Word-level tokenization can struggle with unseen words.
Translation quality depends heavily on dataset quality and size.
Only a small number of predictions are manually demonstrated.
The notebook requires significant RAM/GPU resources, especially for mBART.
Overall conclusion

Overall, this project is a comparative English-to-Hindi machine translation prototype. It demonstrates how translation can be performed using both a pretrained multilingual transformer and a custom LSTM sequence-to-sequence architecture.

For a stronger research project, the next important improvements would be to fine-tune mBART, add attention or beam search to the LSTM model, and evaluate both approaches using BLEU, chrF and human evaluation.

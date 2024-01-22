# Llama Homograph Disambiguation (HD) Dataset

This repository provides a balanced dataset for training and evaluating
English homograph disambiguation (HD) models, generated with Meta's
Llama 2-Chat 70B model.

The dataset contains 3,260 sentences covering the same set of 162 homograph
words as in Google's [Wikipedia HD
dataset](https://github.com/google-research-datasets/WikipediaHomographData).
Most words have two pronunciations; two words (`august` and `mobile`) have
three. For each pronunciation of each homograph word, this dataset contains
10 sentences in which the homograph word occurs exactly once. The 10 sentences
are divided evenly into a training set and an evaluation set.

This dataset is intended to be **balanced** and **diverse**:

* Each pronunciation of each homograph word gets the same number of sentences.
  This is unlike Google's Wikipedia HD dataset, in which some pronunciations
  get very few or no sentences at all.
* For each pronunciation of each homograph, we tried to capture as many word
  senses as possible. We also ensured the sentences come from diverse domains
  (e.g. math, chemistry, linguistics), and the homograph words play different
  roles in a sentence (e.g. as the subject or the object; in the main clause or
  a relative clause).

## Data Format

The dataset comes in two files: `llama_hd_train.tsv` and `llama_hd_eval.tsv`.
Each file contains five fields, separated by a tab:

* `homograph`: The homograph word, in lower case.
* `wordid`: A string identifying a pronunciation of the homograph word. For the
  full list of wordids, see [`wordids.tsv`](https://github.com/google-research-datasets/WikipediaHomographData/blob/master/data/wordids.tsv)
  in the repo of the Wikipedia dataset.
* `sentence`: A sentence containing the homograph word exactly once.
* `start`, `end`: The start and end indices of the homograph word in the
  sentence.

**Notes:**

1. All the fields are enclosed in double quotes (`"`), and double quotes within
   the fields are escaped as two double quotes (`"`). You can read and unescape
   the fields in Python using `csv.reader(..., delimiter="\t", quotechar='"')`.
2. The homograph word in the sentence may be capitalized, have surrounding
   punctuations, take the possessive suffix (`'s`), or be part of a hyphenated
   word (e.g. `lead-free`). You need to make sure your tokenizer can treat the
   homograph word itself as a token.
3. The `start` and `end` indices aren't really necessary, since the homograph
   word always occurs only once in the sentence. They are included to be
   consistent with the Wikipedia dataset. Note that the indices are counted in
   **UTF-8 bytes**, not Unicode characters, e.g. `é` (`C3 A9` in UTF-8) counts
   as two bytes.

## License

This dataset is released under the Creative Commons Attribution Non-Commercial
(CC-BY-NC) 4.0 license.

This dataset is only intended for training models for homograph disambiguation
(HD) and related elementary NLP tasks, such as text normalization (TN) and POS
tagging.

## Citing

If you use this data in a publication, please cite the following paper:

Wonjune Kang, Yun Wang, Shun Zhang, Arthur Hinsvark, Qing He. [Multi-task
learning for front-end text processing in TTS](https://arxiv.org/pdf/2401.06321.pdf).
In _Proceedings of the 2024 IEEE International Conference on Acoustics,
Speech, and Signal Processing (ICASSP)_, Seoul, Korea, April 2024.

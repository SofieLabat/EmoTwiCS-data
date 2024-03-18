# EmoTwiCS data
[![CC BY-NC-SA 4.0][cc-by-nc-sa-shield]][cc-by-nc-sa]

## Table of Contents
1. Location
2. Overview
3. Citation
4. Data structure
5. License
6. Contact

## 1. Location
__The EmoTwiCS dataset described in this README.md is permanently relocated to https://lt3.ugent.be/resources/emotwics/.__

## 2. Overview
EmoTwiCS is a corpus of 9,489 Dutch customer service dialogues that were scraped from Twitter. In our business-oriented corpus, we view emotions as dynamic attributes of the customer that can change at each utterance of the conversation. EmoTwiCS is annotated for:
- fine-grained _emotions_ experienced by customers which are annotated with:
  - 28 emotion labels, 
  - 9 emotion clusters,
  - valence scores on a 5-point scale,
  - arousal scores on a 5-point scale,
  - dominance scores on a 5-point scale.
- the _cause_ of the conversation, namely the event happening prior to the interaction that causes a customer to contact the company. If a conversation has a cause, it is annotated with one of 8 categories.
- _responses strategies_ used by the company operator which are annotated with 8 categories (multilabel setup).

For more details, we refer interested parties to the two papers in the next section.

## 3. Citation
If you use this dataset in your work, please cite the following two papers. We also refer interested parties to these papers to learn more about the corpus.

Paper introducing the EmoTwiCS dataset:
```
@article{Labat-etal-2023,
  author       = {Sofie Labat and Thomas Demeester and Véronique Hoste},
  title        = {{EmoTwiCS}: a corpus for modelling emotion trajectories in {D}utch customer service dialogues on {T}witter},
  journal      = {Language Resources and Evaluation},
  month        = {dec},
  year         = {2023},
  issn         = {1574-020X},
  pages        = {42},
  publisher    = {Springer},
  doi          = {10.1007/s10579-023-09700-0},
  url          = {http://doi.org/10.1007/s10579-023-09700-0},
}
```

Paper releasing the first ML baselines for EmoTwiCS:
```
@inproceedings{Labat-etal-2022,
  author       = {Sofie Labat and Amir Hadifar and Thomas Demeester and V{é}ronique Hoste},
  title        = {An Emotional Journey: Detecting Emotion Trajectories in {D}utch Customer Service Dialogues},
  booktitle    = {Proceedings of the Eighth Workshop on Noisy User-generated Text ({W-NUT} 2022)},
  month        = {oct},
  year         = {2022},
  address      = {Gyeongju, Republic of Korea},
  publisher    = {Association for Computational Linguistics},
  url          = {https://aclanthology.org/2022.wnut-1.12},
  pages        = {106--112},
}
```

## 4. Data Structure
The dataset EmoTwiCS is structured as a collection of conversations, with each conversation containing the following fields:
- ```id```: (int) ID of the conversation.
- ```company```: (string) Name of the company involved in the interaction.
- ```is_subjective```: (bool) Indicates whether the conversation is subjective (i.e., contains emotions).
- ```has_cause```: (bool) Indicates whether the conversation has a cause.
- ```cause```: (dict) Additional information about the cause, present only if ```has_cause``` is True.
- ```turns```: (list of dict) List of turns in the conversation.

If a ```cause``` is in the conversation, it contains the following fields:
- ```cause_label```: (string) Annotation for the type of cause.
- ```tweet_id```: (int) Position of the cause in the list of tweets in this conversation (sequential).

Each turn in ```turns``` contains the following fields:
- ```tweets```: (list of dict) List of tweets within the turn.
- ```is_made_by_customer```: (bool) Indicates whether the turn is made by the customer.
- ```response_strats```: (list of string) List of response strategies used by the operator, present only if ```is_made_by_customer``` is False.
- ```emotions```: (dict) Emotion information, present only if ```is_made_by_customer``` is True.

If ```is_made_by_customer``` is True for a turn, the dictionary ```emotions``` in ```turns``` contains the following fields:
- ```arousal```: (int) Score on a 1-5 scale.
- ```dominance```: (int) Score on a 1-5 scale.
- ```valence```: (int) Score on a 1-5 scale.
- ```emo_clusters```: (list of string) List of emotion clusters.
- ```emo_labels```: (list of string) List of emotion labels.

Each tweet in ```tweets``` contains the following fields:
- ```text```: (string) Text in the tweet (note that URLs and users are anonymized).
- ```response_strats```: (list of string) List of response strategies used by the operator, present only if ```is_made_by_customer``` is False.
- ```emotions```: (dict) Emotion information, present only if ```is_made_by_customer``` is True.

If ```is_made_by_customer``` is True for a turn, the dictionary ```emotions``` in ```tweets``` contains the following fields:
- ```arousal```: (int) Score on a 1-5 scale.
- ```dominance```: (int) Score on a 1-5 scale.
- ```valence```: (int) Score on a 1-5 scale.
- ```emo_clusters```: (list of string) List of emotion clusters.
- ```emo_labels```: (list of string) List of emotion labels.

## 5. License
This work is licensed under a
[Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International License][cc-by-nc-sa]. This means that the repository is freely available for academic purposes or individual research, but restricted for commecial use. If you want to use the data for commercial purposes, please contact the authors (see contact details below).

[cc-by-nc-sa]: http://creativecommons.org/licenses/by-nc-sa/4.0/
[cc-by-nc-sa-image]: https://licensebuttons.net/l/by-nc-sa/4.0/88x31.png
[cc-by-nc-sa-shield]: https://img.shields.io/badge/License-CC%20BY--NC--SA%204.0-lightgrey.svg

## 6. Contact
For any questions regarding the dataset, do not hesitate to contact us at:
- sofie.labat@ugent.be
- thomas.demeester@ugent.be
- veronique.hoste@ugent.be

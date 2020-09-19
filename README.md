# SST-Aligned-Audiobooks
SST-Aligned-Audiobooks is a multimodal corpus designed to train English-to-Italian End-to-End Speech-to-Text Machine Translation models. The corpus consists of 60561 triplets of English audio, English source text, and Italian textual translation. These segments were extracted from 373 chapters read by 98 speakers for a total amount of 131.23 hours of English audio aligned with both its English source text and its Italian textual translation.

  * [Methodology](#methodology)
  * [Links to Corpus Download](#links-to-corpus-download)
  * [Corpus Statistics](#corpus-statistics)
  * [Reference](#reference)
  * [Licence](#licence)

## Methodology
To read in details the methodological approach, the experiments, and the evaluation of this corpus, please refer to <a href="https://www.diva-portal.org/smash/get/diva2:1440026/FULLTEXT01.pdf">Text and Speech Alignment Methods for Speech Translation Corpora Creation: Augmenting English LibriVox Recordings with Italian Textual Translations</a>. What it follows is a table that provides a quick glance at the tasks tackled and the technologies used. 

| Task | Technology|
| ------------- | ---: |
| English-to-Italian Books Titles Translation | Named Entity Recognition, WikiData, SPARQL| 
| Data Collection | Web Scraping, BeautifulSoup|
| Chapter Extraction from Text Files| Python, RegEx|
| Sentence Segmentation | <a href="https://spacy.io/">SpaCy</a>|
| Bilingual Dictionary Generation| <a href="www.statmt.org/moses/">Moses SMT</a>, <a href="https://github.com/moses-smt/giza-pp">Giza++</a>|
| Gale-Church Based Bilingual Text Alignment | <a href="https://github.com/danielvarga/hunalignHunalign">Hunalign</a> |
| Sentences Embeddings Based Bilingual Text Alignment | <a href="https://github.com/facebookresearch/LASER">Facebook LASER</a>, <a href="https://github.com/thompsonb/vecalign">Vecalign |
| Forced Alignment | <a href="https://github.com/readbeyond/aeneas">Aeneas</a> |
| Audio Processing and Features Extraction | <a href="https://github.com/astorfi/speechpy">Speechpy</a>, <a href="https://numpy.org/">Numpy</a> |

## Links to Corpus Download
A binary file containing the 60561 triplets of parallel English audio, English text, and Italian textual translation is available as a <a href="https://www.kaggle.com/giuseppedellacorte/stt-aligned-audiobooks-en-it/">Kaggle dataset</a>. The Kaggle dataset also contains two parallel texts for textual Machine Translation.

Numpy arrays containing 40-MFCC features extracted from the audio segments and aligned with their English transcription and their Italian textual translations are available through <a href="https://drive.google.com/file/d/19bpKRnIGwZU1bbFURSNCbi95xO8-xdk-/view?usp=sharing">Google Drive.</a>

## Corpus Statistics 

| Datum | Value |
| ------------- | :---: |
| Aligned Segments | 60561 |
| Average Segment Duration | 7.80s |
| Total Hours of English Speech | 131.23 |
| Number of Speakers | 98 |
| Number of Aligned Chapters | 373 |
| Average Number of Chapters Read by Speaker | 3.80 |

## Reference

Author: **Giuseppe Della Corte**

Course: **Master's Thesis in Language Technology, Uppsala University**

Supervisor: **Sara Stymne**

To use this work please cite:

```
@misc{della2020text,
  title={Text and Speech Alignment Methods for Speech Translation Corpora Creation: \
         Augmenting English LibriVox Recordings with Italian Textual Translations},
  author={Della Corte, Giuseppe},
  year={2020}
  url={https://www.diva-portal.org/smash/get/diva2:1440026/FULLTEXT01.pdf} 
}
```
## Licence

Shield: [![CC BY 4.0][cc-by-shield]][cc-by]

This work is licensed under a [Creative Commons Attribution 4.0 International
License][cc-by].

[![CC BY 4.0][cc-by-image]][cc-by]

[cc-by]: http://creativecommons.org/licenses/by/4.0/
[cc-by-image]: https://i.creativecommons.org/l/by/4.0/88x31.png
[cc-by-shield]: https://img.shields.io/badge/License-CC%20BY%204.0-lightgrey.svg

CREATIVE COMMONS MAKES NO WARRANTIES REGARDING THE INFORMATION PROVIDED, AND DISCLAIMS LIABILITY FOR DAMAGES RESULTING FROM ITS USE. THE WORK (AS DEFINED BELOW) IS PROVIDED UNDER THE TERMS OF THIS CREATIVE COMMONS PUBLIC LICENSE ("CCPL" OR "LICENSE").

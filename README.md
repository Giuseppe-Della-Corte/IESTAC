# IESTAC

IESTAC (Italian-English speech and text audiobook corpus) is a corpus designed to train English-to-Italian End-to-End Speech-to-Text Machine Translation models. The corpus consists of 60561 triplets of English audio, English source texts, and Italian textual translations. These segments were extracted from 373 chapters read by 98 speakers for a total amount of 131.23 hours of English audio aligned with both its English source text and its Italian textual translation.

  * [Methodology](#methodology)
  * [SQL Database](#sql-database)
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

## SQL Database
**database.sql.sz** contains a compressed SQL database that allows users to query the corpus according to their needs.
The database is composed of 6 tables.

The **metadata** table provides information regarding the original author, the Italian translator, book titles etc...
In case we did not find the Italian translator, a reference to the publication is given. 

The **public_domain_status** table provides information  regarding authors and their date of death. 
You have to respect the copyright laws of your country. This corpus is intended for countries were literary works enter in the public domain 50 years after the death of the author. Please remember that translators have to be considered authors as well, as translations are creative works. You'll have
to check the laws of the country where you are located before using this corpus. Filter out the works that you cannot use according to the laws of your country.

Here it follows a description of the tables in the database. Please notice that the SQL database does not contain the audio files, but only their names.
To download the audio files see [Links to Corpus Download](#links-to-corpus-download)

```
alignments
+---------------+-------+------+-----+---------+----------------+
| Field         | Type  | Null | Key | Default | Extra          |
+---------------+-------+------+-----+---------+----------------+
| id            | int   | NO   | PRI | NULL    | auto_increment |
| audiofilename | text  | NO   |     | NULL    |                |
| eng_text      | text  | NO   |     | NULL    |                |
| it_text       | text  | NO   |     | NULL    |                |
| book_id       | int   | NO   |     | NULL    |                |
| chapter_id    | int   | NO   |     | NULL    |                |
| score         | float | YES  |     | NULL    |                |
+---------------+-------+------+-----+---------+----------------+

audio_chapters
+------------+------+------+-----+---------+-------+
| Field      | Type | Null | Key | Default | Extra |
+------------+------+------+-----+---------+-------+
| chapter_id | int  | NO   |     | NULL    |       |
| book_id    | int  | NO   |     | NULL    |       |
| speaker_id | text | NO   |     | NULL    |       |
+------------+------+------+-----+---------+-------+

audio_segments
+---------------+-------+------+-----+---------+-------+
| Field         | Type  | Null | Key | Default | Extra |
+---------------+-------+------+-----+---------+-------+
| audiofilename | text  | NO   |     | NULL    |       |
| duration      | float | NO   |     | NULL    |       |
+---------------+-------+------+-----+---------+-------+

metadata
+----------------+------+------+-----+---------+-------+
| Field          | Type | Null | Key | Default | Extra |
+----------------+------+------+-----+---------+-------+
| book_id        | int  | NO   |     | NULL    |       |
| gutenberg_link | text | NO   |     | NULL    |       |
| librivox_link  | text | NO   |     | NULL    |       |
| author         | text | NO   |     | NULL    |       |
| author_it      | text | NO   |     | NULL    |       |
| title_en       | text | NO   |     | NULL    |       |
| title_it       | text | NO   |     | NULL    |       |
+----------------+------+------+-----+---------+-------+

public_domain_status
+---------------+------+------+-----+---------+-------+
| Field         | Type | Null | Key | Default | Extra |
+---------------+------+------+-----+---------+-------+
| author        | text | YES  |     | NULL    |       |
| date_of_death | int  | YES  |     | NULL    |       |
+---------------+------+------+-----+---------+-------+

speakers
+--------------+------+------+-----+---------+-------+
| Field        | Type | Null | Key | Default | Extra |
+--------------+------+------+-----+---------+-------+
| speaker_id   | int  | NO   |     | NULL    |       |
| speaker_link | text | NO   |     | NULL    |       |
| speaker_name | text | NO   |     | NULL    |       |
+--------------+------+------+-----+---------+-------+
```



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

Authors: **Giuseppe Della Corte, Sara Stymne**

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

This corpus is intended for countries were literary works enter in the public domain 50 years after the death of the author. Please remember that translators have to be considered authors as well, as translations are creative works. You'll have
to check the laws of the country where you are located before using this corpus.

Shield: [![CC BY 4.0][cc-by-shield]][cc-by]

This work is licensed under a [Creative Commons Attribution 4.0 International
License][cc-by].

[![CC BY 4.0][cc-by-image]][cc-by]

[cc-by]: http://creativecommons.org/licenses/by/4.0/
[cc-by-image]: https://i.creativecommons.org/l/by/4.0/88x31.png
[cc-by-shield]: https://img.shields.io/badge/License-CC%20BY%204.0-lightgrey.svg

CREATIVE COMMONS MAKES NO WARRANTIES REGARDING THE INFORMATION PROVIDED, AND DISCLAIMS LIABILITY FOR DAMAGES RESULTING FROM ITS USE. THE WORK (AS DEFINED BELOW) IS PROVIDED UNDER THE TERMS OF THIS CREATIVE COMMONS PUBLIC LICENSE ("CCPL" OR "LICENSE").

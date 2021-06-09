# ASR for Greek

This is meant to be a repository where one can find datasets and information about Greek audio datasets. In my previous job, my team was given the task to create a new speech to text engine and I noticed that it was really hard to find any open audio data for Greek. My current intention is to group the open/free sources so it will be easier for someone to find them. 

In addition, I plan to add some example scripts on how to train your own system. The idea of this repo came from [this](https://github.com/egorsmkv/speech-recognition-uk) similar project for Ukrainian.

Feel free to contact me for anything related. If you have any addition sources, please add them yourself (PR) or send me an email and I can add them.

## Data

Currently, there are not many available audio data in Greek (especially for speech recognition). Below, I will give a list of available sources:

| Provider                    | Hours | Link                                                                                         | Description                                                                                                                                                                                                       |
|-----------------------------|-------|----------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| VoxForge                    | 3.8   | http://www.voxforge.org/el/downloads                                                         | Different users say random sentences.                                                                                                                                                                             |
| Gsoc2019 (EELLAK) RADIO     | 1     | https://github.com/eellak/gsoc2019-sphinx/wiki/Datasets-and-Adaptation#radio                 | Multiple Greek speakers of the Department of Journalism tell the news lasting 1 hour (medium size, different speakers).                                                                                           |
| Gsoc2019 (EELLAK) Fairytale | 4     | https://github.com/eellak/gsoc2019-sphinx/wiki/Datasets-and-Adaptation#paramythi_horis_onoma | Greek woman speaker reads a fairytale lasting 4 hours (large size, one speaker).                                                                                                                                  |
| Gsoc2019 (EELLAK) Pda       | -     | https://github.com/eellak/gsoc2019-sphinx/wiki/Datasets-and-Adaptation#pda                   | Recordings of Greek people asking questions about the weather, nearest hospitals, and pharmacies. It was created for the purposes of this diploma thesis (medium size, different speakers, very specific domain). |
| Mozilla Common Voice        | 6     | https://commonvoice.mozilla.org/en/datasets                                                  | Each entry in the dataset consists of a unique MP3 and corresponding text file. May also include demographic metadata like age, sex, and accent that can help train the accuracy of speech recognition engines.   |


If you know of any other open/free datasets that contain audios with their transcription, please contact me or make a PR.

I also plan to upload some scripts that can create kaldi files out of the audios above (`wav.scp`, `utt2spk`, `spk2utt`, `text` and maybe `spk2gender`).

### E-book datasets

In addition to the sources above, you may also find it useful to use e-books. The negative of this approach is that, in most cases, e-books are many hours long and the corresponding text is a whole book. This makes allignment difficult and would probably require a separate alligner in order to make it work. 

A good approach would be to 

### Youtube Videos

Another source of data would be to look for youtube videos along with their transcriptions. In my experience, you will be able to find a good amount of data from TEDx talks since they almost always contain transcription.

I plan to add some links to some greek youtube videos that also contain greek subtitles. They will be available at the [`youtube_data` directory](/youtube_data/). Feel free to enrich it.


### Alignment

If you intend to use any of the above two approaches (e-books and youtube videos) then you should split the audio into smaller chunks and, hence, you should know the corresponding text of each chunk. 

Now, this is what an aligner is supposed to do. A great tool for that would be [Aeneas](https://github.com/readbeyond/aeneas). Personally, I have also tested the [Prosodylab-Aligner](https://github.com/prosodylab/Prosodylab-Aligner) project and I managed to get good results, but the negative thing is that you will need to train a new aligner from scratch (for which you would need data...). 

At last, you could use the open/free data above in order to create a simple Kaldi model and then use Kaldi's script for audio alignment. The recommended way for that is the following:
```bash
# Assumptions: 
#    1. You have trained a triphone model (the path is in `tri3_path`)
#    2. You have a language model (e.g. in data/lang) (the path is in `lang_dir`)
#    3. You have saved the path to your long-utterance files (e.g. wav.scp) in a variable named `train_dir`.
# Segment long utterances.
steps/cleanup/segment_long_utterances.sh $tri3_path $lang_dir $train_dir data/train_reseg exp/segment_train_utts
# Clean data (removing utterances that we are unsure of).
steps/cleanup/clean_and_segment_data.sh data/train_reseg $lang_dir $tri3_path ${tri3_path}_cleanup data/train_cleaned
```

For more information about audio-book alignment (and alignment for lengthy audios, in general), I advise you to read the [librispeech paper](http://www.danielpovey.com/files/2015_icassp_librispeech.pdf).


## Pre-trained Models

| Type         | Trained-on             | Test-WER | Link                                                                      |
|--------------|------------------------|----------|---------------------------------------------------------------------------|
| coqui-ai     | Common Voice 6.1 train | 80.2%    | https://github.com/coqui-ai/STT-models/releases/tag/greek%2Fitml%2Fv0.1.1 |
| Kaldi        | Audio Books and other  | -        | https://alphacephei.com/vosk/models                                       |
| Pocketsphinx | Unknown                | -        | https://sourceforge.net/projects/cmusphinx/files/Acoustic%20and%20Language%20Models/Greek/ |

There is also a [`voice2json`](https://github.com/synesthesiam/voice2json) model which can be found [here](https://github.com/synesthesiam/el-gr_pocketsphinx-cmu).

## Kaldi Model

[Alphacephei]() has published a kaldi model for doing Speech Recognition for Greek. The model is not really strong but you can adjust it to your needs (adaptation). 

For example, if you have 8-10 hours of transcripted audio in Greek, then you can use alphacephei's model and adapt it so it can fit your data. I have personally tried this and the results were really good (with a `TDNN` architecture). I am planning to upload a tutorial on acoustic model adaptation with Kaldi later on. In the meantime, feel free to reach me.


## TODO:
- Add simple kaldi tutorial.
- Add kaldi adaptation tutorial (based on alphacephei's greek model).
- Add long audio alignment scripts and example usages.
- Add e-book pages links.
- Add youtube video links (in a separate folder).

# ASR for the Greek Language

This is meant to be a repository where one can find datasets and information about Greek audio datasets. I was inspired by [this](https://github.com/egorsmkv/speech-recognition-uk) project for Ukrainian.

Feel free to contact me for anything related. 

## Data

Currently, there are not many available audio data in Greek (especially for speech recognition). Below, I will give a list of available sources:

| Provider                    | Hours | Link                                                                                         | Description                                                                                                                                                                                                      |
|-----------------------------|-------|----------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| VoxForge                    | 3.8   | http://www.voxforge.org/el/downloads                                                         | Different users say random sentences.                                                                                                                                                                            |
| Gsoc2019 (EELLAK) RADIO     | 1     | https://github.com/eellak/gsoc2019-sphinx/wiki/Datasets-and-Adaptation#radio                 | Multiple Greek speakers of the Department of Journalism tell the news lasting 1 hour (medium size, different speakers).                                                                                          |
| Gsoc2019 (EELLAK) Fairytale | 4     | https://github.com/eellak/gsoc2019-sphinx/wiki/Datasets-and-Adaptation#paramythi_horis_onoma | Greek woman speaker reads a fairytale lasting 4 hours (large size, one speaker).                                                                                                                                 |
| Gsoc2019 (EELLAK) Pda       | -     | https://github.com/eellak/gsoc2019-sphinx/wiki/Datasets-and-Adaptation#pda                   | Recordings of Greek people asking questions about the weather, nearest hospitals, and pharmacies. It was created for the purposes of this diploma thesis (medium size, different speakers, very specific domain). |
|                             |       |                                                                                              |                                                                                                                                                                                                                  |


I also plan to upload some scripts that can create kaldi files out of the audios above (`wav.scp`, `utt2spk`, `spk2utt`, `text` and maybe `spk2gender`). 

## Kaldi Model

[Alphacephei]() has published a kaldi model for doing Speech Recognition for Greek. The model is not really strong but you can adjust it to your needs (adaptation). 

For example, if you have 8-10 hours of transcripted audio in Greek, then you can use alphacephei's model and adapt it so it can fit your data. I have personally tried this and the results were really good (with a `TDNN` architecture). I am planning to upload a tutorial on acoustic model adaptation with Kaldi later on. In the meantime, feel free to reach me.
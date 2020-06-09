# DL202001-U5
RNN project for Fundamentals of Deep Learning

## Speech Emotion Recognition (Jaime Vergara - Luis F. Parra)

This project implements a model which detects the emotion of a particular subject based on his/her waveform associated 
to his/her speech. All the experiments are condensed in the notebook SER.ipynb included in this repository.

The dataset used for this excercise consists in selected audios from the dataset “Berlin database of emotional speech” taken from [here](http://emodb.bilderbar.info/start.html). The audios were sampled at 16kHz with 16-bit resolution and contains recordings of 10 authors (5 male and 5 female) producing 10 German utterances in an emotional manner. The recordings were labeled in seven emotions: anger, boredom, disgust, anxiety, happiness, sadness and neutral. A total of 13 MFCCs were extracted using a window of 25 ms. with a frameshift of 10 ms. Also, cepstral mean subtraction 
was applied. 

Many-to-one training was implemented. Different models were implemented and trained with various sequences lengths (10,20,50,100). Since the dataset is labeled at utterance level, each frame belonging to  an audio inherits the same label. Other experiments include labeling the silences (a new class) and removing the silences using VAD. 

Two main architectures based on recurrent neural netwoks were implemented:

| 1 | 2 |
| --- | --- |
| [LSTM,GRU][64,256] | [LSTM,GRU][64,256] x 2 |
| FC(256)| FC(256)|

#### Results

After trying with different values for loopbacks, we found that the model works better with lower values (we got better results with 10 and 20 frames compared to 50 and 100 frames). This seems to imply that the phenomenon does not have long memory.

Silence suppression did not improve overall performance. This is probably related to the hypothesis that silence and other disfluencies give significant information about [emotions](https://researchmgt.monash.edu/ws/portalfiles/portal/262318392/257088422_oa.pdf). On the other side, adding the silence as a new label supposes a more difficult problem.

As seen in the results, emotions grouped in terms or arousal are easily separated, due to the high or low activation characteristics shared among them.

Adding dropout in recurrent networks avoid the overfitting experimented in the first experiments. It also slightly improved the performance in terms of validation accuracy

# Transfer learning on small dataset for Singing Voice Synthesis

## Overview

Singing voice synthesis (SVS) is one of the most important examples in neural audio synthesis. Recently, [[2]](https://xiaoicesing.github.io/) might be the state of the art of chinese singing voice synthesis. It successfully synthesizes female singing voice from music score format. However, it still requireds a lot trainging data to develope this model.

This repo demonstrates how to build a singing voice synthesis model with small singing voice dataset. What we need additionally is a large scale speech voice dataset which is aqcuired more easily (compare to singing voice dataset). 
We use the same model in [[1]](https://github.com/NVIDIA/mellotron). It shows the possibility of synthesizing singing voice from only speech dataset. This model can be further improved by transfer learning on a small singing voice dataset.

This repo is only for sharing the results of the small experiments.  The code is mostly the same as the [[1]](https://github.com/NVIDIA/mellotron), and thus the code is not provided in this repo. However, I hope the short experiment could help someone who are interesting in SVS.



## Method

### Pretrain Mellotron on speech dataset

- Clone the Mellotron from its repo.
- Prepare your chinese speech dataset (BiaoBei Dataset is used in this repo [[3]](https://www.data-baker.com/open_source.html)).
- Process the text into pinyin or Bopomofo format (Both are OK. Bopomofo works slightly better in our experiments)
- Follow the instruction from its repo to training the mellotron.

### Transfer learning on singing voice dataset

- Prepare your singing voice data with score (in MusicXML format).
- Note that the attention is used to align the audio and text in mellotron. While transfer learning for the singing voice dataset, this attention module should be removed. (The alignment is provided by MusicXML).

- Prepare the unseen music score and now you can test your singing voice synthesis.

## Result

This experiment test on 1 male singer (~10 minutes training data) and 1 female singer (~18 minutes training data). Below is the synthesis result from unseen music score. 

- male samples:

  - [Synthesis result](https://drive.google.com/file/d/1reL9JLrzq0Y2afBN6Y6BuFPA5DaSiu64/view?usp=sharing)
  - [Reference in training data](https://drive.google.com/file/d/1T6DJAOQS67GXAsZYYQ_q573f_cCOH5bZ/view?usp=sharing)

- Female samples:

  - [Synthesis result](https://drive.google.com/file/d/1dvZtrSwiwXD9XMpHRR-37yJ7i6m8Q2RB/view?usp=sharing)
  - [Reference in training data](https://drive.google.com/file/d/1wSKVQUGD_9faf7C7IvxHkunBa6NhncJO/view?usp=sharing)

  

## Short Discussion & Future Work

The result shows singing voice with similar timbre could be synthesized successfully. However, some shortcomings also be found in the generated audio

1. The pronunciation is not clear enough.
2. The pitch weirdly deviates when note is relative long.
3. The singing voice is lack of expression.


Although the quality is not comparable to [[2]](https://xiaoicesing.github.io/), it gives another way to build SVS with lower cost. Some modification may help to improve the synthesis quality.

1. More singing voice training data
2. Data representation for singing expression.
3. Predict on Vocdoder feature domain (sp/ap/f0). It separate the singing voice into pronuciation, voiced/unvoiced and pitch.
4. Replace Waveglow with MelGAN.

## Reference
[1] Valle, Rafael, et al. "Mellotron: Multispeaker expressive voice synthesis by conditioning on rhythm, pitch and global style tokens." ICASSP 2020-2020 IEEE International Conference on Acoustics, Speech and Signal Processing (ICASSP). IEEE, 2020.

[2] Lu, Peiling, et al. "XiaoiceSing: A High-Quality and Integrated Singing Voice Synthesis System." arXiv preprint arXiv:2006.06261 (2020).

[3] BiaoBei speech dataset https://www.data-baker.com/open_source.html


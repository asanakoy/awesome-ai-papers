Jukebox: A Generative Model for Music
https://openai.com/blog/jukebox

- symbolic generators have limitations—they cannot capture human voices or many of the more subtle timbres, dynamics, and expressivity that are essential to music.
- model music directly as raw audio

Challenges:
- Sequences are very long. We have to deal wth extremely long-range dependencies
A typical 4-minute song at CD quality (44 kHz, 16-bit) has over 10 million timesteps.
 For comparison, GPT-2 had 1,000 timesteps and OpenAI Five took tens of thousands of timesteps per game

 - previous work on MuseNet  synthesized music based on large amounts of MIDI data

### Method

 - based on Vector Quantised-Variational AutoEncoders [VQ-VAE] (NeurIPS 2017) and VQ-VAE-2 (NeurIPS 2019)
 https://papers.nips.cc/paper/7210-neural-discrete-representation-learning.pdf
 https://arxiv.org/pdf/1906.00446.pdf
 - Hierarchical VQ-VAEs (NIPS 2018)
 https://arxiv.org/abs/1806.10474

 - three levels in our VQ-VAE, shown below, which compress the 44kHz raw audio by 8x, 32x, and 128x, respectively, with a codebook size of 2048 for each level.
 - Generating codes using transformers. Sparse Transformers as the learned priors for VQ-VAEs.
  - 3 levels of priors: a top-level prior that generates the most compressed codes, and two upsampling priors that generate less compressed codes conditioned on above.

Learning Music Priors and Upsamplers:
- [Sparse Transformers](https://openai.com/blog/sparse-transformer/) as the learned priors for VQ-VAEs.


Conditional music generation:
  - The top-level transformer is trained on the task of predicting compressed audio tokens conditionedf on artist and genre.
  - Lyrics conditioning using an extra encoder to produce a representation for the lyrics and attention layers that use queries from the music decoder to attend to keys and values from the lyrics encoder.


  Dataset:
  - Colected a new dataset of 1.2 million songs (600,000 of which are in English), paired with the corresponding lyrics and metadata from LyricWiki.


### Results and Limitations

- There is still a significant gap between these generations and human-created music.
-  local musical coherence, traditional chord patterns, impressive solos.
- No choruses that repeat.
- downsampling and upsampling process introduces discernable noise
- Very slow to sample (because of the autoregressive structure). ~9 hours to  render 1 min audio.
- currently trained on English lyrics and mostly Western music.
- Set of 10 musicians from various genres which git early acces to JukeBox Tool  discuss their feedback on this work. While Jukebox is an interesting research result, these musicians did not find it immediately applicable to their creative process given some of its current limitations.

Future work:
- Speed improvement (e.g., via model distillation)
- Conditioning on MIDI files.

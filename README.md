# extract-jukebox-embeddings

[Link to Colab Notebook](https://colab.research.google.com/drive/1jdR5w-XlJQFog47ZJ36ckEVMW0F5qIpl).

A notebook for extracting embeddings from [OpenAI's Jukebox model](https://openai.com/index/jukebox/), following the approach described in [Castellon et al. (2021)](https://arxiv.org/abs/2107.05677) with some modifications followed in [Spotify's Llark paper](https://arxiv.org/pdf/2310.07160):

- Source: Output of the 36th layer of the Jukebox encoder
- Original Jukebox encoding: 4800-dimensional vectors at 345Hz
- Audio/embeddings are chunked into 25 seconds clips as that is the max Jukebox can take in as input, any clips shorter than 25 seconds are padded before passed through Jukebox
- Approach: Mean-pooling within 100ms frames, resulting in:
    - Downsampled frequency: 10Hz
    - Embedding size: 1.2 × 10^6 for a 25s audio clip.
    - For a 25s audio clip the 2D array shape will be [250, 4800]
- This method retains temporal information while reducing the embedding size

Having a Colab notebook for this gives us an easily reproducible environment and allows us to take advantage of the cheap T4 GPU's Colab offers.

Extended from this repo: https://github.com/Broccaloo/jukebox

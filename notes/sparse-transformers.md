# Sparse Tansformers

Generative Modeling with Sparse Transformers, OpenAI, 2019  
Rewon Child, Scott Gray, Alec Radford, Ilya Sutskever

[[BLog]](https://openai.com/blog/sparse-transformer/) [[paper]](https://arxiv.org/abs/1904.10509)

- The Sparse Transformer incorporates an O(N^1.5) reformulation of the O(N^2) Transformer self-attention mechanism;
- To reduce memory consumption: recomputing the attention matrix from checkpoints during backpropagation
- computing a single attention matrix can become impractical for very large inputs. We instead use sparse attention patterns, where each output position only computes weightings from a subset of input positions (O(N*1.5) inputs)

Results:
-  sparse attention achieved lower loss than full attention, in addition to being significantly faster 
- image completion and generation
- Generating raw audio waveforms

Future work and limitations
- exploring different sparce attention patterns
- the proposed method seems still impractical for very high resolution images or video.
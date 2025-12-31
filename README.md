This repo currently contains a python notebook that trains a few language models and an LLM-generated summary and analysis of its results. The training was done locally on a 16gb GPU, and the perplexity results so far seem promising. However, we're not sure we're properly equipped to verify our findings.

<img width="726" height="220" alt="image" src="https://github.com/user-attachments/assets/c3fb7109-767c-40b0-b946-75c4a037e754" />

We created this Resonance strategy by following some general principles stumbled upon from an unrelated domain. We have enough understanding of training LLMs to have assembled this, but not enough to understand if what we have is meaningful in the sense that it seems like it might be. This "Resonance" framework attempts to introduce a unique kind of multimodality into the training structure. Take a look at the implementation, take a look at the results, and if you are so moved kindly leave a comment, issue or PR with your feedback.

If you've stumbled onto this repo, and you understand LLM training strategies and evaluation, please consider taking a moment to consider the notebook first. It lays everything out, and the most important findings happen near the end - there are some false negatives as the structure is built up, but keep going. If what you see is interesting, then read the pdf file which digs into the findings.

## What's the TLDR?
By introduciung an orthogonal modality to semantics based on a sort of phase mechanism we are able to split the attention head between both interpretations of a given token. "Phase" for our purposes is generic and doens't need to be specified, but an example of a non-semantic modality would be using phonetic similarity for latent space positioning - two words that rhyme are closer together, two words that don't rhyme are farther apart. This sounds silly, but we have some fascinating theory behind why this might work the way it seems to. But as you can see from our findings, rhyme has a minimal impact specifically - but phase as a secondary modality has a *massive* impact.

## Diagram
The Full Picture

┌─────────────────────────────────────────────────────────────────┐
│                         INPUT                                    │
│                    "light shines at night"                       │
└─────────────────────────────────────────────────────────────────┘
                              │
                              ▼
┌─────────────────────────────────────────────────────────────────┐
│                    GPT-2 TOKENIZER                               │
│                    [2971, 27741, 379, 1755]                      │
│                    (standard, nothing special)                   │
└─────────────────────────────────────────────────────────────────┘
                              │
                              ▼
┌─────────────────────────────────────────────────────────────────┐
│                 DUAL EMBEDDING (key innovation)                 │
│  ┌──────────────┐          ┌──────────────┐                     │
│  │   Semantic   │          │    Phase     │                     │
│  │   [768 dim]  │          │   [32 dim]   │                     │
│  │   (meaning)  │          │   (sound)    │                     │
│  └──────┬───────┘          └──────┬───────┘                     │
│         │                         │                              │
│         │    ┌─────────────┐      │                              │
│         └───►│   BLEND     │◄─────┘                              │
│              │  (learned)  │                                     │
│              └──────┬──────┘                                     │
│                     │                                            │
│                     ▼                                            │
│              Final Embedding                                     │
└─────────────────────────────────────────────────────────────────┘
                              │
                              │ also compute
                              ▼
┌─────────────────────────────────────────────────────────────────┐
│              RESONANCE MATRIX (key innovation)                  │
│                                                                  │
│            light  shines  at   night                             │
│    light  [ 1.0   0.12  0.08  0.95 ]                            │
│    shines [ 0.12  1.0   0.15  0.11 ]                            │
│    at     [ 0.08  0.15  1.0   0.09 ]                            │
│    night  [ 0.95  0.11  0.09  1.0  ]                            │
│                                                                  │
└─────────────────────────────────────────────────────────────────┘
                              │
                              ▼
┌─────────────────────────────────────────────────────────────────┐
│           RESONANCE ATTENTION (key innovation)                  │
│                                                                  │
│    Standard:  attention = softmax(QK^T / √d)                    │
│    Yours:     attention = softmax(QK^T / √d + λR)               │
│                                             ^^                   │
│                                    resonance bias                │
│                                                                  │
│    Result: "night" attends more to "light" (they rhyme)         │
└─────────────────────────────────────────────────────────────────┘
                              │
                              ▼
┌─────────────────────────────────────────────────────────────────┐
│                    STANDARD FFN + LAYERS                         │
│                    (nothing special here)                        │
└─────────────────────────────────────────────────────────────────┘
                              │
                              ▼
┌─────────────────────────────────────────────────────────────────┐
│                         OUTPUT                                   │
│                    Next token prediction                         │
└─────────────────────────────────────────────────────────────────┘

## What We Want
If this is doing what we think it's doing then we have strong intuition for how to further develop this. However, we're soon going to get to a point where we need compute resources outside of our current capabilities. So ideally, in a best-case reality, we've stumbled onto something signficant and someone is willing to throw some compute resources at us so that we can see if it scales in the ways we hope. In the worst case, this is noise masquerading as signal. We'd really like an opportunity to find out.

## Are These Results Meaningful?
The biggest question we have right now is, are these results meaningful? Because if so, this feels significant. 


### Authors
I'm not the primary author of this code - it was created in collaboration with a human associate who at this point would prefer to go by the name Tacokotor.

### Related Links
After sharing this, someone shared a paper from last month that uses similar ideas to improve RAG. We arrived at this concept independently, literally yesterday, but the existence of [this paper](https://arxiv.org/abs/2511.11848) feels ...resonant.

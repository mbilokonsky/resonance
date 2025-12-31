# The Resonator Architecture
>  What if you gave your LLM ADHD by teaching it to pay attention to things like rhyme, and it suddenly got 60% smarter?

This repo contains a very simple proof of concept for a novel LLM training architecture we call The Resonator. It works like this:

<img width="606" height="1231" alt="image" src="https://github.com/user-attachments/assets/3b196530-5e8c-4df2-b607-21492dd8af82" />

Against a (relatively small, but not trivial) dataset, we saw the following results:

<img width="726" height="220" alt="image" src="https://github.com/user-attachments/assets/c3fb7109-767c-40b0-b946-75c4a037e754" />

We created The Resonator by following some general principles stumbled upon from an unrelated domain. We have enough understanding of training LLMs to have assembled this, but not enough to understand if what we have is meaningful in the sense that it seems like it might be. The Resonator framework attempts to introduce a unique kind of multimodality into the training structure. Take a look at the implementation, take a look at the results, and if you are so moved kindly leave a comment, issue or PR with your feedback.

Alternatively, consider dropping the notebook, the results, the diagram and this readme into your favorite robot and asking it what it thinks.

If you've stumbled onto this repo, and you understand LLM training strategies and evaluation, please consider taking a moment to consider the notebook first. It lays everything out, and the most important findings happen near the end - there are some false negatives as the structure is built up, but keep going. If what you see is interesting, then read the pdf file which digs into the findings.

## What's the TLDR?
By introduciung an orthogonal modality to semantics based on a sort of phase mechanism we are able to split the attention head between both interpretations of a given token. "Phase" for our purposes is generic and doens't need to be specified, but an example of a non-semantic modality would be using phonetic similarity for latent space positioning - two words that rhyme are closer together, two words that don't rhyme are farther apart. This sounds silly, but we have some fascinating theory behind why this might work the way it seems to. But as you can see from our findings, rhyme has a minimal impact specifically - but phase as a secondary modality has a *massive* impact.

## What We Want
If this is doing what we think it's doing then we have strong intuition for how to further develop this. However, we're soon going to get to a point where we need compute resources outside of our current capabilities. So ideally, in a best-case reality, we've stumbled onto something signficant and someone is willing to throw some compute resources at us so that we can see if it scales in the ways we hope. In the worst case, this is noise masquerading as signal. We'd really like an opportunity to find out.

## Are These Results Meaningful?
The biggest question we have right now is, are these results meaningful? Because if so, this feels significant. 


### Authors
I'm not the primary author of this code - it was created in collaboration with a human associate who at this point would prefer to go by the name Tacokotor.

### Resonant Works
We literally stumbled onto this idea from first principles less than 24 hours before the time of this writing. Since starting to share it folks have shared a few things it has reminded them of, and I find this fascinating.

* [Phase-Coded Memory and Morphological Resonance: A Next-Generation Retrieval-Augmented Generator Architecture](https://arxiv.org/abs/2511.11848) feels ...resonant. They're suggesting that RAG could be improved using similar techniques to compress external knowledge sources.
* [Phase-Coded Memory and Morphological Resonance: A Next-Generation Retrieval-Augmented Generator Architecture](https://arxiv.org/abs/2509.10534) also seems to have converged on the idea of "multi-polar" coordinates, which might rhyme with this. They're solving a different problem, I think - they're trying to fix a known issue with positionality vs meaning. But there's a resonance here.

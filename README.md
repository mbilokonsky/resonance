# The Resonance Transformer
>  What if you gave your LLM ADHD by teaching it to pay attention to non-semantic resonance, and it suddenly got 60% smarter?

This repo contains a very simple proof of concept for a novel LLM training architecture we call Resonance Transformers. The files here include:

  * [test5.ipynb](https://github.com/mbilokonsky/resonance/blob/main/test5.ipynb), the original notebook that was used to generate our provisional results.
  * [resonacne_transformer_result_v2.md.pdf](https://github.com/mbilokonsky/resonance/blob/main/resonance_transformer_report_v2.md.pdf), an LLM-generated analysis of the findings from test5.ipynb
  * [Resonance_Transformers.ipynb](https://github.com/mbilokonsky/resonance/blob/main/Resonance_Transformers.ipynb), a more coherent and better structured presentation of this idea.

This is under rapid exploratory development. test5 and the PDF are here because they were the first meaningful result, and because the more robust notebook does not yet have data included - it's literally processing right now, against a much larger dataset. If you are curious to see what we achieved with the prototype, look at test5 and the pdf. If you want to test this for yourself, or to step through a more annotated and detailed explanation of what's going on, please jump right into Resonance_Transformers.ipynb. Over the next few days I will deprecate the original stuff and replace it with the new notebook, including results.

## Flow Diagram
<img width="606" height="1231" alt="image" src="https://github.com/user-attachments/assets/3b196530-5e8c-4df2-b607-21492dd8af82" />

## Initial Findings
Take this with a grain of salt - this is the result from test5.ipynb, which was run against too small a dataset to fully rely on what's here. That said, the findings strike us as enough to dig deeper. As stated above, we'll deprecate these findings and replace them with more robust findings as we assemble them.

<img width="726" height="220" alt="image" src="https://github.com/user-attachments/assets/c3fb7109-767c-40b0-b946-75c4a037e754" />

We created The Resonance Transformer architecture by following some general principles stumbled upon from an unrelated domain. We have enough understanding of training LLMs to have assembled this, but not enough to understand if what we have is meaningful in the sense that it seems like it might be. This Transformer attempts to introduce a unique kind of multimodality into the training structure. Take a look at the implementation, take a look at the results, and if you are so moved kindly leave a comment, issue or PR with your feedback.

Alternatively, consider dropping the notebooks, the results, the diagram and this readme into your favorite robot and asking it what it thinks.

## What's the TLDR?
By introduciung an orthogonal modality to semantics based on a sort of phase mechanism we are able to split the attention head between both interpretations of a given token. "Phase" for our purposes is generic and doens't need to be specified, but an example of a non-semantic modality would be using phonetic similarity for latent space positioning - two words that rhyme are closer together, two words that don't rhyme are farther apart. This sounds silly, but we have some fascinating theory behind why this might work the way it seems to. But as you can see from our findings, rhyme has a minimal impact specifically - but phase as a secondary modality has a *massive* impact.

## What We Want
If this is doing what we think it's doing then we have strong intuition for how to further develop this. However, we're soon going to get to a point where we need compute resources outside of our current capabilities. So ideally, in a best-case reality, we've stumbled onto something signficant and someone is willing to throw some compute resources at us so that we can see if it scales in the ways we hope. In the worst case, this is noise masquerading as signal. We'd really like an opportunity to find out.

## Are These Results Meaningful?
The biggest question we have right now is, are these results meaningful? Because if so, this feels significant. 

### Reason For Concern
However, the tests here are against a relatively small amount of data given the parameter size. We really need to be running this against a larger source of data. (Currently this is happening, but it's going to take a few days to finish). When we have better numbers we will update this readme with new information, but the one big weakness we are aware of is that the data we're using isn't sufficient for the model sizes to truly hit their stride.

## Authors
I'm not the primary author of this code - it was created in collaboration with a human associate who at this point would prefer to go by the name Tacokotor.

## Resonant Works
We literally stumbled onto this idea from first principles less than 24 hours before the time of this writing. Since starting to share it folks have shared a few things it has reminded them of, and I find this fascinating.

* [Phase-Coded Memory and Morphological Resonance: A Next-Generation Retrieval-Augmented Generator Architecture](https://arxiv.org/abs/2511.11848) feels ...resonant. They're suggesting that RAG could be improved using similar techniques to compress external knowledge sources.
* [Phase-Coded Memory and Morphological Resonance: A Next-Generation Retrieval-Augmented Generator Architecture](https://arxiv.org/abs/2509.10534) also seems to have converged on the idea of "multi-polar" coordinates, which might rhyme with this. They're solving a different problem, I think - they're trying to fix a known issue with positionality vs meaning. But there's a resonance here.

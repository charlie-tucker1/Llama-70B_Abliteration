# Llama-70B_Abliteration
3 methods of abliteration applied to Llama 3.2 70B Instruct -- **Work in progress**

I've found the layer specific abliteration works the best in practice. It computes refusal directions for each targeted layer.

For the intuition behind abliteration:
refusal direction = (m(harmful) - m(harmless) / ||m(harmful) - m(harmless)||     (In terms of activations when given harmful/harmless prompts) m = mean

post abliteration weight = pre abl. weight - (pre abl. weight * refusal direction)

By finding refusal directions and decreasing weights by the mean activation in that direction, we lessen the model's ability to refuse certain prompts.

Limitations:
abliteration is done based on the activations of our contrast prompts, so the model will likely refuse prompts whose activations fall outside that of our contrast prompts used to calculate abliteration directions.

I want to expand the selection of contrast prompts to get a wider breadth of refusals, but I have a suspision that this would hurt model performance, as forcefully changing activations could have unintended consequences

Theoretically, you could carefully select contrast prompts that have very similar semantics to the kind of task you want the abliterated model to comply with. Then abliterate the refusal direction associated with those specific prompts. This 'task-specific-abiliteration' represents a vulnerability in language models of all sizes, because theoretically, activations would remain similar for a given set of semantically similar prompts, so, no matter model size, you could isolate the refusal direction(s) for said prompt/task, abliterate them, then the model should comply.




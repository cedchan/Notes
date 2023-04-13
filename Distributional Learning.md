
- Idea: measure words/noun class learning

- Young children know the distributional regularity of words
	- E.g., nouns follow "the"
- Lexical frames
	- Not used to classify, but to group
	- Could potentially assume that there are nouns and verbs
- Subdivide by "biggest" feature
	- Choose largest feature
	- Lexical frames

- Greedy recursion makes decision tree? how to become categories from that?
- How to prevent over-specification?
	- Don't learn now

- e.g., pronoun->how to separate from nouns

ONLY SUBDIVIDE IF NO RULE GENERALIZES. after stopping subdivision, can still generalize new rules to make new categories 

- ditransitive, 2 words after lexical frame

- efficiency if we have to remake lexical frames every time we generalize


### Algo

1. Find lexical frames of each word
2. Create hypotheses based on frames
3. If a hypothesis generalizes by TP, its members are a category. Reprocess lexical frames to replace its members with that class

### Questions

1. When you preprocess lexical frames with categories
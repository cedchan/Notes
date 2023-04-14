
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
3. If a hypothesis generalizes by TP, its members are a category. Reprocess lexical frames to replace its members with that class. Otherwise, find the biggest frame (i.e., has the most members), and subdivide the set into that and all others. 
4. Recursively apply step 3 to all sets of words (first it's all words, then the sets become each subdivided set). Note the base case: if a hypothesis generalizes over a set by TP, it becomes a category and is no longer subdivided.

### Questions

1. When you preprocess lexical frames with categories, do you replace with a "deeper"/more specific category every time one is discovered? Or do you only ever recategorize when you've hit the base case?
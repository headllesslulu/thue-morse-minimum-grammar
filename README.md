# thue-morse-minimum-grammar
Exact minimum grammars for Thue–Morse words. Includes a proof, Lean-checked finite cases, and a lossless encoder and decoder that reconstruct a 1,048,576-bit word from 75 rule-body symbols.

Smallest grammars for Thue–Morse words

This project proves how small a lossless grammar can be for every Thue–Morse word. A grammar is a list of reusable pieces and instructions for joining them. Its decoder expands those instructions to recover every bit of the original word.

The result
Start with 0. In each round, replace every 0 with 01 and every 1 with 10. After $n$ rounds the word $T_n$ has $2^n$ bits.
What you count	Exact minimum	For $T_{20}$, a 1,048,576-bit word
Symbols across all rule bodies	$4n-5$ for $n\geq3$	75 symbols
Productions in a binary grammar, including the terminal rules	$2n+1$ for $n\geq1$	41 rules


For levels 0, 1, and 2, the minimum rule-body symbol counts are 1, 2, and 4. At level 0 the binary grammar has one terminal rule. These figures count grammar symbols or rules. A serialized file also has to store the references and rule boundaries.
How the proof works
The eight-bit word 01101001 already shows how the grammar saves space. Store 01 once as C. The start rule C 1 C 0 C expands to all eight bits. The two rule bodies contain seven symbols in total.

For the lower bound, run the substitution backward. A block of at least four bits tells you how it lines up with the pairs in the word. That alignment lets you delete alternate bits directly from a grammar and obtain a grammar for the previous level or its bitwise complement. For levels five and above, a fixed 18-bit prefix rules out every case where both choices save fewer than four symbols. The matching construction spends exactly four more symbols per round.

The binary rule count uses a second fact. Any block longer than a quarter of the word occurs only once. From level two onward, that forces at least two single-use rules below the start in a binary grammar. Inlining those rules connects the binary count to the symbol bound.

Mieno, Inenaga, and Horiyama identified Thue–Morse words as a family to study in their work on smallest grammars. CPM 2022 paper, Section 6

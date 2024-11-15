# Named-Entity-Recognition (NER)

This repository introduces the fundamentals of Named Entity Recognition (NER), including a general definition, task modeling, and evaluation methods used for this task.

## Definition

Named Entity Recognition (NER) involves identifying and labeling proper names within text, such as persons, locations, or organizations. These entities are assigned semantic types, like:

- **PER**: Person (e.g., Max Planck)
- **LOC**: Location (e.g., Germany)
- **ORG**: Organization (e.g., Max Planck Institute)

In recent years, NER has expanded to include dates, temporal expressions, and even numerical expressions, which is particularly relevant in domains like astrophysics.

#### Examples of NER Model Output:

1. **Max Planck** [PER] was born in **Germany** [LOC] on **April 23, 1858** [DATE].
2. Fundamental research in physics is conducted at **Max Planck** [ORG] in **Germany** [LOC].
3. The **Planck** [VALUE] constant is fundamental in quantum mechanics.

## Task Modelization

The NER task can be modelled as a sequence labelling task, where the sequence consists of several tokens (words), and the tagger must assign the correct label to each token. As shown in the table below, various tagging schemes have been proposed. The standard approach to sequence labelling is the BIO tagging scheme. This method labels a sequence of tokens to capture both the boundary and the named entity type. In the BIO tagging scheme, tokens that begin a span of interest are labelled with B, tokens within a span are tagged with I, and tokens outside any span of interest are labelled O. The BIOES tagging scheme, on the other hand, adds an E tag for the end of a span and an S tag for spans consisting of a single token.

- **BIO**: Beginning (B), Inside (I), and Outside (O)
- **BIOES**: Adds End (E) and Single (S) tags for better boundary detection

Below is an example sequence with different tagging schemes:

| Tokens       | IO Label      | BIO Label         | BIOES Label      |
|--------------|---------------|-------------------|------------------|
| The          | O             | O                 | O               |
| Fermi        | I-Telescope   | B-Telescope       | B-Telescope     |
| Gamma-ray    | I-Telescope   | I-Telescope       | I-Telescope     |
| Space        | I-Telescope   | I-Telescope       | I-Telescope     |
| Telescope    | I-Telescope   | I-Telescope       | E-Telescope     |
| observed     | O             | O                 | O               |
| 4FGL         | I-CelestialObject | B-CelestialObject | B-CelestialObject |
| J2007.9      | I-CelestialObject | I-CelestialObject | E-CelestialObject |
| Vizier       | I-Database    | B-Database        | S-Database      |

This table shows the differences between tagging schemes (IO, BIO, and BIOES) used for NER as a sequence classification problem.

## Evaluation Metrics

NER model performance is typically measured with **Precision (P)**, **Recall (R)**, and the **F1 score**:

**P** = <sup>TP</sup> / <sub>(TP + FP)</sub>
**P** = <sup>TP</sup> / <sub>(TP + FN)</sub>
**P** = <sup>2*R*P</sup> / <sub>(R+P)</sub>


Where:
- **True Positive (TP)**: Correctly identified entities
- **False Positive (FP)**: Incorrectly labeled entities
- **False Negative (FN)**: Missed entities

Two primary evaluation settings for entity matching:
1. **Exact-match (Strict)**: Both the entity type and boundaries must match exactly.
2. **Relaxed-match (Overlap)**: Matches if boundaries overlap, counting an entity as a true positive if it shares half of its tokens with the gold standard.

## External References

For more detailed information on named entity recognition, see section 17.3 (page 367) of [Stanford's Speech and Language Processing book](https://web.stanford.edu/~jurafsky/slp3/ed3book.pdf)

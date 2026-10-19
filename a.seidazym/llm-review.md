# LLM Review — Top Words Specification

## Model Used

OpenAI GPT-6

## Final Review Prompt

Review the revised Top Words specification for Python 3.

Check for:
1. Ambiguous or contradictory requirements.
2. Missing input and output definitions.
3. Unicode normalization and multilingual text handling.
4. Word boundaries and combining marks.
5. Frequency counting, sorting, and tie-breaking.
6. Empty inputs and invalid input types.
7. Missing edge cases and incorrect expected outputs.

Determine whether two independent programmers could reasonably produce different outputs while following the specification.

## Final Review Output

### Overall Assessment

The revised specification provides deterministic rules for implementing the Top Words problem.

The function interface, input validation, Unicode processing, word identification, frequency counting, sorting, and output format are explicitly defined.

### Review Findings

**1. Function interface:** Clear. The file name, function name, input type, and output structure are specified.

**2. Unicode handling:** Clear. NFC normalization is performed before tokenization and after case folding. Combining marks are explicitly handled.

**3. Word identification:** Clear. Alphabetic characters begin words, and combining marks may continue them. Other characters separate words.

**4. Case sensitivity:** Clear. Case folding is applied after extracting words.

**5. Frequency counting:** Clear. All occurrences throughout the article are counted.

**6. Sorting:** Clear. Frequencies are sorted descending, with normalized Unicode strings used for ascending tie-breaking.

**7. Edge cases:** Covered. Empty strings, whitespace, punctuation, digits, invalid inputs, and fewer than ten unique words are addressed.

**8. Examples:** The specification contains 16 examples demonstrating the major requirements.

### Implementation Verification

A Python implementation was created independently from the specification and checked against the 16 examples.

Result: 16 of 16 examples passed.

Additional checks confirmed that invalid inputs raise TypeError and that underscores and isolated combining marks follow the stated rules.

### Final Conclusion

No unresolved contradictions or significant underspecified behaviors were identified in the final review.

The specification is sufficiently precise for implementation and ready for submission.
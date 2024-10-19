# pastal
PASTAL (Phonetic and Semantic Text Analysis Library)

PASTAL is a library designed for advanced text tokenization and matching, with an emphasis on phonetic and semantic analysis. This library addresses several real-world use cases like bypassing copyright filters, detecting subtle homophonic manipulations, and improving the accuracy of text matching in contexts like profanity detection.

<details>
<summary>updated README contents in progress</summary>
Basic and custom tokenization for flexible text splitting.
Phonetic and semantic matching to capture subtle variations and meanings in text.
Batch processing for high-performance analysis of large datasets.
Customizable thresholds for fine-tuning phonetic and semantic match sensitivity.
Functional Overview
Package Stucture
1. Basic Tokenization
Function: basic_tokenize(text: str) -> List[str]

Description: Splits input text into tokens (words) based on common delimiters like spaces and punctuation.
Use Cases: Simple word boundary detection, standard text tokenization for preprocessing.
Requirements:

Split text into tokens using spaces and punctuation as delimiters.
Returns a list of tokens without further analysis (no phonetic or semantic matching).
2. Custom Tokenization
Function: custom_tokenize(text: str, split_by: str = " ", normalize: bool = True) -> List[str]

Description: Allows for tokenizing text using a user-specified delimiter and optional normalization (lowercasing, removing special characters).
Use Cases: Tokenization for non-standard text inputs, customized text preprocessing for specific formats.
Requirements:

Users can specify a delimiter for splitting text (default: space " ").
Optional normalization step to prepare text for tokenization (lowercasing, special character removal).
Returns a list of tokens based on the chosen delimiter.
3. Tokenization with Phonetic and Semantic Matching
Function: tokenize_with_phonetics_and_semantics(text: str, phonetic_threshold: float = 0.8, semantic_threshold: Optional[float] = None) -> List[Tuple[str, str, Optional[str]]]

Description: Tokenizes input text and provides phonetic and optional semantic matches for each token.
Use Cases: Detecting homophones, avoiding common workarounds in copyright detection, detecting euphemisms in profanity filters.
Requirements:

Tokenizes the input text.
Finds phonetic matches for each token based on a phonetic similarity threshold.
Optionally, finds semantic matches if a semantic threshold is provided.
Returns a list of tuples: (original token, phonetic match, semantic match).
4. Phonetic and Semantic Matching Without Tokenization
Function: get_matches(text: str, phonetic_threshold: Optional[float] = None, semantic_threshold: Optional[float] = None) -> List[Tuple[str, Optional[str], Optional[str]]]

Description: Finds phonetic and/or semantic matches for a block of input text without splitting it into tokens.
Use Cases: Large-text matching tasks, finding paraphrased or homophonic variations in non-tokenized text.
Requirements:

Accepts a block of text as input.
Finds phonetic matches based on the phonetic threshold.
Optionally finds semantic matches if a semantic threshold is provided.
Returns a list of tuples: (original text, phonetic match, semantic match).
5. Batch Processing
Function: batch_process(texts: List[str], mode: str = "tokenize", phonetic_threshold: Optional[float] = None, semantic_threshold: Optional[float] = None) -> List[List[Tuple[str, Optional[str], Optional[str]]]]

Description: Processes a list of texts in batch, applying tokenization and/or matching based on the selected mode (tokenize, phonetic, semantic, both).
Use Cases: High-performance processing for large datasets, bulk copyright or profanity filtering.
Requirements:

Processes a list of texts based on the selected mode:
tokenize: Standard tokenization.
phonetic: Finds phonetic matches.
semantic: Finds semantic matches.
both: Tokenizes and finds both phonetic and semantic matches.
Allows customizable thresholds for phonetic and/or semantic matching.
Returns a list of lists, where each sublist contains tuples: (original token, phonetic match, semantic match).
Potential Use Cases
Bypassing Copyright Filters: Detecting homophonic workarounds where users submit phonetically similar but non-copyrighted text to bypass detection systems.
Profanity Filters: Identifying euphemisms and homophones used to evade standard profanity detection algorithms.
Plagiarism Detection: Detecting paraphrased or semantically similar content in academic or creative works, even if exact wording is changed.
Text-to-Speech Filtering: Ensuring TTS systems avoid generating restricted content by identifying phonetic or semantic similarities.
Adversarial Text Analysis: Providing robust defenses against adversarial inputs designed to trick AI models.
Installation
You can install PASTAL using pip:

bash
Copy code
pip install pastal
Usage
Example usage for basic tokenization:

python
Copy code
from pastal import basic_tokenize

text = "The quick brown fox jumps over the lazy dog."
tokens = basic_tokenize(text)
print(tokens)
To use phonetic and semantic matching:

python
Copy code
from pastal import tokenize_with_phonetics_and_semantics

text = "pastal sounds like pastel"
matches = tokenize_with_phonetics_and_semantics(text)
print(matches)
For batch processing:

```python
Copy code
from pastal import batch_process
```

</details>
<details open>
<summary>Features</summary>

  - **Phonetic Matching:**  PASTAL can detect text that sounds similar to a target string, even when the spelling is entirely different. This feature makes it particularly useful for:
    - **Circumventing filters:** Detect attempts to bypass profanity or copyright filters using homophones (e.g., "wouldn't it" vs. "wooden tit").
    - **Detection of adversarial inputs:** Identify crafted inputs meant to trigger unintended outputs from language models.
  - **Mondegreen Detection:** Mondegreens—phrases that are misheard or misinterpreted in a way that retains a similar sound—are automatically detected. PASTAL identifies text or phrases that might sound like a target phrase, even when their literal interpretation is entirely different. This is particularly useful for:
    - **Profanity filters:** Catch attempts to bypass filters using sound-alike words or phrases.
    - **Copyright enforcement:** Detect attempts to have AI models output copyrighted material via phonetic approximations.
  -  **Semantic Awareness:** PASTAL also understands the meaning behind text, allowing for more sophisticated detection and transformation. For example:
    - **Copyright violations:** Catch phrases semantically similar to protected content, even if they don't match phonetically.
    - **Adversarial testing:** Ensure models cannot be tricked into generating copyrighted or harmful content by subtly rephrased inputs.
  -  **Configurable Thresholds:** PASTAL allows for fully configurable similarity thresholds, so developers can fine-tune the library for their specific use cases:
    - **Phonetic similarity:** Set percentage thresholds for how closely two syllables or phrases must sound alike to trigger a match.
    - **Semantic similarity:** Adjust how strict the library should be when considering text to be semantically equivalent.
  - **Multiple Functionality Modes:** PASTAL offers different functions to return specific data depending on the use case:
    - Phonetic match detection
    - Semantic match detection
    - Combined phonetic and semantic analysis

This flexibility ensures PASTAL can be integrated into various applications where different outputs are needed based on the desired behavior.
</details>

<details open>
<summary>Use Cases</summary>
  
### Copyright Violation Detection
When generating or processing content with AI models, avoiding unauthorized reproduction of copyrighted materials is critical. PASTAL prevents circumvention by detecting phonetic approximations of lyrics, text, or speech, where models might otherwise be tricked into producing forbidden output. For instance, using "wooden tit" to trick a music generation AI into singing "wouldn't it."

### Profanity Filtering
Profanity filters often rely on exact string matches, leaving them vulnerable to clever re-spellings or phonetic approximations that result in the same offensive speech. PASTAL addresses this gap by detecting sound-alike words, ensuring filtered terms can't be easily bypassed. For example, "f***" could be spelled differently or replaced with phonetic equivalents but would still be caught.

### Adversarial Testing for AI Models
PASTAL helps ensure AI models, particularly in natural language generation, aren't fooled by cleverly manipulated inputs designed to trigger undesired or forbidden outputs. This is important for content moderation, legal compliance, and preventing harmful misuse of generative models.

### Detection of Similar Yet Distinct Text in Plagiarism Detection
PASTAL can be used to detect more sophisticated plagiarism attempts where text isn't exactly copied but altered phonetically or semantically. This ensures that plagiarized content can't bypass detection by simply swapping out words with homophones or similar meanings.
</details>

## Installation
To install PASTAL, simply run:

```bash
Copy code
pip install pastal
```

<details open>
<summary>API Overview</summary>
Here’s a brief overview of PASTAL’s primary functions. Each function is built to accommodate specific use cases, offering developers flexibility in how they apply the library.

1. detect_phonetic_match(input_text, target_text, phonetic_threshold=0.8)
Detects if the input text sounds like the target text based on a phonetic similarity threshold.

2. detect_semantic_match(input_text, target_text, semantic_threshold=0.75)
Detects if the input text has a similar meaning to the target text based on a semantic similarity threshold.

3. detect_phonetic_and_semantic_match(input_text, target_text, phonetic_threshold=0.8, semantic_threshold=0.75)
Combines phonetic and semantic analysis to detect approximate matches on both fronts.

4. get_phonetic_alternatives(input_text)
Returns a list of phonetic variations for a given input text, useful for identifying alternate spellings or sound-alike words.

5. get_semantic_alternatives(input_text)
Returns a list of semantically related phrases for a given input, helpful for detecting rephrased text.

</details>

Contributing
We welcome contributions! Whether you’re fixing bugs, adding new features, or improving documentation, your efforts are highly appreciated.

To get started, simply fork this repo and submit a pull request.

License
This project is licensed under the MIT License—see the LICENSE file for details.

Roadmap
Adversarial Test Suite: A set of adversarial examples for testing model robustness against phonetic and semantic attacks.
Model Training Extensions: Integration with AI models to extend their filtering capabilities, ensuring they can detect phonetic/semantic attempts to generate forbidden content.
Advanced Profanity Filter: Enhance the profanity filter by leveraging both phonetic and semantic analysis to close loopholes in current systems.
Plagiarism Detection Enhancement: Improve upon existing plagiarism detection methods by integrating homophone-based detection and semantically equivalent text identification.

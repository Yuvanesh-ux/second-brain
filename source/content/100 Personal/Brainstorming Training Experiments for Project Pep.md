
## Acquiring the Dataset

Initial explorations are to incorporate the method used in the DeepSeekMath paper


 > Step 1: Select [OpenWebMath](https://arxiv.org/pdf/2310.06786.pdf), a collection of high-quality mathematical web texts, as our initial seed corpus for training a FastText model.
 > Step 2: Use the FastText model to retrieve mathematical web pages from the deduplicated Common Crawl database.
 > Step 3: Identify potential math-related domains through statistical analysis.
 > Step 4: Manually annotate URLs within these identified domains that are associated with mathematical content.
 > Step 5: Add web pages linked to these annotated URLs, but not yet collected, to the seed corpus. Jump to step 1 until four iterations. 
 
 We can customize it to Pep by using __ as the inital seed corpus to the train the FastTest model

This will allow us to retrieve chess web pages from the depuped CC

### Initial Seed Corpus

1. **Compile a list of documents** from public domain books, annotated PGN files, articles, and forum discussions.
2. **Format each document** as plain text with optional metadata fields.
3. **Label the documents** as “chess-related” for positive examples.
4. **Prepare a parallel set** of non-chess documents labeled as “non-chess.”
5. **Decide on granularity** (document-level or chunks) based on the content length.
# PyCon2022-Notes
Notes from 2022 PyCon tutorials and talks - code is in separate repositories.

## Intro to NLP
Google colab notebook: https://colab.research.google.com/drive/1eF_ygaoPaBLpCORbquwGxDZFpaXjk5jX?usp=sharing \
NLP jargon
- Tokens - character level, word level (the usual), unigrams (she, was, offered, the), bigrams (she was, offered the), char level (sh, he, wa, as)
- Document - group of tokens: collection of tokens, essentially all the text in a word file
- Corpus - group of documents
- Vocabulary - unique set of tokens in the corpus (capitalization and punctuation matters here so “The” and “the” are two unique tokens
Preprocessing Text: **all of these are good sometimes and not good sometimes, and order matters!**
- Normalization: lowercase all terms, remove punctuation, remove numbers, remove stop words - words that don’t carry a lot of value (be careful, stopwords can capture abbreviations - IT/it, etc)
- Tokenization: separate text into smaller units
- Stemming: remove the last characters of a word - play/played/playing -> play, not an especially smart process so use carefully
- Lemmatization: convert a word to its root form - similar to above but a smarter process
- Stemming: good/better/best -> good/bett/best
- Lemmatization: good/better/best -> good/good/good
Spacy
- Open source library
- Pre-trained pipeline for processing text \
	**Many packages can do these things** 
- NER (named entity recognition)
  - Identify real world objects
people , nationalities, countries, and many more
  - Model based, so there may be errors
- Parts of speech (POS) tagging
  - Identify the part of speech for each token
  - Used for lemmatization and NER
  - Can be used for translation tools
- Dependency parsing: analyze structure of a sentence based on the dependencies between words (sentence diagrams, essentially) \
Term Frequency
- The number of times a token appears in the corpus or in a specific document
- A great way to summarize data \
Sklearn count vectorizer
- Converts text into a matrix of token counts
- Stop_words - can use non, built in english, or pass your own list
- Ngram_range: allows us to view popular words and phrases \
EDA -> top words in data set (exploratory data analysis) \
Text Similarity: determine how similar two documents are \
- Lexical similarity: the shared words of the documents \
- Semantic similarity: the meaning of the documents \
- Use cases: \
  - Remove duplicates
  - Recommendation system
  - Plagiarism
  - Search engine
-Distance metrics:
  - Jaccard similarity: treat tokens as a set and take the intersection divided by the union
  - Cosine similarity: measures the cosine of the angle between the vector of the two documents
  - TFIDF (term frequency - inverse document frequency), a way to represent a document as a vector
    - Term frequency is the relative frequency a token occurs in a document
    - Inverse document frequency is a measure of how often a token occurs in the corpus I.E. how much information does the token provide
  - Edit distance: the number of edits to transform one document into another
    - Levenshtein distance - has a tendency to not work well with documents of different length
    - Jaro-winkler distance
      - Transpose
      - Prefix
Topic  modeling:
- Latent semantic analysis (LSA): linear algebra approach
    - Based on distributional hypothesis
    - Unsupervised learning
    - Uses tfidf and singular value decomposition
  - Finding the optimal number of topics
    - Silhouette coefficient: consider each topic a separate cluster and calculate
    - Topic coherence: find the average or median pairwise word similarity scores for the words present
  - Latent dirichlet allocation (LDA) 
    - Unsupervised learning
    - Ignores ordering of words
    - Probabilistic

## Metaprogramming
pycon2022.pym.dev, psswrd arbitrary

## Network Analysis Made Simple
All notes in the jupyter notebooks.

### Python Oddities Explained
Given by the same guy that gave the metaprogramming tutorial - no notes as I didn’t have wifi in that room

### D&D and G - A daring tale of Dungeons and Dragons and also Graphs
- Graphs are data structures that codifies systems as entities and relationships
- Treat relationships as first-class members
  - Directional
  - Transitive \
(Random thought, consider breaking IP list up into individual dfs per signature, merging to get the IPs as nodes and the sig as an edge attribute) \
- Representing graphs in python
  - Matrices
  - Edge list
  - Dictionary (better for directed graphs), nodes are keys with each node they connect to as the items
- **YOU MEET IN A TAVERN** - you get a lager, need to get through the busy bar - but what path do you take?
  - The corridors are edges and the intersections are nodes
  - Can use **breadth first search** (you have notes on this in the network analysis notebook) - can build graph on the fly with breadth first search
  - What are the important nodes?
    - Articulation nodes
      - Nodes in a graphs that reduce connectivity
    - Degree centrality
  - Community detection - lots of algorithms here
  - What happens when graph algorithms fail?
    - What does success/failure look like?
    - Is the algorithm implemented correctly?
    - Maybe redefine what the node/edges are?

### Sculpting Data for Machine Learning
Well-Calibrated Data \
Sophisticated algorithms \
Efficient Calculations \
Modern approaches are data hungry \
Better data beats more data. \
In search of data sources:
- Clothing fit dataset (modcloth)
- Sarcasm detection (theOnion and HuffPost)
  - Sarcastic news, non-sarcastic/real news
- News category (HuffPost) \
Approach (guided search):
- Formal problem definition
- Essential data signal determination
- Data volume requirement \
Approach (unguided search): collecting data without a problem in mind and then determining how that data can be useful.
- Interesting problem recognition
  - Data signals worth estimating?
  - Lead to fascinating results?
- Metadata association
- Data volume requirement (more relaxed constraint than before, can adjust on the fly)
- Data uniqueness check \
Dataset preparation
- Data trimming
  - All data records my not contain essential data signals
  - Exclude records with irrelevant, redundant, or extreme information
- Data integration
- Data transformation: scrub datasets raw values to remove redundancies and correct language and logical semantics \
Feature Engineering: typically where most of the effort goes

### What to do when the bug is in someone else’s code
https://github.com/pganssle-talks/pycon-us-2022-upstream-bugs \
The right thing to do - file an issue upstream, maybe even submit a patch! \
Lots of things can go wrong - production deadlines, long upstream release cycles (it was fixed upstream but not locally), long deployment cycles in house \
What to do in the meantime:
= Work around the bug, good if:
  - The bug is in exactly in one place
  - The workaround is easy
  - You’re indifferent to how the code works
- Wrapper function
  - Encapsulates complicated workaround logic
  - Provides an easy target for later removal
  - A little hacky
- Opportunistic upgrading (fancy if/then, essentially), provide a workaround iff the bug is present
- **Monkey patching**: dynamically modify the code you want to patch at runtime
  - Fixes the issue globally and transparently
  - May fix the issue in other code you don’t control
  - Why is this a terrible idea?
    - Action at a distance
    - No one is expecting you to do this
- Vendoring: include a copy of one or more of your dependencies in the project source code
  1. Copy source code into your project tree somewhere
  2. Update references
  3. Apply patches to your local copy
- Maintaining a fork
  - Mostly accomplished with .patch files
  - You’re maintaining a fork that your upstream doesn’t know about
  - Updating all your patches adds friction to the upgrade process
  - No guarantees of compatibility

### Handling Timezones in Python
Benjamin Zagorsky (Zagoran Software) \
Python 3.9 zoneinfo added to python standard library \
Handling timezones wrong - 5 cardinal sins
- Don’t use naive datetimes EVER (use the tzinfo=timezone.utc (or whatever) when using datetime) SPECIFY the timezone when using datetime!
- Don’t use datetime.now() or datetime.utcnow(), they depend on system time and return a naive datetime
- Don’t use dates without a timezone
- Don’t use date.today(), same reason as above
  - Can lead to bugs that only show up between 7pm and midnight
- Don’t do duration arithmetic outside of UTC
- Don’t use pytz
- Don’t replace the timezone info for an aware datetime (that has timezone info)
- Don’t do aware_datetime.replace(tzinfo=xxx) \
Handling timezones right
- UTC: Coordinated Universal Time
  - Has no temporal discontinuities (except for leap seconds)
  - All other timezone are defined in relation to UTC
  - It’s the official timezone of the international space station and space is cool
- Use Zoneinfo (instead of pytz): from zoneinfo import zoneinfo \
Common recipes
- Get current time
  - datetime.now(timezone.utc)
- Get current date
  - datetime.now(ZoneInfo(“America/New_York”)).date()
- If you have dates, do datetime on dates
- Look into django

### Securing Code with the Python Type System
SQL injection attack (or any other command injection attack) \
- First of all - separate the sql command from the data!!! (don’t use query=f”””this is the quere”””)
- Can use a type checker (def (query: str) -> Cursor: .. BUT this is too permissive - there is a literal string type def thing(s: LiteralString) -> int: . . . 
- Type annotations shift the burden of security thinking to library authors and off of the user
- External data validation
  - Body = json.loads(request.body)
  - Picture_id = “.../etc/passwd”   BAD, need to validate that the user is inputting the correct kind of thing
  - Runtime type validation
- Data flow analysis

### Testing Machine Learning Models
Test early, test often \
Define the problem
- What are we trying to solve?
- Who is the ML for?
- Does this even need ML? \
Define success and assess risk
- Define initial baselines
- Consider privacy and security risks
- Create a proof of concept
- Do we have the proper resources to do this \
Design the initial architecture
- Which DB or tables will we pull data from
- What does our ELT process look like 
- others \
Collect data
- Where is the data coming from
- Is this different than STAGE or DEV
- Where are we storing the data
- Is the data streamed and/or batched
- Understand the data journey \
Prepare data
- Are there any missing values or errors
- Poop data makes poop models
- What are the data types
- What shapes does the data need to be in \
Train and validate models
- Use tests (exploratory and automated)
- Tune weights and parameters
- Visualize results for further analysis
- Capture training and validation metrics
- Experiment and compare multiple models \
Test the models
- What behaviors does the model show
- Does it demonstrate harmful biases
- Is it performant and reliable
- Does it solve the problems that we set out to solve
- Does it meet privacy and security requirements \
Deploy the model \
Observe and iterate 
- Monitor
- Measure
- Alert
- Insights
- learn




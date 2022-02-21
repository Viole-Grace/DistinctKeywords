# DistinctKeywords
This is a utility function to extract semantically distinct keywords. This is an unsupervised method based on word2vec. Current implementation used a word2vec model trained in simplewiki. 
Hilbert curve act as a Locality-sensitive hashing. 

## Methodology

After creating word2vec, the words are mapped to a hilbert space and the results are stored in a key-value pair (every word has a hilbert hash). Now for a new document, the words and phrases are cleaned, hashed using the dictionary. One word from each different prefix is then selected using wordnet ranking from NLTK (rare words are prioritized). The implementation of grouping and look up is made fast using Trie and SortedDict
![enter image description here](https://github.com/sahyagiri/DistinctKeywords/raw/main/steps_hilbert_hashing.png)
## Installation Instructions
1. conda create -n  keyphrases python=3.8 --no-default-packages
2. conda activate keyphrases
3. pip install distinct-keywords
4. python -m spacy download en_core_web_sm
5. conda install --channel=conda-forge nb_conda_kernels jupyter
6. jupyter notebook 

## Model Files for processing (English)

Download the following files and keep it in the current working directory. 

1. [Hilbert Lookup Dictionary](https://github.com/sahyagiri/DistinctKeywords/blob/main/hilbert_lookup_dictionary_simplewiki_17_2_22_v3.pickle.gz?raw=true)

2. [KeyWordProcessor](https://github.com/sahyagiri/DistinctKeywords/blob/main/keyword_processor_simple_wiki2022.pickle?raw=true)

3. [Stop Words](https://github.com/sahyagiri/DistinctKeywords/blob/main/stopwords.pickle?raw=true)

## Benchmarks

Currently this is tested against KPTimes test dataset (20000 articles). A recall score of 30% is achieved when compared to the manual keywords given in the dataset. 

## Usage
```
from keywords import DistinctKeywords

doc = """
         Supervised learning is the machine learning task of learning a function that
         maps an input to an output based on example input-output pairs. It infers a
         function from labeled training data consisting of a set of training examples.
         In supervised learning, each example is a pair consisting of an input object
         (typically a vector) and a desired output value (also called the supervisory signal). 
         A supervised learning algorithm analyzes the training data and produces an inferred function, 
         which can be used for mapping new examples. An optimal scenario will allow for the 
         algorithm to correctly determine the class labels for unseen instances. This requires 
         the learning algorithm to generalize from the training data to unseen situations in a 
         'reasonable' way (see inductive bias).
      """



distinct_keywords=DistinctKeywords()

distinct_keywords.get_keywords(doc)

  ```
## Output

['machine learning',
 'pairs',
 'mapping',
 'vector',
 'typically',
 'supervised',
 'bias',
 'supervisory',
 'task',
 'algorithm',
 'unseen',
 'training']

## German Model (On test) 
I have added a german model based on word2vec found at https://devmount.github.io/GermanWordEmbeddings/
You can find it in the example folder. If anyone here can test it/ suggest a better light German word2vec file, please share 

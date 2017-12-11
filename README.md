# Six Line Search Engine
This project demonstrates how to write a fast document search engine using pandas, NLTK and a simple Python dictionary.

Not including data cleaning or import statements, it consists of six lines of code to index the document (in this case, all of Shakespeare). After that, the code to search the index is a one line function.

Here they are:
````python
# These don't count
import pandas as pd
from nltk.stem import PorterStemmer
from nltk.tokenize import word_tokenize
from collections import defaultdict
df = pd.read_csv('shakespeare.csv')

# These count
ps = PorterStemmer() # 1
word2idx = defaultdict(list) # 2
for row in df.itertuples(): # 3
    for word in word_tokenize(row.Line): # 4
        if word.isalpha(): # 5
            word2idx[ps.stem(word.lower())].append(row.Index) #6
            
# And to search:
def search(term):
    return df.loc[[idx for idx in word2idx[ps.stem(term.lower())]]]
````

The code is demonstrated in the [Jupyter notebook](https://github.com/jeremyadamsfisher/7-line-search-engine/blob/master/Searchspeare.ipynb) above.

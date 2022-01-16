# Relevant Document Data Extraction

We have to remember that our goal is to collapse topics into small values and to keep in mind that the "hidden" meanings are important, in other words, the projection of the term *apple* in the similarity space should be in the same region than the projection of the term *phone*, as well as close to the projection of the term *fruit*. Term weighting is an additional step to get more meaning quality.

## Term weighting

The idea of term weighting is to take into account specific words that often appear or in most documents. To do so, instead of having the *term document matrix*, we compute a transformation of the elements of that matrix.

$$ a_{ij} = \frac{log(d_{ij}) log(\frac{n}{\sum_{j}\chi(d_{ij})})}{\sqrt{\sum_{i}[log(d_{ij}+1)log(\frac{n}{\sum_{j}\chi(d_{ij})})]}} $$

Please, note that we compute the logarithm of the elements of the term document matrix $d_{ij}$, every time we have $log_{10}(·)$ of something. That means that the important information is the number of digits we need to represent that. In order to understand the formula:

* $n$ is the number of documents.
* $\chi(d_{ij})$ is an indicator function. It determines if a word appears in the document $j$ or not.

Words common to all documents are irrelevant, for example, in the corpus of a medical text the word ”*patient*” gives us no information. Because of that, we define $log(\frac{n}{\sum_{j}\chi(d_{ij})}) = log(\frac{\verb|documents|}{\verb|# documents with word i|})$. Due to $log(\frac{n}{\sum_{j}\chi(d_{ij})})$ we are able to give more or less importance to words. When a word appears in all documents its value will be $log(\frac{n}{n})=log(1)=0$. In other words, this term allows us to penalize most common words and make more relevant the ones that are not as frequent.
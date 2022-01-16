# Similarity between texts

Any graph created from a social network or the different pages from the internet, takes much higher value if takes into account the distance between texts. The idea is to get a distance between tests that has the following properties:

* It should not depend on their length.
* It should capture meaning (semantics) - something that we would like to get explicitly in the correct context.
* It must deal with non-trivial synonyms (for example apple, computer, phone).

Some classical linear algebra tools we can use for projection are Singular Value Decomposition (SVD) and QR Decomposition.

## Vector Space Model

We create a table from a collection of all the documents. This table is called **term document matrix**, and consists in a one-hot encoding of the terms (in rows) for each document (in columns). However, what we would like is to have a relationship between synonyms (in rows) and topics (in columns).

Since we have a one-hot encoding representation of words in documents, the score of a query (which will be a one-hot vector too) is related with the dot product:

$$ score = query^{T}[term doc mat] = [q^{T}_{doc_{1}}, q^{T}_{doc_{2}}, ..., q^{T}_{doc_{N}}] $$

The meaning of dot product is actually a projection. We want to go from the term document matrix space to a lower dimension subspace where vectors are projected grouped by the topics they have.

## Document preparation

Before the projection, some pre-processing should be applied to the documents in order to optimize the results and avoid some of the term document matrix representation issues.

1. **Extract tokens**. Extract everything between blancks using regular expressions.

2. **Filter symbols**. Remove any unwanted symbol since html tags, punctuation marks, etc.

3. **Normalize to lower case**. We must normalize all the document to standard basic letter, we clear all bold and italic texts and we convert everything to lower case letters.

4. **Remove stop words**. There are many words (articles, pronouns), like ”to”, ”the”, ”me”, that don’t variate the meaning of the document if we remove them. There is a list of about 300 meaningless words.

5. **Stemming** (*Optative*): Eliminate grammar functions. Clear the word composition. For example: Reform, Reformative, Reformation, Reformism, have the same core word, but they all derive from Reform.

After this document preparatoin, we would have a document matrix like it follows:

$$ \mathbf{A} =
  \begin{pmatrix}

    \begin{pmatrix}
        \vdots \\ d_{1} \\ \vdots
    \end{pmatrix}
    &
    \begin{pmatrix}
        \vdots \\ d_{2} \\ \vdots
    \end{pmatrix}
    &
    \ldots
    &
    \begin{pmatrix}
        \vdots \\ d_{j} \\ \vdots
    \end{pmatrix}
    &
    \ldots
    &
  \end{pmatrix}
$$

where $d_{ij}$ is the number of times that word $i$ appears in document $j$.
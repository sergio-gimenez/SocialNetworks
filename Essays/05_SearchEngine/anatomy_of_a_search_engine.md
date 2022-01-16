# Anatomy of a Search Engine

The search engine is composed by two main components: the **crawler** and the **distributed database**. The **crawler** is the machine that explores all the network, follows all links and indexes the visited pages. Ok, the crawler needs to store all the useful information he finds in the network. The guys at Google invented a new type of database called _Non-Relational Database_. This **distributed database** consists on:

* An adjacency matrix $\mathbf{A}$ of size $N_{doc}$ x $N_{doc}$ implemented as a list of columns with a list of occupied rows.
* An inverted index. This is a list of words that point to the document where they appear, plus some other relevant information. 

The operation of the search engine works as follows:

1. Given a _query_ or set of words, the engine filter by function words (that is, drop prepositions, articles, etc.) and look at the inverted index (dictionary where keys are the words and values are a list of documents where the key-word appears).

2. Compute the score of documents given a keyword. The formula to get this score is secret.

3. Get a rank of document by intent. The result is a list of tuples composed by a document and the score of that document for the keyword given.

4. For each selected document, get the PageRank from the graph computed a priori (database) also as a list of tuples.

5. Get a score that combines the PageRank and the score for the query:

    $$ score = \alpha(PageRank, Document) + \beta(QueryScore, Document) $$

## Search engine Optimization

In order to optimize the rank of a page in Google, there are three main factors: 

1. Structure of the web/graph.

2. Structure of the document.

3. Social networks, but only 1 and 2 will be explained.

In a usual web page, there is a main document which points to other documents of the same web page, but it does not have input links from that documents. This structure ends in these documents pointed by the main one are **dangling nodes**. Hence, when the search engine is surfing through the network, as seen in previous lessons, will jump from that webpage to another one to avoid the dangling nodes. A solution to that problem is to interconnect the different documents of the web in order to not do it as dangling nodes.

Another way to increase the rank of our page is if we have input links from other pages. However, it is not a good idea to create single-pages that points to our webpage since Google could detect it and penalize us. Instead, it is recommendable to create small nets, in a long period of time and from different IP’s, that have  links to our main page. Moreover, our rank will also raise if we have input links from pages with a high rank.

Finally, once we have our page structure set, it is time to focus on the content of the documents. The name of the MUST be related with the content of the document, we should use keywords on metadata, and we should also add anchor texts, set important text in bold, do not repeat text and use synonyms instead, avoid copy and keep the main points in first 5000 words.

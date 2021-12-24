# Ranking Systems

In this essay we will describe what is the intuition behind a ranking system. We will analyze the math behind the Google PageRank algorithm and try to understand in a high level how the most famous search engine sort the search result once a user makes a search query.

A ranking system is a method of assigning a numerical value to each item in a set, and the value of an item is determined by the order in which it appears in the set. To give more context, one of the widest used ranking system is Google's [PageRank](https://en.wikipedia.org/wiki/PageRank).  When using Google, once a query is done, Google's outcome is an ordered list of webpages such that the pages near the top are most likely to be what the user is looking for.

## The Original (Incomplete) approach.

PageRank (PR) is an algorithm used by Google Search to rank web pages in their search engine results. It is named after both the term "web page" and co-founder Larry Page. According to Google:

> PageRank works by counting the number and quality of links to a page to determine a rough estimate of how important the website is. The underlying assumption is that **more important websites are likely to receive more links from other websites**

*Irrelevant note: The PageRank algorithm was initiali named BackRub because this idea on checking backlings to determine a site's importance.*

Google's founders began with a simple summation equation based on the underlaying idea of **the more pages point me, the more important I am**. The PageRank of a page $P_{i}$, denoted $r(P_{i})$, is the sum of all the PageRanks pointing into $P_{i}$.

$$r(P_{i}) = \sum_{j \in B_{P_{i})}} \frac{r(P_{j})}{{|P_{j}|}}$$

Let's analyze the elements of the equation.
* $P_{i}$ refers to the a page of label $i$.
* $r(P_{i})$ is a continous value assigned to a page $i$.
* $B_{P_{i}}$ are the *[backlinks](https://en.wikipedia.org/wiki/Backlinks)* i.e., the set of pages that link to $P_{i}$. This is a quite difficult value to find, because we need to explore the grph in order to find this value.

So, the PR of a website $P_{i}$, denoted $r(P_{i})$, is the sum of all the PageRanks pointing into $P_{i}$.

![PageRank](PageRank-hi-res.png)  
*Cartoon illustrating the basic principle of PageRank. The size of each face is proportional to the total size of the other faces which are pointing to it. [source](https://en.wikipedia.org/wiki/PageRank)*

The main problem with the previous equation is that $r(P_{j})$ values are unknown.
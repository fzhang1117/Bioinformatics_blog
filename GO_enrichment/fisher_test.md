# Fisher Test in GO/KEGG enrichment Analysis #

**Fisher's exact test** is a statistical significance test used in the analysis of contingency tables. The fisher's exact test could be used in GO and KEGG enrichment analysis.

## Example ##

Consider we have found **300** Different Expressed Genes (DEGs) from **10000** genes, and **80** genes in DEG was also in a pathway have **100** genes.
Now we can list the contingency table like that:

|                    |  **DE**   | **Not DE** |   Row total  |
| :--------------:   | :------:  |   :------: |   :------:   |
|  **In Pathway**    |  **80**   |   **20**   |      100     |
| **Not in Pathway** |  **220**  |   **9680** |     9900     |
|   Column total     |    300    |    9700    |    10000     |

Now we write the example in a **common format**:
Consider we have found **x** Different Expressed Genes (DEGs) from **n** genes, and **a** genes in DEG was also in a pathway have **y** genes.

|                    |     **DE**    | **Not DE**|       Row total      |
| :--------------:   |    :------:   |  :------: |       :------:       |
|  **In Pathway**    |     **a**     |   **b**   |       a + b( = y)    |
| **Not in Pathway** |     **c**     |   **d**   |       c + d          |
|   Column total     |  a + c( = x)  |   b + d   | a + b + c + d ( = n) |

We know **x**, **y**, **a** and **n**

```
b = y - a
c = x - a
d = n - y - c = n - y - ( x - a ) = (n + a) - (x + y)
```

Then we can use the function **fisher.test()** in R to do Fisher's Exact Test:

```R
a <- 80
b <- 20
c <- 220
d <- 9680

mat <- matrix(c(a, c, b, d), 2, 2)
result <- fisher.test(mat, alternative = "greater")

```

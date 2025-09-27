# CMPS 6610 Problem Set 03
## Answers

**Name:** Abby Ortego


Place all written answers from `problemset-03.md` here for easier grading.


- **1b.**
    - The **work** of `isearch`:
        - Since `iterate` is called recursively, work can best be expressed as a recurrence, $W(n) = W(n-1) + 1$
            - With input size $n$, `iterate` is called recursively on $n-1$ sized inputs so it's cost is $W(n-1)$
            - The inner function of `isearch`, `check`, compares two integers which can be done in constant time so it's cost is $1$
        - Solving the recurrence...
            - $C\texttt{(Root)} = 1$
            - $C\texttt{(1st Level)} = W(n-2) + 1 + 1$
            - Cost is neither increasing nor decreasing so this is balanced. Number of levels is $n$ and the max cost per level is $1$.
        - Therefore, the work of `iterate` is $\mathcal{O}(n)$
    - The **span** of `isearch`:
        - Similar to above, **Span** can also be expressed as a recurrence. This approach cannot be parallelized so it will produce the same recurrence as above, $W(n) = W(n-1) + 1$. 
        - Solving the recurrence...
            - $C\texttt{(Root)} = 1$
            - $C\texttt{(1st Level)} = W(n-2) + 1 + 1$
            - Cost is neither increasing nor decreasing so this is balanced. Number of levels is $n$ and the max cost per level is $1$.
        - Therefore, the span of `iterate` is also $\mathcal{O}(n)$


- **1d.**
    - The **work** of `rsearh`: 
        - Since `reduce` is called recursively its **work** can best be expressed as a recurrence, $W(n) = 2W(\frac{n}{2}) + 1$
            - With input size $n$, `reduce` is called recursively twice on $\frac{n}{2}$ sized inputs so it costs $2W(\frac{n}{2})$
            - The inner function of `rsearch`, `check`, compares the two integers to the key which can be done in constant time so it's cost is $1$
        - Solving the recurrence...
            - $C\texttt{(Root)} = 1$
            - $C\texttt{(1st Level)} = 2(2W(\frac{n}{4}) + 1) + 1 = 2^2W(\frac{n}{4}) + 2 + 1$
            - Cost is increasing so this is leaf dominated. Number of leaves is $2^{\log_2(n)} = n^{\log_2(2)}$
        - Therefore, the work of `reduce` is $\mathcal{O}(n)$
    - The **span** of `rsearch`:
        - Since `reduce` is called recursively its span can also best be expressed as a recurrence, $S(n) = S(\frac{n}{2}) + 1$
            - The two recursive calls `reduce` makes on $\frac{n}{2}$ sized inputs can be done at the same time so it costs $S(\frac{n}{2})$
            - The inner function of `rsearch`, `check`, compares the two integers to the key which can be done in constant time so it's cost is $1$
        - Solving the recurrence...
            - $C\texttt{(Root)} = 1$
            - $C\texttt{(1st Level)} = S(\frac{n}{4}) + 1 + 1$
            - Cost is neither increasing nor decreasing so this is balanced. Number of levels is $\log_2 n$ and the max cost per level is $1$.
        - Therefore, the span of `reduce` is $\mathcal{O}(\log_2 n)$


- **1e.**
    - The **work** of `rsearch` w/ `ureduce`: 
        - The work can best be expressed as the recurrence, $W(n) = 2W(\frac{n}{3}) + 1$
            - With input size $n$, `reduce` is called recursively three times on $\frac{n}{3}$ sized inputs so it costs $2W(\frac{n}{3})$
            - The inner function of `rsearch`, `check`, compares the two integers to the key which can be done in constant time so it's cost is $1$
        - Solving the recurrence...
            - $C\texttt{(Root)} = 1$
            - $C\texttt{(1st Level)} = 2(2W(\frac{n}{9}) + 1) + 1 = 2^2W(\frac{n}{9}) + 2 + 1$
            - Cost is increasing so this is leaf dominated. Number of leaves is $2^{\log_9(n)} = n^{\log_9(2)}$
        - Therefore, the work of `reduce` is $\mathcal{O}(n^{\log_9(2)})$
    - The **span** of `rsearch` w/ `ureduce`:
        - The span can also best be expressed as a recurrence, $S(n) = S(\frac{n}{3}) + 1$ 
            - The two recursive calls `reduce` makes on $\frac{n}{3}$ sized inputs can be done at the same time so it costs $S(\frac{n}{3})$
            - The inner function of `rsearch`, `check`, compares the two integers to the key which can be done in constant time so it's cost is $1$
        - Solving the recurrence...
            - $C\texttt{(Root)} = 1$
            - $C\texttt{(1st Level)} = S(\frac{n}{9}) + 1 + 1$
            - Cost is neither increasing nor decreasing so this is balanced. Number of levels is $\log_3 n$ and the max cost per level is $1$.
        - Therefore, the span of `reduce` is $\mathcal{O}(\log_3 n)$


- **3b.**
    - The **work** of `parens_match_iterative` is detailed below. 
        - The work recurrence is $W(n) = W(n-1) + 1$
            - Since `iterate` applies the function to one less item of the list each time it's cost is $W(n-1)$
            - The inner function `parens_update` can apply the if/else statements in constant time so it's cost is just $1$
        - Solving the recurrence...
            - $C\texttt{(Root)} = 1$
            - $C\texttt{(1st Level)} = W(n-2) + 1 + 1$
            - Cost is neither increasing nor decreasing so this is balanced. Number of levels is $n$ and the max cost per level is $1$.
        - Therefore, $W(n) = \mathcal{O}(n)$
    - The **span** of `parens_match_iterative` is detailed below. 
        - The span recurrence is $S(n) = S(n-1) + 1$
            - Since `iterate` applies the function to one less item of the list each time and it can't be parallelized it's cost is $S(n-1)$
            - The inner function `parens_update` can apply the if/else statements in constant time so it's cost is just $1$
        - Solving the recurrence...
            - $C\texttt{(Root)} = 1$
            - $C\texttt{(1st Level)} = S(n-2) + 1 + 1$
            - Cost is neither increasing nor decreasing so this is balanced. Number of levels is $n$ and the max cost per level is $1$.
        - Therefore, $S(n) = \mathcal{O}(n)$


- **3d.**





- **3f.**


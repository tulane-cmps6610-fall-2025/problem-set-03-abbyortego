# CMPS 6610 Problem Set 03
## Answers

**Name:** Abby Ortego


Place all written answers from `problemset-03.md` here for easier grading.

### Part I
- **1b.**
    - The **work** of `isearch`:
        - Since `iterate` is called recursively, work can best be expressed as a recurrence, $W(n) = W(n-1) + 1$
            - With input size $n$, `iterate` is called recursively on $n-1$ sized inputs so it's cost is $W(n-1)$
            - The inner function of `isearch`, `check`, compares two integers which can be done in constant time so it's cost is $1$
        - Solving the recurrence...
            - $C\texttt{(Root)} = 1$
            - $C\texttt{(1st Level)} = W(n-2) + 1 + 1$
            - Cost is neither increasing nor decreasing so this is balanced. Number of levels is $n$ and the max cost per level is $1$.
        - Therefore, the work is $\mathcal{O}(n)$
    - The **span** of `isearch`:
        - Similar to above, span can also be expressed as a recurrence. This approach cannot be parallelized so it will produce the same recurrence as above, $S(n) = S(n-1) + 1$. 
        - Solving the recurrence...
            - $C\texttt{(Root)} = 1$
            - $C\texttt{(1st Level)} = S(n-2) + 1 + 1$
            - Cost is neither increasing nor decreasing so this is balanced. Number of levels is $n$ and the max cost per level is $1$.
        - Therefore, the span is also $\mathcal{O}(n)$


- **1d.**
    - The **work** of `rsearh`: 
        - Since `reduce` is called recursively its work can best be expressed as a recurrence, $W(n) = 2W(\frac{n}{2}) + 1$
            - With input size $n$, `reduce` is called recursively twice on $\frac{n}{2}$ sized inputs so it costs $2W(\frac{n}{2})$
            - The inner function of `rsearch`, `check`, compares the two integers to the key which can be done in constant time so it's cost is $1$
        - Solving the recurrence...
            - $C\texttt{(Root)} = 1$
            - $C\texttt{(1st Level)} = 2(2W(\frac{n}{4}) + 1) + 1 = 2^2W(\frac{n}{4}) + 2 + 1$
            - Cost is increasing so this is leaf dominated. Number of leaves is $2^{\log_2(n)} = n^{\log_2(2)}$
        - Therefore, the work is $\mathcal{O}(n)$
    - The **span** of `rsearch`:
        - Since `reduce` is called recursively its span can also best be expressed as a recurrence, $S(n) = S(\frac{n}{2}) + 1$
            - The two recursive calls `reduce` makes on $\frac{n}{2}$ sized inputs can be done at the same time so it costs $S(\frac{n}{2})$
            - The inner function of `rsearch`, `check`, compares the two integers to the key which can be done in constant time so it's cost is $1$
        - Solving the recurrence...
            - $C\texttt{(Root)} = 1$
            - $C\texttt{(1st Level)} = S(\frac{n}{4}) + 1 + 1$
            - Cost is neither increasing nor decreasing so this is balanced. Number of levels is $\log n$ and the max cost per level is $1$.
        - Therefore, the span is $\mathcal{O}(\log n)$


- **1e.**
    - The **work** of `rsearch` w/ `ureduce`: 
        - The work can best be expressed as the recurrence, $W(n) = 2W(\frac{n}{3}) + 1$
            - With input size $n$, `reduce` is called recursively three times on $\frac{n}{3}$ sized inputs so it costs $2W(\frac{n}{3})$
            - The inner function of `rsearch`, `check`, compares the two integers to the key which can be done in constant time so it's cost is $1$
        - Solving the recurrence...
            - $C\texttt{(Root)} = 1$
            - $C\texttt{(1st Level)} = 2(2W(\frac{n}{9}) + 1) + 1 = 2^2W(\frac{n}{9}) + 2 + 1$
            - Cost is increasing so this is leaf dominated. Number of leaves is $2^{\log_9(n)} = n^{\log_9(2)}$
        - Therefore, the work is $\mathcal{O}(n^{\log_9(2)})$
    - The **span** of `rsearch` w/ `ureduce`:
        - The span can also best be expressed as a recurrence, $S(n) = S(\frac{n}{3}) + 1$ 
            - The two recursive calls `reduce` makes on $\frac{n}{3}$ sized inputs can be done at the same time so it costs $S(\frac{n}{3})$
            - The inner function of `rsearch`, `check`, compares the two integers to the key which can be done in constant time so it's cost is $1$
        - Solving the recurrence...
            - $C\texttt{(Root)} = 1$
            - $C\texttt{(1st Level)} = S(\frac{n}{9}) + 1 + 1$
            - Cost is neither increasing nor decreasing so this is balanced. Number of levels is $\log_3 n$ and the max cost per level is $1$.
        - Therefore, the span is $\mathcal{O}(\log_3 n)$


### Part II
- **2a.** I was having some issues with getting the below latex to render on github (even though it rendered fine in my VS Code extension), so I have an alternative beneath it that doesn't use latex. 

$\texttt{dedup A} =\\
\texttt{let}\\ 
\texttt{iterate}(f, x, a)= 
    \begin{cases} 
      x & \texttt{if} |a|=0\\
      \texttt{iterate}(f, f(x, a[0]), a[:1]) & \texttt{otherwise}\\ 
    \end{cases}\\
\texttt{countDup}(\texttt{(count, key)}, a)= 
    \begin{cases} 
      \texttt{(count+1, key)} & \texttt{if } a=\texttt{key}\\
      \texttt{(count, key)} & \texttt{otherwise}\\ 
    \end{cases}\\
\texttt{isDup} (A, a) = \texttt{iterate}(\texttt{countDup}, [0, a], A)[0] \leq 1\\
\texttt{in}\\
\texttt{filter} (\texttt{isDup}, A) = \langle a : a \in A | \texttt{isDup}(A, a) \rangle\\$

``` 
dedup A = 
    let
        iterate(f, x, a) = 
            x   if |a| = 0
            iterate(f, f(x, a[0]), a[:1])   otherwise
        countDup((count, key), a) = 
            (count+1, key)  if a = key
            (count, key)    otherwise
        isDup(A, a) = iterate(countDup, [0, a], A)[0] <= 1
    in
        filter(isDup, A) = (a: a in A | isDup(A, a))
```
- The **work** of `dedup`:
    - `isDup` calls iterate which costs $W(n-1)$ and `countDup` which costs $1$
    - `filter` costs $n$ since it's applied to each item in the list
    - Solving the recurrence: $W(n-1) + 1 + n$
        - $C\texttt{(Root)} = 1 + n$
        - $C\texttt{(1st Level)} = W(n-2) + 1 + n + 1 + n$
        - Cost is neither increasing nor decreasing so this is balanced. Number of levels is $n$ and max cost per level is $n$. 
    - $W(n) = W(n-1) + 1 + n = \mathcal{O}(n^2)$
- The **span** of `dedup`:
    - `isDup` calls iterate which costs $S(n-1)$ and `countDup` which costs $1$
    - `filter` costs $1$ since it can be applied to each item in the list in parallel
    - Solving the recurrence: $S(n-1) + 2$
        - $C\texttt{(Root)} = 2$
        - $C\texttt{(1st Level)} = S(n-2) + 2 + 2$
        - Cost is neither increasing nor decreasing so this is balanced. Number of levels is $n$ and max cost per level is $1$. 
    - $S(n) = S(n-1) + 2 = \mathcal{O}(n)$


- **2b.**


- **2c.** Yes. Iterate is useful for getting a count of the number of times each item appears in the list and then returning if they're duplicates or not based on that. Filter is useful for filtering out items that are duplicates and returning a list with the distinct items. 


### Part III
- **3b.**
    - The **work** of `parens_match_iterative`: 
        - The work recurrence is $W(n) = W(n-1) + 1$
            - Since `iterate` applies the function to one less item of the list each time it's cost is $W(n-1)$
            - The inner function `parens_update` can apply the if/else statements in constant time so it's cost is just $1$
        - Solving the recurrence...
            - $C\texttt{(Root)} = 1$
            - $C\texttt{(1st Level)} = W(n-2) + 1 + 1$
            - Cost is neither increasing nor decreasing so this is balanced. Number of levels is $n$ and the max cost per level is $1$.
        - Therefore, $W(n) = \mathcal{O}(n)$
    - The **span** of `parens_match_iterative`: 
        - The span recurrence is $S(n) = S(n-1) + 1$
            - Since `iterate` applies the function to one less item of the list each time and it can't be parallelized it's cost is $S(n-1)$
            - The inner function `parens_update` can apply the if/else statements in constant time so it's cost is just $1$
        - Solving the recurrence...
            - $C\texttt{(Root)} = 1$
            - $C\texttt{(1st Level)} = S(n-2) + 1 + 1$
            - Cost is neither increasing nor decreasing so this is balanced. Number of levels is $n$ and the max cost per level is $1$.
        - Therefore, $S(n) = \mathcal{O}(n)$


- **3d.**
    - The **work** recurrence of `parens_match_scan`:
        - `map` costs $n$ since the function is applied to each item in the list
        - `scan` (if using contraction) for prefix sums costs $W(\frac{n}{2}) + 1$ since only one recursive call is made on $\frac{n}{2}$ sized input and adding two numbers can be done in constant time
        - `scan` (if using contraction) for finding the minimum cost $W(\frac{n}{2}) + 1$ since only one recursive call is made on $\frac{n}{2}$ sized input and comparing two integers can be done in constant time
        - $W(n)...$
            - $= n + W(\frac{n}{2}) + 1 + W(\frac{n}{2}) + 1$
            - $= W(\frac{n}{2}) + W(\frac{n}{2}) + 2 + n$
    - The **span** recurrence of `parens_match_scan`:
        - `map` cost $1$ since the function can be applied to the items simultaneously 
        - `scan` for prefix sums cost $S(\frac{n}{2}) + 1$ since parallelization doesn't change the cost of adding two numbers together
        - `scan` for finding the minimum costs $S(\frac{n}{2}) + 1$ work, as well, since parallelization doesn't change the cost of comparing two integers either
        - $S(n)...$
            - $= 1 + S(\frac{n}{2}) + 1 + S(\frac{n}{2}) + 1$
            - $= S(\frac{n}{2}) + S(\frac{n}{2}) + 3$


- **3f.**
    - The **work** recurrence of `parens_match_dc_helper`:
        - `base cases` cost $1$ since they take constant time 
        - In the `recursive case`...
            - computing the left and right side costs $2W(\frac{n}{2})$ since `parens_match_dc_helper` is called twice on $\frac{n}{2}$ sized inputs
            - combining the left and right side cost $1$ since the comparison, addition, and subtraction can be done in constant time
        - $W(n)...$
            - $= 1 + 2W(\frac{n}{2}) + 1 $
            - $= 2W(\frac{n}{2}) + 2$
        - Solving the recurrence $W(n) = 2W(\frac{n}{2}) + 2$...
            - $C\texttt{(Root)} = 2$
            - $C\texttt{(1st Level)} = 2(2W(\frac{n}{4}) + 2) + 2 = 2^2W(\frac{n}{4}) + 4 + 2$
            - Cost is increasing so this is leaf dominated. Number of leaves is $2^{\log_2(n)} = n^{\log_2(2)}$
        - In summary, $W(n) = 2W(\frac{n}{2}) + 2 = \mathcal{O}(n)$
    - The **span** recurrence of `parens_match_dc_helper`:
        - `base cases` cost $1$ since they take constant time 
        - In the `recursive case`...
            - computing the left and right side costs $S(\frac{n}{2})$ since computing `parens_match_dc_helper` on the left and right sides can be done at once on $\frac{n}{2}$ sized inputs
            - combining the left and right side cost $1$ since the comparison, addition, and subtraction can be done in constant time
        - $S(n)...$
            - $= 1 + S(\frac{n}{2}) + 1 $
            - $= S(\frac{n}{2}) + 2$
        - Solving the recurrence $S(n) = S(\frac{n}{2}) + 2$...
            - $C\texttt{(Root)} = 2$
            - $C\texttt{(1st Level)} = S(\frac{n}{4}) + 2 + 2$
            - Cost is neither increasing nor decreasing so this is balanced. Number of levels is $\log n$ and the max cost per level is $2$.
        - In summary, $S(n) = S(\frac{n}{2}) + 2 = \mathcal{O}(\log n)$

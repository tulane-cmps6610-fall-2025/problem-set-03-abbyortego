# CMPS 6610 Problem Set 03
## Answers

**Name:** Abby Ortego


Place all written answers from `problemset-03.md` here for easier grading.


- **1b.**
    - Since `iterate` is called recursively, **Work** can best be expressed as a recurrence.
        - With input size $n$, `iterate` is called recursively on $n-1$ sized inputs 
            - $W(n-1)$ in the recurrence below
        - The inner function of `isearch`, `check`, compares two integers which can be done in constant time.
            - $1$ in the recurrence below
        - Putting these things together, left with the recurrence $W(n) = W(n-1) + 1$
        - Solving the recurrence...
            - $C\texttt{(Root)} = 1$
            - $C\texttt{(1st Level)} = W(n-2) + 1 + 1$
            - Cost is neither increasing nor decreasing so this is balanced. Number of levels is $n$ and the max cost per level is $1$.
        - Therefore, the work of `iterate` is $\mathcal{O}(n)$
    - Similar to above, **Span** can also be expressed as a recurrence. 
        - This approach offers no way to be parallelized so it will produce the same recurrence as above, $W(n) = W(n-1) + 1$
        - Solving the recurrence...
            - $C\texttt{(Root)} = 1$
            - $C\texttt{(1st Level)} = W(n-2) + 1 + 1$
            - Cost is neither increasing nor decreasing so this is balanced. Number of levels is $n$ and the max cost per level is $1$.
        - Therefore, the span of `iterate` is also $\mathcal{O}(n)$


- **1d.**
    - Similar to `iterate`, since `reduce` is called recursively its **work** can best be expressed as a recurrence. 
        - With input size $n$, `reduce` is called recursively twice on $\frac{n}{2}$ sized inputs. 
            - $2W(\frac{n}{2})$ in the recurrence below
        - The inner function of `rsearch`, `check`, compares the two integers to the key which (I think?) can be done in constant time. 
            - $1$ in the recurrence below
        - Putting these things together, left with the recurrence $W(n) = 2W(\frac{n}{2}) + 1$
        - Solving the recurrence...
            - $C\texttt{(Root)} = 1$
            - $C\texttt{(1st Level)} = 2(2W(\frac{n}{4}) + 1) + 1 = 2^2W(\frac{n}{4}) + 2 + 1$
            - Cost is increasing so this is leaf dominated. Number of leaves is $2^{\log_2(n)} = n^{\log_2(2)}$
        - Therefore, the work of `reduce` is $\mathcal{O}(n)$
    - Similar to above, since `reduce` is called recursively its **span** can also best be expressed as a recurrence. 
        - With input size $n$, `reduce` is called recursively twice on $\frac{n}{2}$ sized inputs but since the two recursive calls can be done at the same time only need to account for one.  
            - $S(\frac{n}{2})$ in the recurrence below
        - The inner function of `rsearch`, `check`, compares the two integers to the key which (I think?) can be done in constant time. 
            - $1$ in the recurrence below
        - Putting these things together, left with the recurrence $S(n) = S(\frac{n}{2}) + 1$
        - Solving the recurrence...
            - $C\texttt{(Root)} = 1$
            - $C\texttt{(1st Level)} = S(\frac{n}{4}) + 1 + 1$
            - Cost is neither increasing nor decreasing so this is balanced. Number of levels is $\log_2 n$ and the max cost per level is $1$.
        - Therefore, the span of `reduce` is $\mathcal{O}(\log_2 n)$


- **1e.**
    - Similar to `reduce`, since `ureduce` is called recursively its **work** can best be expressed as a recurrence. 
        - With input size $n$, `ureduce` is called recursively twice on $\frac{n}{3}$ sized inputs. 
            - $2W(\frac{n}{3})$ in the recurrence below
        - The inner function of `rsearch`, `check`, should get called the same with `ureduce` so it will have the same cost as above. 
            - $1$ in the recurrence below
        - Putting these things together, left with the recurrence $W(n) = 2W(\frac{n}{3}) + 1$
        - Solving the recurrence...
            - $C\texttt{(Root)} = 1$
            - $C\texttt{(1st Level)} = 2(2W(\frac{n}{9}) + 1) + 1 = 2^2W(\frac{n}{9}) + 2 + 1$
            - Cost is increasing so this is leaf dominated. Number of leaves is $2^{\log_9(n)} = n^{\log_9(2)}$
        - Therefore, the work of `reduce` is $\mathcal{O}(n^{\log_9(2)})$
    - Similar to above, since `ureduce` is called recursively its **span** can also best be expressed as a recurrence. 
        - With input size $n$, `ureduce` is called recursively twice on $\frac{n}{3}$ sized inputs but since the two recursive calls can be done at the same time only need to account for one.  
            - $S(\frac{n}{3})$ in the recurrence below
        - The inner function of `rsearch`, `check`, should get called the same with `ureduce` so it will have the same cost as above.
            - $1$ in the recurrence below
        - Putting these things together, left with the recurrence $S(n) = S(\frac{n}{3}) + 1$
        - Solving the recurrence...
            - $C\texttt{(Root)} = 1$
            - $C\texttt{(1st Level)} = S(\frac{n}{9}) + 1 + 1$
            - Cost is neither increasing nor decreasing so this is balanced. Number of levels is $\log_3 n$ and the max cost per level is $1$.
        - Therefore, the span of `reduce` is $\mathcal{O}(\log_3 n)$



- **3b.**




- **3d.**





- **3f.**




- **4a.**




- **4b.**





- **4c.**





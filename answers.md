# CMPS 6610 Problem Set 03
## Answers

**Name:** Abby Ortego


Place all written answers from `problemset-03.md` here for easier grading.


- **1b.**
    - Since `iterate` is called recursively, **Work** can best be expressed as a recurrence.
        - With input size $n$, `iterate` is called recursively on $n-1$ sized inputs 
            - $W(n-1)$ in the recurrence below
        - The inner function of `isearch`, `check`, compares two integers which can be done in constant time.
            - $c$ in the recurrence below
        - Putting these things together, left with the recurrence $W(n) = W(n-1) + c$
        - Solving the recurrence...
            - $C\texttt{(Root)} = c$
            - $C\texttt{(1st Level)} = W(n-2) + c + c$
            - Cost is neither increasing nor decreasing so this is balanced. Number of levels is $n$ and the max cost per level is $c$.
        - Therefore, the work of `iterate` is $\mathcal{O}(n)$
    - Similar to above, **Span** can also be expressed as a recurrence. 
        - This approach offers no way to be parallelized so it will produce the same recurrence as above, $W(n) = W(n-1) + c$
        - Solving the recurrence...
            - $C\texttt{(Root)} = c$
            - $C\texttt{(1st Level)} = W(n-2) + c + c$
            - Cost is neither increasing nor decreasing so this is balanced. Number of levels is $n$ and the max cost per level is $c$.
        - Therefore, the span of `iterate` is also $\mathcal{O}(n)$


- **1d.**





- **1e.**





- **3b.**




- **3d.**





- **3f.**




- **4a.**




- **4b.**





- **4c.**





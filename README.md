# dihedralcheck
Implementation of checksum algorithms based on the dihedral group for the serial numbers of the Deutsche Mark (DM).

## How it works

Lets check if the serial number `DS5885114Y8` is valid:

1. Substitute all letters with numbers using following table:
    
    | A | D | G | K | L | N | S | U | Y | Z |
    |---|---|---|---|---|---|---|---|---|---|
    | 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 |

    Now we receive `16588511488`.

2. Now permute all digit using following permutation (given as table). Row corresponds to index of the digit and columns to digit itself. 

    These permutations can be generated by $p = (1 ~ 5 ~ 7 ~ 6 ~ 2 ~ 8 ~ 3 ~ 0 ~ 9 ~ 4)$.
    
    Having $p_i = p^i$ with exception of $p_{11} = \text{id}$.
    
    |     | 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 |
    |-----|---|---|---|---|---|---|---|---|---|---|
    | p1  | 1 | 5 | 7 | 6 | 2 | 8 | 3 | 0 | 9 | 4 |
    | p2  | 5 | 8 | 0 | 3 | 7 | 9 | 6 | 1 | 4 | 2 |
    | p3  | 8 | 9 | 1 | 6 | 0 | 4 | 3 | 5 | 2 | 7 |
    | p4  | 9 | 4 | 5 | 3 | 1 | 2 | 6 | 8 | 7 | 0 |
    | p5  | 4 | 2 | 8 | 6 | 5 | 7 | 3 | 9 | 0 | 1 |
    | p6  | 2 | 7 | 9 | 3 | 8 | 0 | 5 | 4 | 1 | 5 |
    | p7  | 7 | 0 | 4 | 6 | 9 | 1 | 3 | 2 | 5 | 8 |
    | p8  | 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 |
    | p9  | 1 | 5 | 7 | 6 | 2 | 8 | 3 | 0 | 9 | 4 |
    | p10 | 5 | 8 | 0 | 3 | 7 | 9 | 6 | 1 | 4 | 2 |
    | p11 | 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 |
   
    Now we receive `56470001248`

3. Let's simplify this expression by treating all of its digits as group elements of the dihedral group $D_5$. Here we got the Cayley Table of $D_5$.

    |       | 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 |
    |-------|---|---|---|---|---|---|---|---|---|---|
    | **0** | 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 |
    | **1** | 1 | 2 | 3 | 4 | 0 | 6 | 7 | 8 | 9 | 5 |
    | **2** | 2 | 3 | 4 | 0 | 1 | 7 | 8 | 9 | 5 | 6 |
    | **3** | 3 | 4 | 0 | 1 | 2 | 8 | 9 | 5 | 6 | 7 |
    | **4** | 4 | 0 | 1 | 2 | 3 | 9 | 5 | 6 | 7 | 8 |
    | **5** | 5 | 9 | 8 | 7 | 6 | 0 | 4 | 3 | 2 | 1 |
    | **6** | 6 | 5 | 9 | 8 | 7 | 1 | 0 | 4 | 3 | 2 |
    | **7** | 7 | 6 | 5 | 9 | 8 | 2 | 1 | 0 | 4 | 3 |
    | **8** | 8 | 7 | 6 | 5 | 9 | 3 | 2 | 1 | 0 | 4 |
    | **9** | 9 | 8 | 7 | 6 | 5 | 4 | 3 | 2 | 1 | 0 |

    We can evaluate the digits as following using the law of associativity:

    $(5 6)(4 7)(0 0)(0 1)(2 4)8 = (46)(01)(18) = (51)9 = (99) = 0$

4. If the result of your evaluation is the neutral element 0 the serial number is valid, else invalid. So our example is a valid serial number.

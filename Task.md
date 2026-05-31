# Task 1
Provide reachability conditions, infection conditions, propagation conditions, and test case values to kill mutants 2, 4, 5, and 6 in Figure 5.1.

**Original Method**

```cpp
int Min (int A, int B){
    int minVal;
    minVal = A;
    if (B < A)
    {
        minVal = B;
    }
    return (minVal);
} // end Min
```

**With Embedded Mutants**

```cpp
int Min (int A, int B)
{
    int minVal; 
    minVal = A;
Δ1  minVal = B;
    if (B < A)
Δ2  if (B  > A)
Δ3  if (B < minVal)
    {
        minVal = B;
        Δ4  Bomb();
        Δ5  minVal = A;
        Δ6  minVal = failOnZero (B);
    }
    return (minVal);    
} // end Min
```

# Task 2
Answer questions (a) through (d) for the mutant in the method findVal().

(a) If possible, find a test input that does not reach the mutant.

(b) If possible, find a test input that satisfies reachability but not infection for the mutant.

(c) If possible, find a test input that satisfies infection, but not propagation for the mutant.

(d) If possible, find a test input that kills mutant m.

```
// Effects:If numbers null throw NullPointerException
//    else return LAST occurrence of val in numbers[]
//    If val not in numbers[] return -1
public static int findVal(int numbers[], int val) {
    int findVal = -1;

    for (int i = 0; i < numbers.length; i++)
        // for (int i=(0+1); i<numbers.length; i++)
        if (numbers[i] == val)
            findVal = i;
    return (findVal);
}
```
# Learning Algorithms

## The Role Of Algorithms In Computing

An `algorithm` is any well-deûned computational procedure that takes some value, or set of values, as input and produces some value, or set of values, as output in a ûnite amount of time.

An input is called as `instance` of problem.

An algorithm for a computational problem is `correct` if, for every problem instance provided as input, it halts finishes its computing in finite time and outputs the `correct` solution to the problem instance. A `correct` algorithm solves the given computational problem. An `incorrect` algorithm might not halt at all on some input instances, or it might halt with an incorrect answer.

## Sorting Algorithms

### Insertion Sort

The numbers to be sorted are also known as the `keys`, the data associated with these keys is called as `satellite data`, these together form a `record`.

`Input` : A sequence of n numbers (a1, a2, ..., an).
`Output` : A permutation (reordering) (a1, a2, ..., an) of the input sequence such that a1 <= a2 <= ... <= an.

```pseudo-code
INSERTION-SORT(A, n)

1. for i = 2 to n
2.  key = A[i]
3.  // insert A[i] into the sorted sub array A[1: i - 1].
4.  j = i - 1
5.  while j >= 0 and A[j] > key
6.    A[j + 1] = A[j]
7.    j = j - 1
8.  A[j + 1] = key
```

`Loop invariants` helps us understand why an algorithm is correct, it requires this three things

- `Initialization`, Prior to first iteration
- `Maintenance`, If it is true prior to the first iteration, then it remains true before the next iteration
- `Termination`, The loop terminates, and when it terminates, the invariant usually along with the reason that the loop terminated gives us a useful property that helps show that the algorithm is correct.

## Characterizing running times

`Asymptotic` efficiency, here we study how the running time of an algorithm
increases with the size of the input in the limit, as the size of the input
increases without bound.

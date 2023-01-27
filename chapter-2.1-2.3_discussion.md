## Discussion Notes
- Compound data. What is it?
- Data abstraction
	- How is it different from compound data?  Data abstraction is a methodology that enables us to isolate how a compound data object is used from the details of how it is constructed from more primitive data objects.
- How are selectors and constructors important to the idea of data abstraction?
	- _selectors_ and _constructors_  implement the abstract data in terms of the concrete representation
- What is a pair?
	- A compound data object that contains two arguments as parts
- What are the selectors and constructors for a pair?
	
```
(define x (cons 1 2))

(car x)
1

(cdr x)
2
```

- Abstraction barriers 
	- Describe the concept
	- How is this idea useful?
	- Explain how these abstraction barriers from the book are determined, or describe abstraction barriers in an area of code you're working on 
<img width="698" alt="Screen Shot 2023-01-26 at 20 42 58" src="https://user-images.githubusercontent.com/28715808/215192851-373a6832-ff34-4f1f-8d72-baffc82a5995.png">

- GOTCHA: Section 2.13 What is meant by data?
	- In general, we can think of data as defined by some collection of selectors and constructors, together with specified conditions that these procedures must fulfill in order to be a valid representation
	- The procedural representation, although obscure, is a perfectly adequate way to represent pairs, since it fulfills the only conditions that pairs need to fulfill. This may seem a curiosity now, but procedural representations of data will play a central role in our programming repertoire. This style of programming is often called _message passing_, and we will be using it as a basic tool in [Chapter 3](https://sarabander.github.io/sicp/html/Chapter-3.xhtml#Chapter-3) when we address the issues of modeling and simulation.
- Hierarchical Data Structures 
	- What are they used for?
		- Hierarchies 
		- Binary trees & Binary search trees 
		- Parse tree (mathematical operations)
	- Helpful for sequences whose elements are themselves sequences
	- What is the closure property?
		- In general, an operation for combining data objects satisfies the closure property if the results of combining things with that operation can themselves be combined using the same operation
		- eg. The ability to create pairs whose elements are pairs
	
	- Describe the box-and-pointer notation used in the book for representing sequences
	<img width="757" alt="Screen Shot 2023-01-26 at 20 34 21" src="https://user-images.githubusercontent.com/28715808/215193027-397f0aee-b266-4738-89eb-a47ad149241c.png">

	
- What is a list? A sequence of pairs 
<img width="767" alt="Screen Shot 2023-01-26 at 20 52 10" src="https://user-images.githubusercontent.com/28715808/215192918-65b5970f-4ce8-4fa8-a115-17e189286a01.png">

- What is meant by a list operation successively "`cdr-ing` down" a list? When would this be useful?
```
(define (list-ref items n)
  (if (= n 0)
      (car items)
      (list-ref (cdr items) 
                (- n 1))))

(define squares 
  (list 1 4 9 16 25))

(list-ref squares 3)
16
```
- What is meant by a list operation “`cons`-ing up” an answer list while `cdr`ing down a list? When would this be useful?
```
(append squares odds)
(1 4 9 16 25 1 3 5 7)

(append odds squares)
(1 3 5 7 1 4 9 16 25)
```
- What is different from operating on a tree versus a list?
	- in the reduction step, where we strip off the `car` of the list, we must take into account that the `car` may itself be a tree whose leaves we need to count.
	- The base case often checks `pair?` versus `nil`
- How does the following diagram represent conventional interfaces?
<img width="735" alt="Screen Shot 2023-01-26 at 21 00 45" src="https://user-images.githubusercontent.com/28715808/215193074-2c20c5e3-f93a-4fcd-8395-9c09e0dca21f.png">

- What is meant by signal-flow structure? Concentrate on the “signals” that flow from one stage in the process to the next.
- Are there any examples or concepts that stood out to you as particularly important or interesting in this section?

## Exercises
- [X] Warm up: 2.17
- [X] 2.22
- 2.26
- 2.30 or 2.54

**Exercise 2.7:** Alyssa’s program is incomplete because she has not specified the implementation of the interval abstraction. Here is a definition of the interval constructor:

(define (make-interval a b) (cons a b))

Define selectors `upper-bound` and `lower-bound` to complete the implementation.

**Exercise 2.8:** Using reasoning analogous to Alyssa’s, describe how the difference of two intervals may be computed. Define a corresponding subtraction procedure, called `sub-interval.

**Exercise 2.10:** Ben Bitdiddle, an expert systems programmer, looks over Alyssa’s shoulder and comments that it is not clear what it means to divide by an interval that spans zero. Modify Alyssa’s code to check for this condition and to signal an error if it occurs.

**Exercise 2.12:** Define a constructor `make-center-percent` that takes a center and a percentage tolerance and produces the desired interval. You must also define a selector `percent` that produces the percentage tolerance for a given interval. The `center` selector is the same as the one shown above.

**Exercise 2.17:** Define a procedure `last-pair` that returns the list that contains only the last element of a given (nonempty) list:
```
(last-pair (list 23 72 149 34))
(34)

(last-pair (items) 
	(if ((cdr items) == nil)
		(cons (car items)))
	(last-pair (cdr (items)))
)
```


**Exercise 2.20:** The procedures `+`, `*`, and `list` take arbitrary numbers of arguments. One way to define such procedures is to use `define` with _dotted-tail notation_. In a procedure definition, a parameter list that has a dot before the last parameter name indicates that, when the procedure is called, the initial parameters (if any) will have as values the initial arguments, as usual, but the final parameter’s value will be a _list_ of any remaining arguments. For instance, given the definition
```
(define (f x y . z) ⟨body⟩)
```
the procedure `f` can be called with two or more arguments. If we evaluate
```
(f 1 2 3 4 5 6)
```
then in the body of `f`, `x` will be 1, `y` will be 2, and `z` will be the list `(3 4 5 6)`. Given the definition
```
(define (g . w) ⟨body⟩)
```
the procedure `g` can be called with zero or more arguments. If we evaluate
```
(g 1 2 3 4 5 6)
```
then in the body of `g`, `w` will be the list `(1 2 3 4 5 6)`. Use this notation to write a procedure `same-parity` that takes one or more integers and returns a list of all the arguments that have the same even-odd parity as the first argument. For example,

```
(same-parity 1 2 3 4 5 6 7)
(1 3 5 7)

(same-parity 2 3 4 5 6 7)
(2 4 6)
```


**Exercise 2.22:** Louis Reasoner tries to rewrite the first `square-list` procedure of [Exercise 2.21](https://sarabander.github.io/sicp/html/2_002e2.xhtml#Exercise-2_002e21) so that it evolves an iterative process:

```
(square-list (list 1 2 3 4))
(1 4 9 16)

(define (square-list items)
  (define (iter things answer)
    (if (null? things)
        answer
        (iter (cdr things)
              (cons (square (car things))
                    answer))))
  (iter items nil))

>> (square-list (1 2 3 4))
>> (iter (1 2 3 4) nil)
>> (iter (2 3 4) (1 nil))
>> (iter (3 4) (4 1 nil))
>> (iter (4) (9 4 1 nil))
>> (iter () (16 9 4 1 nil))
>> (16 9 4 1 nil)
```

Unfortunately, defining `square-list` this way produces the answer list in the reverse order of the one desired. Why?

Louis then tries to fix his bug by interchanging the arguments to `cons`:
```
(define (square-list items)
  (define (iter things answer)
    (if (null? things)
        answer
        (iter (cdr things)
              (cons answer
                    (square 
                     (car things))))))
  (iter items nil))
>> (square-list (1 2 3 4))
>> (iter (1 2 3 4) nil)
>> (iter (2 3 4) (nil 1))
>> (iter (3 4) (nil 1 4)
>> (iter (4) ((nil 1) (4) (9))
>> (iter () ((nil 1 (4 (9) (16)))))

(cons 1 (2 3))
(1 (2 3))
(cons (1 (2 3) (4 5)))
(1 (2 3 (4 5)))
```

This doesn’t work either. Explain.

Reference first `square-list` procedures (recursive):
```
(define (square-list items)
  (if (null? items)
      nil
      (cons (* (car items) (car items)) (square-list (cdr items)))))

(define (square-list items)
  (map (lambda (x) (* x x)) items ))
```

**Exercise 2.23:** The procedure `for-each` is similar to `map`. It takes as arguments a procedure and a list of elements. However, rather than forming a list of the results, `for-each` just applies the procedure to each of the elements in turn, from left to right. The values returned by applying the procedure to the elements are not used at all—`for-each` is used with procedures that perform an action, such as printing. For example,
```
(for-each 
 (lambda (x) (newline) (display x))
 (list 57 321 88))

>> 57
>> 321
>> 88
```

The value returned by the call to `for-each` (not illustrated above) can be something arbitrary, such as true. Give an implementation of `for-each`.


**Exercise 2.24:** Suppose we evaluate the expression `(list 1 (list 2 (list 3 4)))`. Give the result printed by the interpreter, the corresponding box-and-pointer structure, and the interpretation of this as a tree (as in [Figure 2.6](https://sarabander.github.io/sicp/html/2_002e2.xhtml#Figure-2_002e6)).

**Exercise 2.26:** Suppose we define `x` and `y` to be two lists:
```
(define x (list 1 2 3))
(define y (list 4 5 6))
```

What result is printed by the interpreter in response to evaluating each of the following expressions:
```
> (append x y)
> (cons x y)
> (list x y)
```

**Exercise 2.29:** A binary mobile consists of two branches, a left branch and a right branch. Each branch is a rod of a certain length, from which hangs either a weight or another binary mobile. We can represent a binary mobile using compound data by constructing it from two branches (for example, using `list`):
```
(define (make-mobile left right)
  (list left right))
```

A branch is constructed from a `length` (which must be a number) together with a `structure`, which may be either a number (representing a simple weight) or another mobile:

```
(define (make-branch length structure)
  (list length structure))
```

1.  Write the corresponding selectors `left-branch` and `right-branch`, which return the branches of a mobile, and `branch-length` and `branch-structure`, which return the components of a branch.
2.  Using your selectors, define a procedure `total-weight` that returns the total weight of a mobile.
3.  A mobile is said to be _balanced_ if the torque applied by its top-left branch is equal to that applied by its top-right branch (that is, if the length of the left rod multiplied by the weight hanging from that rod is equal to the corresponding product for the right side) and if each of the submobiles hanging off its branches is balanced. Design a predicate that tests whether a binary mobile is balanced.
4.  Suppose we change the representation of mobiles so that the constructors are
```
(define (make-mobile left right)
  (cons left right))

(define (make-branch length structure)
  (cons length structure))
```

How much do you need to change your programs to convert to the new representation?


**Exercise 2.30:** Define a procedure `square-tree` analogous to the `square-list` procedure of [Exercise 2.21](https://sarabander.github.io/sicp/html/2_002e2.xhtml#Exercise-2_002e21). That is, `square-tree` should behave as follows:
```
(square-tree
 (list 1
       (list 2 (list 3 4) 5)
       (list 6 7)))
(1 (4 (9 16) 25) (36 49))
```

Define `square-tree` both directly (i.e., without using any higher-order procedures) and also by using `map` and recursion.

**Exercise 2.31:** Abstract your answer to [Exercise 2.30](https://sarabander.github.io/sicp/html/2_002e2.xhtml#Exercise-2_002e30) to produce a procedure `tree-map` with the property that `square-tree` could be defined as
```
(define (square-tree tree) 
  (tree-map square tree))
```


**Exercise 2.32:** We can represent a set as a list of distinct elements, and we can represent the set of all subsets of the set as a list of lists. For example, if the set is `(1 2 3)`, then the set of all subsets is `(() (3) (2) (2 3) (1) (1 3) (1 2) (1 2 3))`. Complete the following definition of a procedure that generates the set of subsets of a set and give a clear explanation of why it works:

```
(define (subsets s)
  (if (null? s)
      (list nil)
      (let ((rest (subsets (cdr s))))
        (append rest (map ⟨??⟩ rest)))))
```

**Exercise 2.36:** The procedure `accumulate-n` is similar to `accumulate` except that it takes as its third argument a sequence of sequences, which are all assumed to have the same number of elements. It applies the designated accumulation procedure to combine all the first elements of the sequences, all the second elements of the sequences, and so on, and returns a sequence of the results. For instance, if `s` is a sequence containing four sequences, `((1 2 3) (4 5 6) (7 8 9) (10 11 12)),` then the value of `(accumulate-n + 0 s)` should be the sequence `(22 26 30)`. Fill in the missing expressions in the following definition of `accumulate-n`:

```
(define (accumulate-n op init seqs)
  (if (null? (car seqs))
      nil
      (cons (accumulate op init ⟨??⟩)
            (accumulate-n op init ⟨??⟩))))
```


**Exercise 2.38:** The `accumulate` procedure is also known as `fold-right`, because it combines the first element of the sequence with the result of combining all the elements to the right. There is also a `fold-left`, which is similar to `fold-right`, except that it combines elements working in the opposite direction:

```
(define (fold-left op initial sequence)
  (define (iter result rest)
    (if (null? rest)
        result
        (iter (op result (car rest))
              (cdr rest))))
  (iter initial sequence))
```


What are the values of
```
(fold-right / 1 (list 1 2 3))
(fold-left  / 1 (list 1 2 3))
(fold-right list nil (list 1 2 3))
(fold-left  list nil (list 1 2 3))
```

Give a property that `op` should satisfy to guarantee that `fold-right` and `fold-left` will produce the same values for any sequence.

**Exercise 2.54:** Two lists are said to be `equal?` if they contain equal elements arranged in the same order. For example,

```
(equal? '(this is a list) 
        '(this is a list))
```


is true, but
```
(equal? '(this is a list) 
        '(this (is a) list))
```


is false. To be more precise, we can define `equal?` recursively in terms of the basic `eq?` equality of symbols by saying that `a` and `b` are `equal?` if they are both symbols and the symbols are `eq?`, or if they are both lists such that `(car a)` is `equal?` to `(car b)` and `(cdr a)` is `equal?` to `(cdr b)`

Using this idea, implement `equal?` as a procedure.

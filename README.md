[![Review Assignment Due Date](https://classroom.github.com/assets/deadline-readme-button-24ddc0f5d75046c5622901739e7c5dd533143b0c8e959d652212380cedb1ea36.svg)](https://classroom.github.com/a/OlW38W4k)
# Recurrence Analysis -- Mystery Function

Analyze the running time of the following recursive procedure as a function of
$n$ and find a tight big $O$ bound on the runtime for the function. You may
assume that each operation takes unit time. You do not need to provide a formal
proof, but you should show your work: at a minimum, show the recurrence relation
you derive for the runtime of the code, and then how you solved the recurrence
relation.

- Based on my work of last semester

```javascript
function mystery(n) {
    if(n <= 1)
        return; // => 1
    else {
        mystery(n / 3); // => T(n/3)
        var count = 0;  // => 1
        mystery(n / 3); // => T(n/3)
        for(var i = 0; i < n*n; i++) {  // => n*n
            for(var j = 0; j < n; j++) {    // => n
                for(var k = 0; k < n*n; k++) { //=> n*n
                    count = count + 1;  // => 1
                }
            }
        }
        mystery(n / 3); // => T(n/3)
    }
}
```

We can see how long it will take to run mystery n (added comments to the code above about the run time), we add all the times

1 + T(n/3) + 1 + T(n/3) + ($n^2 * n * n^2 * 1$) + T(n/3)

= 3T(n/3) + $n^5$ + 3

with our base case we get that T(n) = 

- T(n) = 1 if n <= 1

- T(n) = $3T(\frac{n}{3})+n^5+3$ if n>1

We can start out recurrence relation:

T(n) = $3T(\frac{n}{3})+n^5+3$ 

- we want to know what T(n/3) is so we put that into our formula
- T(n/3) = $3T(\frac{\frac{n}{3}}{3})+(\frac{n}{3})^5+3$
- T(n/3) = $3T(\frac{n}{9})+(\frac{n^5}{3^5})+3$
- next we substitute it back into the function

T(n) = $3(3T(\frac{n}{9})+(\frac{n^5}{3^5})+3)+n^5+3$ 

T(n) = $9T(\frac{n}{9})+3(\frac{n^5}{3^5})+9+n^5+3$

T(n) = $9T(\frac{n}{9})+(\frac{n^5}{3^4})+9+n^5+3$

- we want to know what T(n/9) is so we put that into our formula
- T(n/3) = $3T(\frac{\frac{n}{9}}{3})+(\frac{n}{9})^5+3$
- T(n/3) = $3T(\frac{n}{27})+(\frac{n^5}{9^5})+3$
- next we substitute it back into the function

T(n) = $9(3T(\frac{n}{27})+(\frac{n^5}{9^5})+3)+(\frac{n^5}{3^4})+9+n^5+3$

T(n) = $27T(\frac{n}{27})+9(\frac{n^5}{9^5})+27+(\frac{n^5}{3^4})+9+n^5+3$

T(n) = $27T(\frac{n}{27})+(\frac{n^5}{9^4})+(\frac{n^5}{3^4})+n^5+3+9+27$

-
-
-

T(k) = $3^kT(\frac{n}{3^k}) + \sum_{i=0}^{k} (\frac{n^5}{3^{4(i-1)}}) + \sum_{i=0}^{k} (3^i)$ 

- T(n) in the kth generation is:

T(n) = $3^kT(\frac{n}{3^k}) + n^5\sum_{i=0}^{k} (\frac{1}{3^{4(i-1)}}) + \sum_{i=0}^{k} (3^i)$ 

- We want to get to the base case of T(1) so we solve for k $\frac{n}{3^k} = 1$

- $\frac{n}{3^k} = 1$
- $log_3n = k$
- we substitute k back in 

T(n) = $3^{log_3n}T(\frac{n}{3^{log_3n}}) + n^5\sum_{i=0}^{log_3n} (\frac{1}{3^{4(i-1)}}) + \sum_{i=0}^{log_3n} (3^i)$ 

T(n) = $nT(1) + n^5\sum_{i=0}^{log_3n} (\frac{1}{3^{4(i-1)}}) + \sum_{i=0}^{log_3n} (3^i)$ 

- simplifying the sums with time complexity in mind, discarding constants

T(n) = $n(1) + n^5$

- we take the bigger term of $n^5$

so $T(n) \in O(n^5)$

Add your answer to this markdown file. [This
page](https://docs.github.com/en/get-started/writing-on-github/working-with-advanced-formatting/writing-mathematical-expressions)
might help with the notation for mathematical expressions.

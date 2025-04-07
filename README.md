# Recurrence Analysis -- Mystery Function

Analyze the running time of the following recursive procedure as a function of
$n$ and find a tight big $O$ bound on the runtime for the function. You may
assume that each operation takes unit time. You do not need to provide a formal
proof, but you should show your work: at a minimum, show the recurrence relation
you derive for the runtime of the code, and then how you solved the recurrence
relation.

```javascript
function mystery(n) {
    if(n <= 1)
        return;
    else {
        mystery(n / 3);
        var count = 0;
        mystery(n / 3);
        for(var i = 0; i < n*n; i++) {
            for(var j = 0; j < n; j++) {
                for(var k = 0; k < n*n; k++) {
                    count = count + 1;
                }
            }
        }
        mystery(n / 3);
    }
}
```

Add your answer to this markdown file. [This
page](https://docs.github.com/en/get-started/writing-on-github/working-with-advanced-formatting/writing-mathematical-expressions)
might help with the notation for mathematical expressions.


//


Name: Kane Kriz

Start Date: 11 Feb 2025

Last Edited: 7 April 2025

Feedback Request 1 Date: 7 April 2025


//


Response: Formatting WIP, issues still exist

First, I wanted to make a write down of my step by step interpretation of the code and how it processes through the mystery function: The first considered condition is if the value of n is less than or equal to 1, the function returns.

If that condition is not met, the else{ statement making up the bulk of the function is called. This else contains three recursive calls to mystery(n / 3) and a nested loop structure. 

To derive the overall complexity of the function as requested, we need to consider the behavior of the nested loops as well as how the deepest layer of the nested loops behaves.
Based off of that, we can grow our understanding of the behavior of the function from the deepest layer outward, eventually leading to a solution to the overall complexity of the function as requested.

The runtime of the mystery recursive code overall can be derived as follows:

I noted that the base case, where n ≤ 1, takes constant time, Θ(1).

I then considered the recursive case. In the recursive case, the function makes three calls to mystery(n / 3) and executes a nested loop that runs n^2 × n × n^2 = n^5 times.

Each operation inside the innermost loop takes unit time, resulting in a total time complexity of Θ(n^5) for the loops.



 
To find the overall running time of the whole function, we can express the recurrence relation as:
 
$T(n) = 3T\left(\frac{n}{3}\right) + \Theta(n^5)$
 
This above recurrence relation is derived from the fact that the function makes three recursive calls to mystery(n / 3), each contributing T(n / 3) towards computing the total running time, 
and the nested loops contribute Θ(n^5) to the overall running time of the function.
 

Following what was covered in the videos and class slides, I have elected to use the substitution method, similarly to what was done to solve the mergeSort runtime in provided examples.
I begun by expanding the recurrence relation step by step. Initially, the relation begins as:
 
$T(n) = 3T\left(\frac{n}{3}\right) + n^5$


 
Substituting T(n / 3) into the equation, it results in:
 
$T(n) = 3 \left[ 3T\left(\frac{n}{9}\right) + \left(\frac{n}{3}\right)^5 \right] + n^5$

$T(n) = 3^2 T\left(\frac{n}{9}\right) + 3 * \frac{n^5}{3^5} + n^5$

$T(n) = 9T\left(\frac{n}{9}\right) + \frac{n^5}{9} + n^5$


 

Continuing this process, we substitute T(n / 9) into the equation to further expand the relation:

$T(n) = 9 \left[ 3T\left(\frac{n}{27}\right) + \left(\frac{n}{9}\right)^5 \right] + \frac{n^5}{9} + n^5$

$T(n) = 3^3 T\left(\frac{n}{27}\right) + 9 * \frac{n^5}{9^5} + \frac{n^5}{9} + n^5$

$T(n) = 27T\left(\frac{n}{27}\right) + \frac{n^5}{3^5} + \frac{n^5}{9} + n^5$
 



Following this pattern, we then can begin to draw conclusions regarding the behavior of the function after an arbitrary number of substitutions.
 
After i substitutions, the general form of the recurrence relation becomes:
 
$T(n) = 3^i T\left(\frac{n}{3^i}\right) + \sum_{k=0}^{i-1} 3^k \left(\frac{n}{3^k}\right)^5$
 
To simplify the sum, we let i = log_3 n, so $\(\frac{n}{3^i} = 1\)$.
 


 

The choice of log_3 is based on the fact that the problem size is reduced by a factor of 3 in each recursive call.
This means that after i recursive calls, the problem size becomes n / 3^i. 

In order to reach the base case where the problem size is 1, we need to solve for i such that n / 3^i = 1. 
This gives us i = log_3 n, which is the number of times the function needs to recursively call itself to reduce the problem size to 1.

$T(n) = n T(1) + n^5 * \frac{1 - (1/81)^{\log_3 n}}{1 - 1/81}$
 
The sum $\sum_{k=0}^{\log_3 n - 1} \frac{1}{3^{4k}}$ is a geometric series with ratio $r = \frac{1}{81}$. 

Its closed form is:
$\sum_{k=0}^{i-1} \frac{1}{3^{4k}} = \frac{1 - (1/81)^{\log_3 n}}{1 - 1/81}$

For large n, $(1/81)^{\log_3 n} \approx 0$, so the sum approaches $\frac{81}{80}$, a constant.
 
This is due to in geometric series with a common ratio less than 1, the sum of the series converges to a finite value.

Therefore, the sum $\(\sum_{k=0}^{\log_3 n - 1} \frac{1}{3^{4k}}\)$ converges to a constant value, which simplifies the final form of the recurrence relation:
 
$T(n) = n T(1) + n^5 * \frac{81}{80}$

Since $\frac{81}{80}$ is a constant and $n^5$ dominates $n$ asymptotically:

$T(n) \in n * \Theta(1) + n^5 * \Theta(1) = \Theta(n^5)$

(as the n^5 term dominates the constant and linear terms asymptocially)

As a result of this, the tight asymptotic bound on the runtime for the provided mystery function is T(n) ∈ Θ(n^5)

Logically, this makes sense given the functionality and behavior of the function.

The function's primary computational effort is concentrated in the nested loops, which dominate the overall time complexity.
The recursive calls reduce the problem size by a factor of 3 each time, but the nested loops' complexity, Θ(n^5), grows significantly faster than the reduction achieved by the recursive calls.

Therefore, the Θ(n^5) term dominates the overall time complexity, confirming that the function's running time increases rapidly with larger values of n, as analysed above.
 

//


Plagiarism Acknowledgement: I certify that I have listed all sources used to complete this exercise, including the use of any Large Language Models. All of the work is my own, except where stated otherwise. I am aware that plagiarism carries severe penalties and that if plagiarism is suspected, charges may be filed against me without prior notice.


Citations:

In-Class Slides, Material

“LaTeX Cheat Sheet & Quick Reference.” QuickRef.ME,[https://quickref.me/latex](url).

“Substitution Method to Solve Recurrence Relations.” GeeksforGeeks, 18 Mar. 2024, [www.geeksforgeeks.org/substitution-method-to-solve-recurrence-relations/](url).

Su, Jessica. CS 161 Lecture 3. [https://web.stanford.edu/class/archive/cs/cs161/cs161.1168/lecture3.pdf](url)


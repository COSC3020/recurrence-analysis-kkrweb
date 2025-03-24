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
Last Edited: 24 March 2025
Feedback Request 1 Date: X


//


Response: Incomplete


//


Plagiarism Acknowledgement: I certify that I have listed all sources used to complete this exercise, including the use of any Large Language Models. All of the work is my own, except where stated otherwise. I am aware that plagiarism carries severe penalties and that if plagiarism is suspected, charges may be filed against me without prior notice.

Citations:
“LaTeX Cheat Sheet & Quick Reference.” QuickRef.ME,[https://quickref.me/latex](url).
“Substitution Method to Solve Recurrence Relations.” GeeksforGeeks, 18 Mar. 2024, [www.geeksforgeeks.org/substitution-method-to-solve-recurrence-relations/](url).
Su, Jessica. CS 161 Lecture 3. [https://web.stanford.edu/class/archive/cs/cs161/cs161.1168/lecture3.pdf](url)


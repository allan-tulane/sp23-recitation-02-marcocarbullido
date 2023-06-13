# CMPS 2200  Recitation 02

**Name (Team Member 1): Marco Carbullido**

In this recitation, we will investigate recurrences. 
To complete this recitation, follow the instructions in this document. Some of your answers will go in this file, and others will require you to edit `main.py`.


## Setup
- Make sure you have a Github account.
- Login to Github.
- Login to repl.it, using "sign in with github"
- Click on the assignment link sent through canvas and accept the assignment.
- Click on your personal github repository for the assignment.
- Click on the "Work in Repl.it" button. This will launch an instance of `repl.it` initialized with the code from your repository.
- You'll work with a partner to complete this recitation. To do so, we'll break you into Zoom rooms. You will be able to code together in the same `repl.it` instance. You can choose whose repl.it instance you will share. This person will click the "Share" button in their repl.it instance and email the lab partner.

## Running and testing your code
- In the command-line window, run `./ipy` to launch an interactive IPython shell. This is an interactive shell to help run and debug your code. Any code you change in `main.py` will be reflected from this shell. So, you can modify a function in `main.py`, then test it here.
  + If it seems things don't refresh, try running `from main import *`
- You can exit the IPython prompt by either typing `exit` or pressing `ctrl-d`
- To run tests, from the command-line shell, you can run
  + `pytest main.py` will run all tests
  + `pytest main.py::test_one` will just run `test_one`
  + We recommend running one test at a time as you are debugging.

## Turning in your work

- Once complete, click on the "Version Control" icon in the left pane on repl.it.
- Enter a commit message in the "what did you change?" text box
- Click "commit and push." This will push your code to your github repository.
- Although you are working as a team, please have each team member submit the same code to their repository. One person can copy the code to their repl.it and submit it from there.

## Recurrences

In class, we've started looking at recurrences and how to we can establish asymptotic bounds on their values as a function of $n$. In this lab, we'll write some code to generate recursion trees (via a recursive function) for certain kinds of recurrences. By summing up nodes in the recurrence tree (that represent contributions to the recurrence) we can compare their total cost against the corresponding asymptotic bounds. We'll focus on  recurrences of the form:

$$ W(n) = aW(n/b) + f(n) $$

where $W(1) = 1$.

- [ ] 1. (2 point) In `main.py`, you have stub code which includes a function `simple_work_calc`. Implement this function to return the value of $W(n)$ for arbitrary values of $a$ and $b$ with $f(n)=n$.

- [ ] 2. (2 point) Test that your function is correct by calling from the command-line `pytest main.py::test_simple_work` by completing the test cases and adding 3 additional ones.

- [ ] 3. (2 point) Now implement `work_calc`, which generalizes the above so that we can now input $a$, $b$ and a *function* $f(n)$ as arguments. Test this code by completing the test cases in `test_work` and adding 3 more cases.

- [ ] 4. (2 point) Now, derive the asymptotic behavior of $W(n)$ using $f(n) = 1$, $f(n) = \log n$ and $f(n) = n$. Then, generate actual values for $W(n)$ for your code and confirm that the trends match your derivations.

**1. $f(n) = 1$: $W(n) = \Theta(n^{\log_b{a}})$.**
**2. $f(n) = \log n$: $W(n) = \Theta(n^c \log n) = \Theta(\log^2 n)$.**
**3. $f(n) = n$:  $W(n) = \Theta(n)$.**
**f(n) = 1: [1, 3, 3, 7, 7, 7, 7, 15, 15, 15, 15, 15, 15, 15, 15, 31, 31, 31, 31, 31]**
**f(n) = log(n): [1, 3.0, 3.584962500721156, 8.0, 8.321928094887362, 9.754887502163468, 9.977279923499916, 19.0, 19.169925001442312, 19.965784284662085, 20.10328780841202, 23.094737505048094, 23.210214722468027, 23.761914769057434, 23.86145044260835, 42.0, 42.08746284125034, 42.50977500432694, 42.58777751632821, 44.25349666421153]**
**f(n) = n: [1, 4, 5, 12, 13, 16, 17, 32, 33, 36, 37, 44, 45, 48, 49, 80, 81, 84, 85, 92]**

- [ ] 5. (4 points) Now that you have a nice way to empirically generate valuess of $W(n)$, we can look at the relationship between $a$, $b$, and $f(n)$. Suppose that $f(n) = n^c$. What is the asypmptotic behavior of $W(n)$ if $c < \log_b a$? What about $c > \log_b a$? And if they are equal? Modify `compare_work` to compare empirical values for different work functions (at several different values of $n$) to justify your answer. 

**If the condition c<log_b(a) holds, the asymptotic behavior of the function n^c remains infinite, albeit with a comparatively slower growth rate than when c>log_b(a). In essence, as n approaches infinity, the limit of the function tends towards 0. Conversely, when c>log_b(a), the limit approaches infinity and the function can be classified as O(nlog(n)). In the case where c equals log_b(a), the behavior represents a pure logarithmic equation that grows towards infinity, albeit at a slower pace than c>log_b(a). Consequently, the function falls under the category of O(log(n)), with the limit tending towards infinity.**

- [ ] 6. (3 points) $W(n)$ is meant to represent the running time of some recursive algorithm. Suppose we always had $a$ processors available to us and we wanted to compute the span of the same algorithm. Implement the function `span_calc` to compute the empirical span, where the work of the algorithm is given by $W(n)$. Implement `test_compare_span` to create a new comparison function for comparing span functions. Derive the asymptotic expressions for the span of the recurrences you used in problem 4 above. Confirm that everything matches up as it should. 

**f(n) = 1: leaf dominated: O(n)**
**f(n) = log n: balanced tree: O(nlogn)**
**f(n) = n: root dominated: O(n^2)**

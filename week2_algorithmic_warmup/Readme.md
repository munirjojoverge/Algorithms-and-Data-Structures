Programming Assignment 2:
Algorithmic Warm-up
Revision: January 11, 2018
Introduction
Welcome to your second programming assignment of the Algorithmic Toolbox at Coursera! It consists of seven
programming challenges. The first three challenges require you just to implement carefully the algorithms
covered in the lectures. The remaining four challenges will require you to first design an algorithm and
then to implement it. For all the challenges, we provide starter solutions in C++, Java, and Python3. These
solutions implement straightforward algorithms that usually work only for small inputs. To verify this, you
may want to submit these solutions to the grader. This will usually give you a “time limit exceeded”
message for Python starter files and either “time limit exceeded” or “wrong answer” message for C++
and Java solutions (the reason for wrong answer being an integer overflow issue). Your goal is to replace
a naive algorithm with an efficient one. In particular, you may want to use the naive implementation for
stress testing your efficient implementation.
In this programming assignment, the grader will show you the input data if your solution fails on any
of the tests. This is done to help you to get used to the algorithmic problems in general and get some
experience debugging your programs while knowing exactly on which tests they fail. However, for all the
following programming assignments, the grader will show the input data only in case your solution fails on
one of the first few tests.
Learning Outcomes
Upon completing this programming assignment you will be able to:
1. See the huge difference between a slow algorithm and a fast one.
2. Play with examples where knowing something interesting about a problem helps to design an algorithm
that is much faster than a naive one.
3. Implement solutions that work much more faster than straightforward solutions for the following programming
challenges:
(a) compute a small Fibonacci number;
(b) compute the last digit of a large Fibonacci number;
(c) compute a huge Fibonacci number modulo 𝑚;
(d) compute the last digit of a sum of Fibonacci numbers;
(e) compute the last digit of a partial sum of Fibonacci numbers;
(f) compute the greatest common divisor of two integers;
(g) compute the least common multiple of two integers.
4. Implement the algorithms covered in the lectures, design new algorithms.
5. Practice implementing, testing, and debugging your solution. In particular, you will find out how in
practice, when you implement an algorithm, you bump into unexpected questions and problems not
covered by the general description of the algorithm. You will also check your understanding of the
algorithm itself and most probably see that there are some aspects you did not think of before you
had to actually implement it. You will overcome all those complexities, implement the algorithms, test
them, debug, and submit to the system.
1
Passing Criteria: 4 out of 7
Passing this programming assignment requires passing at least 4 out of 7 programming challenges from this
assignment. In turn, passing a programming challenge requires implementing a solution that passes all the
tests for this problem in the grader and does so under the time and memory limits specified in the problem
statement.
Contents
1 Fibonacci Number 3
2 Last Digit of a Large Fibonacci Number 4
3 Greatest Common Divisor 6
4 Least Common Multiple 7
5 Fibonacci Number Again 8
6 Last Digit of the Sum of Fibonacci Numbers 9
7 Last Digit of the Sum of Fibonacci Numbers Again 10
2
1 Fibonacci Number
Problem Introduction
Recall the definition of Fibonacci sequence: 𝐹0 = 0, 𝐹1 = 1, and 𝐹𝑖 = 𝐹𝑖−1 +𝐹𝑖−2 for
𝑖 ≥ 2. Your goal in this problem is to implement an efficient algorithm for computing
Fibonacci numbers. The starter files for this problem contain an implementation of
the following naive recursive algorithm for computing Fibonacci numbers in C++,
Java, and Python3:
Fibonacci(𝑛):
if 𝑛 ≤ 1:
return 𝑛
return Fibonacci(𝑛 − 1) + Fibonacci(𝑛 − 2)
Try compiling and running a starter solution on your machine. You will see that
computing, say, 𝐹40 already takes noticeable time.
Another way to appreciate the dramatic difference between an exponential time algorithm
and a polynomial time algorithm is to use the following visualization by David
Galles: http://www.cs.usfca.edu/~galles/visualization/DPFib.html. Try computing
𝐹20 by a recursive algorithm by entering “20” and pressing the “Fibonacci Recursive”
button. You will see an endless number of recursive calls. Now, press “Skip
Forward” to stop the current algorithm and call the iterative algorithm by pressing
“Fibonacci Table”. This will compute 𝐹20 very quickly. (Note that the visualization
uses a slightly different definition of Fibonacci numbers: 𝐹0 = 1 instead of 𝐹0 = 0.
This of course has almost no influence on the running time.)
Problem Description
Task. Given an integer 𝑛, find the 𝑛th Fibonacci number 𝐹𝑛.
Input Format. The input consists of a single integer 𝑛.
Constraints. 0 ≤ 𝑛 ≤ 45.
Output Format. Output 𝐹𝑛.
Sample 1.
Input:
10
Output:
55
𝐹10 = 55.
Need Help?
Ask a question or see the questions asked by other learners at this forum thread.
3
2 Last Digit of a Large Fibonacci Number
Problem Introduction
Your goal in this problem is to find the last digit of 𝑛-th Fibonacci number. Recall that Fibonacci numbers
grow exponentially fast. For example,
𝐹200 = 280 571 172 992 510 140 037 611 932 413 038 677 189 525 .
Therefore, a solution like
𝐹[0] ← 0
𝐹[1] ← 1
for 𝑖 from 2 to 𝑛:
𝐹[𝑖] ← 𝐹[𝑖 − 1] + 𝐹[𝑖 − 2]
print(𝐹[𝑛] mod 10)
will turn out to be too slow, because as 𝑖 grows the 𝑖th iteration of the loop computes the sum of longer
and longer numbers. Also, for example, 𝐹1000 does not fit into the standard C++ int type. To overcome
this difficulty, you may want to store in 𝐹[𝑖] not the 𝑖th Fibonacci number itself, but just its last digit (that
is, 𝐹𝑖 mod 10). Computing the last digit of 𝐹𝑖 is easy: it is just the last digit of the sum of the last digits of
𝐹𝑖−1 and 𝐹𝑖−2:
𝐹[𝑖] ← (𝐹[𝑖 − 1] + 𝐹[𝑖 − 2]) mod 10
This way, all 𝐹[𝑖]’s are just digits, so they fit perfectly into any standard integer type, and computing a sum
of 𝐹[𝑖 − 1] and 𝐹[𝑖 − 2] is performed very quickly.
Problem Description
Task. Given an integer 𝑛, find the last digit of the 𝑛th Fibonacci number 𝐹𝑛 (that is, 𝐹𝑛 mod 10).
Input Format. The input consists of a single integer 𝑛.
Constraints. 0 ≤ 𝑛 ≤ 107.
Output Format. Output the last digit of 𝐹𝑛.
Sample 1.
Input:
3
Output:
2
𝐹3 = 2.
Sample 2.
Input:
331
Output:
9
𝐹331 = 668 996 615 388 005 031 531 000 081 241 745 415 306 766 517 246 774 551 964 595 292 186 469.
4
Sample 3.
Input:
327305
Output:
5
𝐹327305 does not fit into one line of this pdf, but its last digit is equal to 5.
Need Help?
Ask a question or see the questions asked by other learners at this forum thread.
5
3 Greatest Common Divisor
Problem Introduction
The greatest common divisor GCD(𝑎, 𝑏) of two non-negative integers 𝑎 and 𝑏
(which are not both equal to 0) is the greatest integer 𝑑 that divides both 𝑎 and 𝑏.
Your goal in this problem is to implement the Euclidean algorithm for computing
the greatest common divisor.
Efficient algorithm for computing the greatest common divisor is an important
basic primitive of commonly used cryptographic algorithms like RSA.
GCD(1344, 217)
=GCD(217, 42)
=GCD(42, 7)
=GCD(7, 0)
=7
Problem Description
Task. Given two integers 𝑎 and 𝑏, find their greatest common divisor.
Input Format. The two integers 𝑎, 𝑏 are given in the same line separated by space.
Constraints. 1 ≤ 𝑎, 𝑏 ≤ 2 · 109.
Output Format. Output GCD(𝑎, 𝑏).
Sample 1.
Input:
18 35
Output:
1
18 and 35 do not have common non-trivial divisors.
Sample 2.
Input:
28851538 1183019
Output:
17657
28851538 = 17657 · 1634, 1183019 = 17657 · 67.
Need Help?
Ask a question or see the questions asked by other learners at this forum thread.
6
4 Least Common Multiple
Problem Introduction
The least common multiple of two positive integers 𝑎 and 𝑏 is the least positive
integer 𝑚 that is divisible by both 𝑎 and 𝑏.
Problem Description
Task. Given two integers 𝑎 and 𝑏, find their least common multiple.
Input Format. The two integers 𝑎 and 𝑏 are given in the same line separated by space.
Constraints. 1 ≤ 𝑎, 𝑏 ≤ 2 · 109.
Output Format. Output the least common multiple of 𝑎 and 𝑏.
Sample 1.
Input:
6 8
Output:
24
Among all the positive integers that are divisible by both 6 and 8 (e.g., 48, 480, 24), 24 is the smallest
one.
Sample 2.
Input:
28851538 1183019
Output:
1933053046
1933053046 is the smallest positive integer divisible by both 28851538 and 1183019.
Need Help?
Ask a question or see the questions asked by other learners at this forum thread.
7
5 Fibonacci Number Again
Problem Introduction
In this problem, your goal is to compute 𝐹𝑛 modulo 𝑚, where 𝑛 may be really huge: up to 1018. For such
values of 𝑛, an algorithm looping for 𝑛 iterations will not fit into one second for sure. Therefore we need to
avoid such a loop.
To get an idea how to solve this problem without going through all 𝐹𝑖 for 𝑖 from 0 to 𝑛, let’s see what
happens when 𝑚 is small — say, 𝑚 = 2 or 𝑚 = 3.
𝑖 0 1 2 3 4 5 6 7 8 9 10 11 12 13 14 15
𝐹𝑖 0 1 1 2 3 5 8 13 21 34 55 89 144 233 377 610
𝐹𝑖 mod 2 0 1 1 0 1 1 0 1 1 0 1 1 0 1 1 0
𝐹𝑖 mod 3 0 1 1 2 0 2 2 1 0 1 1 2 0 2 2 1
Take a detailed look at this table. Do you see? Both these sequences are periodic! For 𝑚 = 2, the period
is 011 and has length 3, while for 𝑚 = 3 the period is 01120221 and has length 8. Therefore, to compute,
say, 𝐹2015 mod 3 we just need to find the remainder of 2015 when divided by 8. Since 2015 = 251 · 8 + 7, we
conclude that 𝐹2015 mod 3 = 𝐹7 mod 3 = 1.
This is true in general: for any integer 𝑚 ≥ 2, the sequence 𝐹𝑛 mod 𝑚 is periodic. The period always
starts with 01 and is known as Pisano period.
Problem Description
Task. Given two integers 𝑛 and 𝑚, output 𝐹𝑛 mod 𝑚 (that is, the remainder of 𝐹𝑛 when divided by 𝑚).
Input Format. The input consists of two integers 𝑛 and 𝑚 given on the same line (separated by a space).
Constraints. 1 ≤ 𝑛 ≤ 1018, 2 ≤ 𝑚 ≤ 105.
Output Format. Output 𝐹𝑛 mod 𝑚.
Sample 1.
Input:
239 1000
Output:
161
𝐹239 mod 1 000 = 39 679 027 332 006 820 581 608 740 953 902 289 877 834 488 152 161 (mod 1 000) = 161.
Sample 2.
Input:
2816213588 30524
Output:
10249
𝐹2 816 213 588 does not fit into one page of this file, but 𝐹2 816 213 588 mod 30 524 = 10 249.
Need Help?
Ask a question or see the questions asked by other learners at this forum thread.
8
6 Last Digit of the Sum of Fibonacci Numbers
Problem Introduction
The goal in this problem is to find the last digit of a sum of the first 𝑛 Fibonacci numbers.
Problem Description
Task. Given an integer 𝑛, find the last digit of the sum 𝐹0 + 𝐹1 + · · · + 𝐹𝑛.
Input Format. The input consists of a single integer 𝑛.
Constraints. 0 ≤ 𝑛 ≤ 1014.
Output Format. Output the last digit of 𝐹0 + 𝐹1 + · · · + 𝐹𝑛.
Sample 1.
Input:
3
Output:
4
𝐹0 + 𝐹1 + 𝐹2 + 𝐹3 = 0 + 1 + 1 + 2 = 4.
Sample 2.
Input:
100
Output:
5
The sum is equal to 927 372 692 193 078 999 175, the last digit is 5.
What To Do
Instead of computing this sum in a loop, try to come up with a formula for 𝐹0 + 𝐹1 + 𝐹2 + · · · + 𝐹𝑛. For
this, play with small values of 𝑛. Then, use a solution for the previous problem.
Need Help?
Ask a question or see the questions asked by other learners at this forum thread.
9
7 Last Digit of the Sum of Fibonacci Numbers Again
Problem Introduction
Now, we would like to find the last digit of a partial sum of Fibonacci numbers: 𝐹𝑚 + 𝐹𝑚+1 + · · · + 𝐹𝑛.
Problem Description
Task. Given two non-negative integers 𝑚 and 𝑛, where 𝑚 ≤ 𝑛, find the last digit of the sum 𝐹𝑚 + 𝐹𝑚+1 +
· · · + 𝐹𝑛.
Input Format. The input consists of two non-negative integers 𝑚 and 𝑛 separated by a space.
Constraints. 0 ≤ 𝑚 ≤ 𝑛 ≤ 1018.
Output Format. Output the last digit of 𝐹𝑚 + 𝐹𝑚+1 + · · · + 𝐹𝑛.
Sample 1.
Input:
3 7
Output:
1
𝐹3 + 𝐹4 + 𝐹5 + 𝐹6 + 𝐹7 = 2 + 3 + 5 + 8 + 13 = 31.
Sample 2.
Input:
10 10
Output:
5
𝐹10 = 55.
Sample 3.
Input:
10 200
Output:
2
𝐹10 + 𝐹11 + · · · + 𝐹200 = 734 544 867 157 818 093 234 908 902 110 449 296 423 262
Need Help?
Ask a question or see the questions asked by other learners at this forum thread.
10

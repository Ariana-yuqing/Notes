
Family Name: Peng 
Given Name: Yuqing
Paper Title: Eraser: A Dynamic Data Race Detector for Multi-Threaded Programs

1) The problem: 
Timing-dependent data races are hard to avoid and debug in multi-threaded programming. Previous work is mostly based on happens-before relation, but there are still some unsolved problems.

2) New Idea(s): 

- Instead of based on _happens-before_ relation, which is sensitive to scheduler interleaving, Eraser calculates the lock set of each shared variable in the heap or globel data to make sure Eraser will cover every possible shared variables.

3) Positive points:

- The paper is very well written and provides sufficient details about the idea, implementation and experiments.
- Eraser is less sensitive to the scheduler interleaving, so the result is more accurate and reliable. Alse, Eraser is able to cover more test cases.
- The paper presents a large number of different types of experiments to support their points.

4) Negative points:

- The paper includes a lot of experiments, but I do not see a huge difference between some of them. Also, the author explains the experiments with so many details that it is hard for me to get the point of the experiments. It is also not fun to read.

5) Discussion:

- The author mentioned that previous work is sensitive to scheduler interleaving, but little context was provided. I am not sure what the author means exactly and why _happens-before_ is highly dependent on the scheduler interleaving.



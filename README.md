# Applied Statistics Assessment

This is my README for my assessment for the module Applied Statistics

Author: Owen Coughlan

Email: g00439345@atu.ie


# Problem 1 - Extending the Lady Tasting Tea

## What I Did
For this project, I took the original Lady Tasting Tea idea (8 cups total) and extended it to a bigger setup with 12 cups.  
This time we have:

- 8 cups where tea was poured first  
- 4 cups where milk was poured first  

The participant has to guess which 4 cups had milk first. The main question I wanted to answer was if someone was just guessing, what’s the chance they’d get all the cups right?


## How I Simulated It
To figure this out, I wrote a small simulation:

1. Label the 12 cups as numbers from 0 to 11.
2. Randomly pick 4 of them to represent the real milk-first cups.
3. Then randomly pick 4 cups again to represent the participant’s guess.
4. Check if the guessed set matches the real set exactly.
5. Repeat that process thousands of times and see how often a perfect match happens.

It's basically simulating a person just guessing randomly.

## What I Found
The simulation showed that the chance of randomly getting everything right is around:

### About 0.002 (or 0.2%)

To double-check, I also calculated the exact probability:

$$
1 / \binom{12}{4} = 1 / 495 \approx 0.00202
$$

So the simulation and the theoretical value match up really well.

For comparison:
- Original 8-cup experiment:  
  1/70 ≈ 0.0143 (about 1.4%)
- Extended 12-cup experiment:  
  1/495 ≈ 0.002 (about 0.2%)

So with the bigger setup, a perfect guess is way less likely just by chance.

## What This Means
Basically, the 12 cup version makes it much harder for someone who’s guessing to get everything correct.  
If someone actually did get all 4 milk-first cups right in this extended version, it would be much stronger evidence that they really can tell the difference.

## About the p-value Threshold
In the original experiment, a perfect score had a p-value around 0.014.  
In the extended version, it drops to about 0.002.

So what does that mean?

- You can keep the same significance level (like 0.05) and the extended design already beats it easily.
- Or you could actually relax it a bit (maybe allow a small mistake), because even then the chance of someone passing just by luck is still extremely low.

## Final Thoughts
Increasing the number of cups makes the test much stricter, and random guessing performs way worse.  
So the extended experiment gives much stronger evidence if someone gets a perfect (or near perfect) result.


## References  

- Wikipedia. “Lady Tasting Tea.” - https://en.wikipedia.org/wiki/Lady_tasting_tea  
- NumPy Documentation. - https://numpy.org/doc/  
- Khan Academy, Probability and Combinations. - https://www.khanacademy.org/math/statistics-probability/counting-permutations-and-combinations


# Problem 2 - Normal Distribution

In this part of my project, I’m running a simulation to compare two different methods for calculating standard deviation. The plan is to generate 100,000 samples, each containing 10 values drawn from a standard normal distribution. For each sample, I’ll compute the standard deviation in two different ways: once using the sample standard deviation (where ddof = 1) and once using the population standard deviation (where ddof = 0).

Before I ran the code, I just wanted to see if the two formulas behaved differently when we repeated the experiment a ton of times. Since ddof = 1 and ddof = 0 divide by different values, I figured they wouldn't match up perfectly, especially with a smaller sample size.

To kick things off, I imported NumPy and Matplotlib. These libraries helped me generate the data and create some plots later on. After setting a seed to ensure consistent results, I created 100,000 samples from the normal distribution.

Next, I calculated the standard deviations using both methods for each sample, leading to two separate arrays of standard deviation values. Once I had those, I plotted them on the same histogram, using some transparency to see how they overlapped. The idea was to visually check how similar or different they were.

## Observations

When I looked at the histogram, I noticed that the two curves overlapped quite a bit, which makes sense since both formulas are trying to measure the same spread. However, there was a clear difference: the sample SD (ddof=1) sat a bit further to the right, while the population SD (ddof=0) leaned slightly to the left. Before creating the plot, I jotted down a note explaining that ddof=1 applies Bessel’s correction by dividing by n–1, which typically makes the sample SD a bit larger on average. Seeing this difference pop up in my simulation pretty much confirmed what the theory suggested.

## What Happens If We Increase the Sample Size?

I also wrote a note in my notebook about what I expected if the sample size increased (like going from 10 to 50 or even 100). I figured that as the sample size grows, the factor \( \frac{n}{n-1} \) gets closer to 1. This would lead to a much smaller difference between the two SD values, and I anticipated that both histograms would narrow and concentrate more closely around the true SD (which is 1 for the standard normal). So, with a large enough sample size, I expected that the two histograms would nearly overlap completely.

## References

- NumPy Documentation - https://numpy.org/doc/stable/reference/generated/numpy.std.html
- SciPy Lecture Notes - https://scipy-lectures.org/intro/scipy.html#statistics
- Khan Academy - Sample vs Population Standard Deviation — https://www.khanacademy.org/math/statistics-probability

# Problem 3 - t-Tests

In this part of the project, I’m looking at type II error, which is when we don’t reject the null hypothesis even though there actually is a difference. 

The goal here was to see how often that happens when the true difference in means gets bigger.

To do this, I ran a simulation for different mean differences \(d = 0, 0.1, 0.2, \dots, 1.0\). For each \(d\), I repeated the same experiment 1,000 times. Each time, I generated two independent samples of size 100:

- Sample A was drawn from a standard normal distribution, \(N(0,1)\)
- Sample B was drawn from \(N(d,1)\)

Then I ran an independent samples t-test on the two samples. I treated it like a normal hypothesis test: if the p-value was less than 0.05, I rejected \(H_0\). Otherwise, I didn’t reject. Since Sample B is generated with mean \(d\), when \(d > 0\) the null hypothesis (no difference in means) is false, so the times I fail to reject \(H_0\) are basically my type II errors. I stored the proportion of “no reject” results for each \(d\) and plotted it against \(d\).

## Observations
When \(d = 0\), the two distributions are the same, so the null hypothesis is actually true. In that case, the test shouldn’t reject very often, and the proportion of “no reject” should be high (roughly around 0.95 because the significance level is 0.05).

As \(d\) increases, the two groups become more separated, so it gets easier for the t-test to pick up the difference. On the plot, the type II error rate drops as \(d\) gets larger. This makes sense because the test has more “signal” to work with when the mean difference is bigger.

So overall, the main pattern was that bigger mean difference meant the lower type II error rate (higher power).

## References
- NumPy Random Normal Documentation — https://numpy.org/doc/stable/reference/random/generated/numpy.random.normal.html  
- SciPy t-test Documentation — https://docs.scipy.org/doc/scipy/reference/generated/scipy.stats.ttest_ind.html  
- Khan Academy (Type I and Type II Errors) — https://www.khanacademy.org/math/statistics-probability/significance-tests-confidence-intervals-new/type-1-errors/v/type-i-and-type-ii-errors
- OpenIntro Statistics (Hypothesis Testing Errors) — https://www.openintro.org/book/os/

# Problem 4 - Anova

The aim of this problem is to simulate three groups from normal distributions with different means, and then test whether the group means look equal statistically.

## What I Did

For this problem I generated three independent samples, each with:

- Sample size: n = 30  
- Standard deviation: 1  
- Means:  
  - Group 1: mean = 0  
  - Group 2: mean = 0.5  
  - Group 3: mean = 1  

After generating the data, I used two approaches:

1. One-way ANOVA to test the overall question:  
 “Are all three population means equal?”

2. Three pairwise two-sample t-tests (two-sided):  
  - Sample 1 vs Sample 2  
  - Sample 1 vs Sample 3  
  - Sample 2 vs Sample 3  

I also included a quick Bonferroni check to show what happens if you adjust for multiple comparisons.

## Results
In the notebook you’ll see:

- A histogram + boxplot to get a feel for how much the three groups overlap.
- The ANOVA F-statistic and p-value (one overall test).
- The three t-test p-values (pair-by-pair comparisons).
- A comparison section explaining how the conclusions can line up (or differ), depending on random sampling and the significance level.

# Applied Statistics Assessment

This is my README for my assessment for the module Applied Statistics

Author: Owen Coughlan

Email: g00439345@atu.ie


# Problem 1: Extending the Lady Tasting Tea

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




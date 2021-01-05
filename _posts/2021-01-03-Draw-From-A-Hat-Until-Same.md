---
title: "Using Markov Chains and Monte Carlo to solve probability questions"
excerpt_separator: "<!--more-->"
categories:
  - Blog
tags:
  - probability
  - monte carlo
  - markov chain
---

The problem: suppose you have a hat with the numbers from 1 to N. Lets say you pick out with replacement, N-numbers, and write them down. Now replace the numbers in the hat with the new numbers you've written down. Draw another N-numbers and repeat. On average, how many draws do you need before all of the numbers are the same?

Let's look at this from the standpoint of N = 3. When N = 3, we have the numbers [1, 2, 3] in our hat. Let's draw N-numbers, so 3 numbers. Suppose we get [1,1,3]. We replace our old hat numbers with this new batch, and draw again. Maybe we'll get [1,1,1]. If so, then we're done! And in 2-steps no less!

But maybe we get unlucky. Maybe we get so unlucky that it takes us 100 tries before we get it! So our question is, on AVERAGE, what is the probability of getting to that final state?

Well, let's use the N = 3 example. There are 3 possible states.
1. All numbers of unique
2. 2 of one number, 1 of another
3. All 3 numbers are the same

In other words, that maximum number of a single element in the set is 1, 2, or 3. We're given that we start at state 1, where all the numbers are unique. We have the numbers from 1 to N in our hat after all. When we draw numbers out of the hat, there are a few possibilities.

We could go from state 1 and get the same 3 numbers, in which case we didn't go anywhere. We could draw 2 numbers the same and one different, and advance to state 2. Or we could draw all 3 numbers the same and go immediately to state 3! Do not collect $200.

What's the probabilities of each occurring? Well for the first case, to draw 3 individual numbers from 3 is 2/9. That's because there's a 3/3 chance of picking the first number, a 2/3 chance of picking one of the other two numbers, and a 1/3 chance of picking the last number to complete our set. That's 2/9.

For the last case of all numbers the same, that's a 1/27 chance for it to happen for any number! Because there are 3 numbers, the total probability of that situation is 1/9.

If we decide to use the laws of probability, our life would be easy and we could say that to reach state 2 we would need 6/9, or 2/3 probability because our total probabilities must equal 1. True, but let's do it the other way.

We're looking at a binomial distribution here. Out of the 3 numbers, we need to choose 2 of them. Then we have a 1/9 chance of getting 2 of those numbers, and a 2/3 of getting any of the other two. This results in a probability of 2/9. How do we get 2/3? Well, we're missing the fact that there are 3 possible numbers to choose from!

The combination 3 choose 2 only decides how many ways can we choose 2 numbers out of 3. It doesn't tell us which of the numbers is double and which one is the single! That means we need to account for each of the 3 numbers being the double, which means we multiply by 3 and get a total probability of 2/3.

Perfect.

Let's now go on from state 2. Fortunately for us, state 2 means we have 2 numbers being the same. This, however, means that we've gotten rid of a number to accommodate the duplicate! This means it's impossible for state 2 to go back to state 1, because at best, we'd only be back at state 2! We can't recover that number that we've lost. That makes our lives a bit easier.

At state 2, the worst we get is to return to state 2. The best case is to go to state 3, and be done. The probability of reaching state 3 is 1/3.

We have a 1/3 chance to choose the less likely number, which means we have to do that two more for a total of 1/27. What about if we pick the 2/3 number? Then we have an 8/27 chance of picking that three times! This totals to 9/27 or 1/3!

With our rules of probability, then we must know that the probability that state 2 remains at state 2 is 2/3 so the probabilities can equal 1.

Turns out our overly complex explanation can be easily summarized in a Markov Chain! If you don't know what they are, I highly recommend reading about them [here](https://en.wikipedia.org/wiki/Markov_chain).

The cool thing about MCs is that we can directly solve for our expected value problem here! We write our MC in a transition matrix. If you're familiar with graphs, this is the adjacency matrix associated with this graph! We can use this to solve our problem!

To do so, I'll refer to [this PDF](http://www.aquatutoring.org/ExpectedValueMarkovChains.pdf), but I'll skip the details. When we chug out the math, we get a whopping 27/7. How do we know this is right?

Let's simulate it! We can use the method of Monte Carlo, or basically just a bunch of mass simulations to test our random processes. With a pretty short Python code, we get a simulated average of 3.855! Super close to the true value.

So that's that. Pretty easy right? Now let's try with N = 4...

Just kidding. Just run the simulation, come back after some water, and get our answer. From random processes, Monte Carlo works just fine.
